## 📸 影像處理基礎學習筆記 (MATLAB)

### 1. 基礎操作與資料型態

這部分涵蓋了影像的讀取、顯示以及像素的基本檢查。

Matlab

```
% Read a grayscale image
I = imread('cameraman.tif');

% Display the image
imshow(I);
title('Original Image');

% Check image size and data type
size(I)    % Image dimensions (e.g., 256x256)
class(I)   % Data type (usually uint8: 0-255)

% Convert image to double precision for analysis (Scale to [0,1])
I_double = im2double(I);

% Inspect value range
min(I_double(:))
max(I_double(:))
```

### 2. 像素級存取與視覺化

了解如何在矩陣中定位特定的像素點。

Matlab

```
% Access a single pixel value
pixel_value = I(100, 150); % Row 100, Column 150

% Display pixel value
disp(pixel_value);

% Visualize pixel location
imshow(I);
hold on;
% Note: plot uses (x, y) which is (column, row)
plot(150, 100, 'r+', 'MarkerSize', 10, 'LineWidth', 2);
title('Pixel Location (row=100, col=150)');
hold off;
```

---

### 3. 強度變換 (Intensity Transformation)

透過線性縮放或自動調整來改善影像對比度。

Matlab

```
% Convert image to double for intensity manipulation
I = im2double(I);

% Linear intensity scaling (Increase brightness)
I_scaled = I * 1.5;

% Clip values to valid range [0, 1]
I_scaled(I_scaled > 1) = 1;

imshow(I_scaled);
title('Linearly Scaled Intensity');

% Contrast stretching using imadjust (Automatic normalization)
I_stretch = imadjust(I);

imshow(I_stretch);
title('Contrast Stretched Image');
```

### 4. 幾何變換 (Geometric Transformation)

包含旋轉以及更進階的仿射變換（縮放與平移）。

Matlab

```
% Rotate image by 30 degrees
I_rot = imrotate(I, 30);

imshow(I_rot);
title('Rotated Image (30 degrees)');

% Create an affine transformation (scaling + translation)
% Matrix: [scaleX  shearY  0; shearX  scaleY  0; transX  transY  1]
tform = affine2d([1.2 0   0;
                  0   1.2 0;
                  30  20  1]);

% Apply transformation
I_affine = imwarp(I, tform);

imshow(I_affine);
title('Affine Transformed Image');
```

---

### 5. 頻域分析 (Frequency Domain)

利用快速傅立葉變換 (FFT) 觀察影像的頻譜。

Matlab

```
% Read image and convert to double
I = imread('cameraman.tif');
I = im2double(I);

% Compute 2D FFT
F = fft2(I);

% Shift zero-frequency component to center
F_shift = fftshift(F);

% Display magnitude spectrum (using log to visualize details)
figure;
imshow(log(1 + abs(F_shift)), []);
title('Magnitude Spectrum (FFT)');
```

### 6. 頻域濾波 (Frequency Domain Filtering)

使用理想低通濾波器 (Ideal Low-pass Filter) 來達成模糊效果。

Matlab

```
% Create frequency grid
[M, N] = size(I);
[u, v] = meshgrid(-N/2:N/2-1, -M/2:M/2-1);
D = sqrt(u.^2 + v.^2); % Distance from center

% Ideal low-pass filter
D0 = 50; % Cutoff frequency
H = double(D <= D0);

% Apply filter in frequency domain
G = H .* F_shift;
I_lp = real(ifft2(ifftshift(G)));

% Display result
imshow(I_lp, []);
title('Low-pass Filtered Image');
```

---

### 7. 影像退化與復原 (Restoration)

模擬運動模糊並嘗試使用維納濾波 (Wiener Filter) 進行修復。

Matlab

```
% --- 影像退化 (Blurring) ---
% Create motion blur PSF (Point Spread Function)
psf = fspecial('motion', 15, 30);

% Apply blur
I_blur = imfilter(I, psf, 'conv', 'circular');

imshow(I_blur);
title('Motion Blurred Image');

% --- 影像復原 (Restoration) ---
% Wiener deconvolution
I_restored = deconvwnr(I_blur, psf);

imshow(I_restored);
title('Restored Image (Wiener Filter)');
```

### 8. 雜訊處理與濾波 (Noise & Denoising)

比較高斯雜訊與椒鹽雜訊，並使用對應的空間域濾波器。

Matlab

```
% --- 添加雜訊 (Adding Noise) ---
% Add Gaussian noise
I_gauss = imnoise(I, 'gaussian', 0, 0.01);

% Add salt & pepper noise
I_sp = imnoise(I, 'salt & pepper', 0.05);

figure;
subplot(1,2,1), imshow(I_gauss), title('Gaussian Noise');
subplot(1,2,2), imshow(I_sp), title('Salt & Pepper Noise');

% --- 去除雜訊 (Denoising) ---
% Remove Gaussian noise using average filter (Linear)
I_avg = imfilter(I_gauss, fspecial('average', 3));

% Remove salt & pepper noise using median filter (Non-linear)
I_med = medfilt2(I_sp);

figure;
subplot(1,2,1), imshow(I_avg), title('Mean Filter Result');
subplot(1,2,2), imshow(I_med), title('Median Filter Result');
```

---

**💡 學習筆記重點摘要：**

1. **中值濾波 (Median Filter)** 對於處理「椒鹽雜訊」的效果遠好於平均濾波。
    
2. **頻域處理** 適合處理週期性雜訊或進行特定的頻譜過濾。
    
3. **維納濾波** 在已知模糊函數 (PSF) 的情況下，是復原影像的強大工具。
    
