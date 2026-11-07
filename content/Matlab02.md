## 🤖 電腦視覺與相機幾何學習筆記 (MATLAB)

### 1. 特徵檢測與影像梯度

了解如何透過梯度找到影像中的邊緣與關鍵點。

Matlab

```
% --- 影像梯度 (Image Gradients) ---
I = imread('cameraman.tif');
I = im2double(I);

% 計算 x 與 y 方向的梯度
[Gx, Gy] = imgradientxy(I);

% 計算梯度幅值與方向
[Gmag, Gdir] = imgradient(Gx, Gy);

% 顯示梯度幅值
imshow(Gmag, []);
title('Gradient Magnitude');

% --- Harris 角點檢測 (Harris Corner Detection) ---
% 偵測影像中的角點特徵
corners = detectHarrisFeatures(I);

% 顯示最強的前 100 個角點
imshow(I); hold on;
plot(corners.selectStrongest(100));
title('Harris Corners');
hold off;

% --- 高斯平滑 (Gaussian Smoothing) ---
% 使用不同尺度的 Sigma 進行平滑處理
I_sigma1 = imgaussfilt(I, 1);
I_sigma3 = imgaussfilt(I, 3);

figure;
subplot(1,2,1), imshow(I_sigma1), title('Sigma = 1');
subplot(1,2,2), imshow(I_sigma3), title('Sigma = 3');
```

---

### 2. 相機標定 (Camera Calibration)

這是獲取相機內部參數（焦距、畸變等）的關鍵步驟。

Matlab

```
% 載入標定用圖片集
images = imageDatastore('calib_images');

% 偵測棋盤格角點
[imagePoints, boardSize] = detectCheckerboardPoints(images.Files);

% 定義棋盤格方塊的實際尺寸 (例如 25mm)
squareSize = 25;
worldPoints = generateCheckerboardPoints(boardSize, squareSize);

% 估計相機參數
% 最小化重投影誤差：min Σ ||x_i - x_hat_i(K, D, R, t)||^2
params = estimateCameraParameters(imagePoints, worldPoints);

% 顯示重投影誤差以評估精確度
showReprojectionErrors(params);
```

> [!NOTE] 參數定義
> 
> - **K**: 相機內參矩陣 (Intrinsic matrix)
>     
> - **D**: 畸變參數 (Distortion parameters)
>     
> - **R, t**: 外參 (Extrinsic parameters - 旋轉與平移)
>     

---

### 3. 影像去畸變與位姿估計

校正鏡頭扭曲並計算相機在 3D 空間中的位置。

Matlab

```
% --- 影像去畸變 (Undistortion) ---
I = imread(images.Files{1});
I_undistorted = undistortImage(I, params); % 移除鏡頭畸變

% 視覺化對比原始與校正後的影像
imshowpair(I, I_undistorted, 'montage');
title('Original vs Undistorted Image');

% --- 相機位姿估計 (Pose Estimation) ---
% 從 2D-3D 對應點估計相機位姿 (解決 PnP 問題)
[orientation, location] = estimateWorldCameraPose(imagePoints, worldPoints, params);

% 顯示計算結果
disp('Camera Orientation (Rotation Matrix):');
disp(orientation);
disp('Camera Location (World Coordinates):');
disp(location);
```

---

### 4. 3D 視覺化 (3D Visualization)

將估計出的相機位置與 3D 世界點繪製出來，進行偵錯與驗證。

Matlab

```
% 在 3D 空間中視覺化相機位姿
figure;
plotCamera('Location', location, 'Orientation', orientation, 'Size', 50);
hold on;

% 繪製 3D 世界參考點
plot3(worldPoints(:,1), worldPoints(:,2), worldPoints(:,3), 'r.');
grid on;
title('Estimated Camera Pose');
```

---

**💡 進階筆記重點：**

- **為什麼要視覺化？**：可以驗證位姿的合理性 (Plausibility)、理解相機與物體的相對位置，並協助調試估計誤差。
    
- **相機標定流程**：偵測特徵點 $\rightarrow$ 生成世界坐標 $\rightarrow$ 優化參數 $\rightarrow$ 去畸變校正。
    
- **MATLAB 高階工具**：提供了快速解決 PnP 問題（Perspective-n-Point）、處理雜訊與不確定性的內建函式。
    
