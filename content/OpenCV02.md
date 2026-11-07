# 🖼️ 數位影像處理學習筆記 (MATLAB)

## 一、 影像基礎與資料型態

在進行任何處理前，必須先了解影像的維度與數值型態。

Matlab

```
% 1. 讀取與顯示
I = imread('cameraman.tif');
imshow(I);
title('Original Image');

% 2. 檢查屬性
size(I)    % 影像尺寸 [高, 寬]
class(I)   % 資料型態 (通常為 uint8, 0-255)

% 3. 轉換為倍精度浮點數 (Scale to [0,1])
% 大多數進階運算 (如 FFT) 都建議在 double 型態下執行
I_double = im2double(I);

% 4. 檢查範圍
min(I_double(:))
max(I_double(:))
```

---

## 二、 像素存取與強度變換

學習如何精確定位像素並調整影像的視覺效果（亮度與對比）。

### 1. 像素存取與標記

Matlab

```
% 存取特定位置：第 100 列, 第 150 行
pixel_value = I(100, 150);
disp(pixel_value);

% 在影像上標記點
imshow(I); hold on;
% 注意：plot(x, y) 的 x 是行(col), y 是列(row)
plot(150, 100, 'r+', 'MarkerSize', 10, 'LineWidth', 2);
title('Pixel Location (row=100, col=150)');
hold off;
```

### 2. 強度縮放與對比調整

Matlab

```
% 線性亮度縮放 (乘法)
I_scaled = I_double * 1.5;
I_scaled(I_scaled > 1) = 1; % 飽和處理：超過 1 的設為 1

% 自動對比拉伸 (Contrast Stretching)
I_stretch = imadjust(I_double);

subplot(1,2,1), imshow(I_scaled), title('Linearly Scaled');
subplot(1,2,2), imshow(I_stretch), title('Contrast Stretched');
```

---

## 三、 幾何變換 (Geometric Transformations)

Matlab

```
% 1. 影像旋轉 (逆時針 30 度)
I_rot = imrotate(I, 30);

% 2. 仿射變換 (Affine Transformation)
% 矩陣結構：[縮放X 錯切Y 0; 錯切X 縮放Y 0; 平移X 平移Y 1]
tform = affine2d([1.2 0   0; 
                  0   1.2 0; 
                  30  20  1]);
I_affine = imwarp(I, tform);
```

---

## 四、 頻域分析與濾波 (Frequency Domain)

利用傅立葉變換處理影像特徵。

Matlab

```
% 1. 計算 2D FFT 並移動低頻至中心
F = fft2(I_double);
F_shift = fftshift(F);

% 2. 顯示振幅譜 (Magnitude Spectrum)
% 加 1 並取 log 是為了壓縮動態範圍，讓細節看得見
imshow(log(1 + abs(F_shift)), []);
title('Magnitude Spectrum (FFT)');

% 3. 理想低通濾波 (Ideal Low-pass Filter)
[M, N] = size(I);
[u, v] = meshgrid(-N/2:N/2-1, -M/2:M/2-1);
D = sqrt(u.^2 + v.^2); % 計算與頻域中心的距離
D0 = 50;               % 截止頻率
H = double(D <= D0);   % 建立遮罩

% 4. 套用濾波器並反變換 (IFFT)
G = H .* F_shift;
I_lp = real(ifft2(ifftshift(G)));
imshow(I_lp, []);
title('Low-pass Filtered Image');
```

---

## 五、 影像退化、復原與雜訊處理

模擬現實生活中的影像損毀並進行修復。

### 1. 運動模糊與維納濾波 (Restoration)

Matlab

```
% 模擬運動模糊
psf = fspecial('motion', 15, 30);
I_blur = imfilter(I, psf, 'conv', 'circular');

% 維納濾波復原 (Wiener Deconvolution)
% 在已知 PSF 的情況下進行反摺積
I_restored = deconvwnr(I_blur, psf);
```

### 2. 雜訊處理 (Denoising)

Matlab

```
% 注入雜訊
I_gauss = imnoise(I, 'gaussian', 0, 0.01);
I_sp = imnoise(I, 'salt & pepper', 0.05);

% 去除雜訊的策略
I_avg = imfilter(I_gauss, fspecial('average', 3)); % 平均濾波 (適合高斯)
I_med = medfilt2(I_sp);                           % 中值濾波 (適合椒鹽)

figure;
subplot(1,2,1), imshow(I_avg), title('Mean Filter (Gaussian)');
subplot(1,2,2), imshow(I_med), title('Median Filter (S&P)');
```

---

> [!TIP] **快速複習筆記**
> 
> - **im2double**: 影像運算的基礎，避免運算時溢位。
>     
> - **fftshift**: 將背景低頻成分移到影像中央，方便設計濾波器。
>     
> - **中值濾波 (Median)**: 去除椒鹽雜訊（黑白點）效果奇佳，且比平均濾波更能保留邊緣線條。
>     
