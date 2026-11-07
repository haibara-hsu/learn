# 影像處理筆記：摺積與相關計算 (Digital Image Processing)

## 📋 核心觀念：摺積 vs. 相關
在空間濾波（Spatial Filtering）中，這兩者唯一的差異在於核心（Kernel）是否需要先進行 **180度旋轉**。

| 運算項目 | 核心處理 (Kernel Handling) | 數學特性 | 應用場景 |
| :--- | :--- | :--- | :--- |
| **摺積 (Convolution)** | 需先旋轉 180° (上下+左右翻轉) | 滿足結合律 $(A * B = B * A)$ | 影像濾波、CNN 特徵提取 |
| **相關 (Correlation)** | 直接滑動，不需翻轉 | 不滿足結合律 | 模板匹配 (Template Matching) |

> [!IMPORTANT] 關鍵對稱性
> 如果核心矩陣 $w$ 是**對稱的**（上下、左右對稱，如高斯濾波器），則摺積與相關的計算結果會**完全相同**。

---

## 🧮 實戰計算流程 (以 $3 \times 3$ 核心為例)
當題目要求計算影像 $f$ 在座標 $(r, c)$ 的輸出值時，請遵循以下步驟：

### Step 1: 擷取子區域 (Sub-image)
以影像 $f$ 的 $(r, c)$ 為中心，挖出與核心大小相同的區塊。
例如中心在 $(2, 3)$，則擷取：
$$f_{sub} = \begin{bmatrix} f(1,2) & f(1,3) & f(1,4) \\ f(2,2) & f(2,3) & f(2,4) \\ f(3,2) & f(3,3) & f(3,4) \end{bmatrix}$$

### Step 2: 點積運算 (Element-wise Multiplication)
將核心 $w$（若為摺積需翻轉）與 $f_{sub}$ 對應位置相乘。
$$Result = \sum w_{i,j} \cdot f_{i,j}$$

### Step 3: 加總 (Summation)
將所有乘積加起來，即為該像素點的最終輸出值。

---

## 🖼️ 邊界處理：零填充 (Zero Padding)
* **目的**：解決核心中心移動到影像邊緣時，部分區域超出範圍的問題。
* **做法**：在影像四周補上一圈或多圈數值為 $0$ 的像素。
* **輸出大小**：若輸入 $M \times N$，核心 $k \times k$，補零圈數 $P = (k-1)/2$，則輸出大小可維持 $M \times N$。

---

## ⚖️ 歸一化 (Normalization) 與 偏差 (Bias)

### 1. 偏差 (Bias)
* **定義**：在神經網路中常見公式 $y = (w * f) + b$，其中 $b$ 即為 Bias。
* **現象**：若核心總和（Sum of Weights）不等於 1，輸出影像會產生整體的亮度偏移（變亮或變暗）。

### 2. 歸一化 (Normalization)
* **目的**：確保處理後的影像亮度與原圖一致。
* **方法**：將核心中的每個元素除以核心所有元素的總和。
* **公式**：
  $$w_{norm} = \frac{1}{\sum w} \cdot w$$

> [!TIP] 範例
> 若核心元素總和為 $16$，則將核心乘以 $\frac{1}{16}$。常見的「均值濾波器」就是歸一化的代表。

---

## 🔖 複習檢查清單
- [ ] **座標定位**：確認題目給的是 (Row, Col) 還是 (x, y)。
- [ ] **對稱檢查**：核心是否對稱？（對稱則 Convolution = Correlation）。
- [ ] **權重總和**：核心加起來等於 1 嗎？如果不等於，影像亮度會變。
- [ ] **填充策略**：題目是否有要求「Minimum Zero Padding」？

---
#DigitalImage Processing #Convolution #ComputerVision