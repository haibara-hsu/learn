
> 🎯 本章核心目標：理解影像在「頻率域」中的濾波方法，以及其數學基礎與工程應用。

---

# **一、頻率域濾波的基本理解**

  

## **1. 了解什麼是 Frequency Domain Filtering**

- 能解釋什麼是頻率域濾波
    
- 能說明它與空間域濾波（Spatial Domain Filtering）的差異
    

  

### **核心對比**

|**空間域**|**頻率域**|
|---|---|
|直接對像素做運算|對頻率成分做運算|
|卷積|乘法|
|操作局部區域|操作整體頻率結構|

---

# **二、取樣與訊號理論基礎**

  

## **2. 取樣（Sampling）**

- 了解取樣的概念
    
- 知道 Nyquist 條件
    

  

## **3. 函數重建（Function Reconstruction）**

- 了解如何從取樣資料重建原始訊號
    
- 理解理想重建條件
    

  

## **4. 混疊（Aliasing）**

- 知道 aliasing 發生原因
    
- 理解取樣頻率不足的後果
    
- 能解釋為什麼會產生錯誤頻率成分
    

---

# **三、頻率域中的卷積**

  

## **5. 頻率域卷積概念**

- 理解：
    

  

f(x,y) * h(x,y) \quad \Longleftrightarrow \quad F(u,v)H(u,v)

- 知道：
    
    - 空間域的卷積
        
    - 等價於頻率域的乘法
        
    
- 理解為什麼這件事等於「濾波」
    

---

# **四、濾波器的建立方式**

  

## **6. 從空間 kernel 推導頻率響應**

- 能將 spatial kernel 轉換成 frequency response
    
- 知道如何透過 Fourier Transform 得到濾波函數
    

  

## **7. 直接在頻率域設計濾波器**

- 能直接建立 transfer function
    
- 例如：
    
    - Ideal filter
        
    - Butterworth filter
        
    - Gaussian filter
        
    

---

# **五、影像補零（Padding）**

  

## **8. 為什麼 Padding 很重要？**

- 防止循環卷積（circular convolution）
    
- 避免邊界失真
    
- 保證線性卷積結果正確
    

---

# **六、頻率域濾波步驟**

  

## **9. 頻率域濾波標準流程**

1. 影像 padding
    
2. 計算 FFT
    
3. 中心化頻譜（可選）
    
4. 與濾波函數相乘
    
5. 計算 inverse FFT
    
6. 取實部
    
7. 裁切回原尺寸
    

---

# **七、什麼時候用頻率域比較好？**

  

## **10. 頻率域優勢判斷**

- 當 kernel 很大時
    
- 當需要全域操作時
    
- 當使用 FFT 計算量較小時
    

  

比較基準：

|**Kernel 大小**|**推薦方法**|
|---|---|
|小|空間域|
|大|頻率域|

---

# **八、其他頻率域濾波技巧**

  

## **11. Unsharp Masking**

- 增強高頻
    
- 提升影像銳利度
    

  

## **12. Homomorphic Filtering**

- 同時處理 illumination 與 reflectance
    
- 常用於光照補償
    

---

# **九、Fast Fourier Transform (FFT)**

  

## **13. FFT 的來源與機制**

- 將 DFT 複雜度從：
    

  

O(N^2)

  

降低為：

  

O(N \log N)

  

## **14. 在影像處理中的應用**

- 快速頻率分析
    
- 快速濾波
    
- 大尺寸卷積
    

---

# **🔎 整章能力總結**

  

完成本章後，你應該能：

- 解釋頻率域濾波原理
    
- 分析 aliasing 問題
    
- 推導卷積對應關係
    
- 建立濾波 transfer function
    
- 完成頻率域濾波流程
    
- 判斷空間域 vs 頻率域的使用時機
    
- 理解 FFT 的數學基礎與效率來源
    
