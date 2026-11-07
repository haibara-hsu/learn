# 🖼️ 數位影像處理學習筆記 (MATLAB)

## 一、 基礎操作與資料型態

在處理影像前，必須先了解影像的維度與數值型態。

Matlab

```
% 1. 讀取並顯示影像
I = imread('cameraman.tif');
imshow(I);
title('Original Image');

% 2. 檢查影像資訊
size(I)    % 取得解析度 (M x N)
class(I)   % 檢查資料型態 (通常為 uint8, 範圍 0-255)

% 3. 轉換為倍精度浮點數 (Scale to [0, 1])
% 這是進行數學運算（如 FFT）前的必要步驟
I_double = im2double(I);

% 4. 檢查數值範圍
min(I_double(:))
max(I_double(:))
```

---

## 二、 像素存取與強度變換

學習如何操作單一像素，以及調整影像的對比度與亮度。

### 1. 像素存取 (Pixel Access)

Matlab

```
% 存取特定位置像素：row 100, col 150
pixel_value = I(100, 150);
disp(pixel_value);

% 在影像上標註特定位置
imshow(I); hold on;
plot(150, 100, 'r+', 'MarkerSize', 10, 'LineWidth', 2);
title('Pixel Location (row=100, col=150)');
hold off;
```

### 2. 強度縮放與對比調整

Matlab

```
% 線性縮放 (變亮)
I_scaled = I_double * 1.5;
I_scaled(I_scaled > 1) = 1; % 飽和處理 (Clipping)

% 自動對比拉伸 (Contrast Stretching)
I_stretch = imadjust(I_double);

subplot(1,2,1), imshow(I_scaled), title('Linearly Scaled');
subplot(1,2,2), imshow(I_stretch), title('Contrast Stretched');
```

---

## 三、 幾何變換 (Geometric Transformations)

影像的旋轉、縮放與平移。

Matlab

```
% 1. 旋轉 30 度
I_rot = imrotate(I, 30);

% 2. 仿射變換 (Affine Transformation)
% 定義轉換矩陣 [Scale, Shear, Translate]
tform = affine2d([1.2 0   0; 
                  0   1.2 0; 
                  30  20  1]);
I_affine = imwarp(I, tform);
```

---

## 四、 頻域分析與濾波 (Frequency Domain)

利用傅立葉變換將影像從空間域轉為頻率域，進行低通濾波。

Matlab

```
% 1. 計算 2D FFT 並移動零頻率分量至中心
F = fft2(im2double(I));
F_shift = fftshift(F);

% 顯示振幅譜 (Magnitude Spectrum)
% 使用 log 壓縮動態範圍以便觀察
imshow(log(1 + abs(F_shift)), []);
title('Magnitude Spectrum (FFT)');

% 2. 建立理想低通濾波器 (Ideal Low-pass Filter)
[M, N] = size(I);
[u, v] = meshgrid(-N/2:N/2-1, -M/2:M/2-1);
D = sqrt(u.^2 + v.^2); % 計算與中心的距離
D0 = 50;               % 截止頻率
H = double(D <= D0);

% 3. 應用濾波器並轉回空間域
G = H .* F_shift;
I_lp = real(ifft2(ifftshift(G)));
imshow(I_lp, []);
```

---

## 五、 影像退化、復原與雜訊處理

模擬影像受損並嘗試修復。

### 1. 運動模糊與維納濾波 (Restoration)

Matlab

```
% 模擬運動模糊
psf = fspecial('motion', 15, 30);
I_blur = imfilter(I, psf, 'conv', 'circular');

% 維納濾波復原 (Wiener Deconvolution)
I_restored = deconvwnr(I_blur, psf);
```

### 2. 雜訊去除 (Denoising)

Matlab

```
% 加入雜訊
I_gauss = imnoise(I, 'gaussian', 0, 0.01);
I_sp = imnoise(I, 'salt & pepper', 0.05);

% 去除雜訊
I_avg = imfilter(I_gauss, fspecial('average', 3)); % 平均濾波 (適合高斯)
I_med = medfilt2(I_sp);                           % 中值濾波 (適合椒鹽)

subplot(1,2,1), imshow(I_avg), title('Mean Filter (Gaussian)');
subplot(1,2,2), imshow(I_med), title('Median Filter (S&P)');
```

---

**💡 快速小結：**

- **im2double**：是處理影像的「起手式」，確保數值在 $[0, 1]$ 之間方便計算。
    
- **fftshift**：將低頻（背景、大輪廓）移到中間，高頻（邊緣、細節、雜訊）移到四周。
    
- **中值濾波 (Median)**：處理「點狀雜訊 (Salt & Pepper)」的神器，比平均濾波更能保留邊緣。
    

