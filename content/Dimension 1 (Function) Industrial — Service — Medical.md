

# 🤖 Robotics: Dimension 1 (Function)

## 🏗️ 1. 工業機器人 (Industrial)

**核心目標：Maximize Performance**

**核心範式：** "Do the same thing exactly the same way, 1 million times."

### A. 性能關鍵指標

|**指標**|**定義**|**決定因素**|
|---|---|---|
|**重複精度 (Repeatability)**|先天能力|剛性 (Stiffness)、編碼器 (Encoders)|
|**精度 (Accuracy)**|後天校準|軟體校準 (Software calibration)、運動學模型 (Kinematic models)|

> [!INFO] ISO 9283
> 
> 衡量與報告工業機器人性能（精度、重複精度、路徑運動）的國際標準。

### B. 重複精度比較 (Repeatability)

- **STÄUBLI TS2-40:** $\pm 0.01$ mm
    
- **FANUC CRX-10iA:** $\pm 0.04$ mm
    
- **TECHMAN ROBOT:** $\pm 0.05$ mm
    
- **KUKA LBR iiwa7:** $\pm 0.10$ mm
    

### C. 提升機械剛性的方法

1. **剛性結構 (Rigid structures)：** 使用鑄鐵或鋁。
    
2. **無背隙齒輪 (Anti-backlash gears)：** 諧波減速機 (Harmonic drives)、擺線減速機 (Cycloidal)。
    
3. **精密軸承 (Precision bearings)：** 預壓軸承消除位移。
    

---

## 📦 2. 物流與移動機器人 (Logistics & AMR)

**核心目標：Maximize Availability**

### A. AGV vs. AMR 深度對比

|**特性**|**AGV (有軌)**|**AMR (無軌)**|
|---|---|---|
|**路徑規劃**|固定引導 (磁鐵、雷射)|靈活導航系統 (SLAM)|
|**障礙物處理**|停止並等待|繞過或重新規劃|
|**靈活性**|低，難以更改路線|高，易於適應環境|
|**設置時間**|長 (需實體安裝)|短 (軟體配置)|

### B. 室內 vs. 室外 AMR

- **室內：** LiDAR SLAM、QR Code、Wi-Fi、平滑地面。
- **室外：** GNSS (GPS)+RTK、IMU、視覺導航、4G/5G、IP65+ 防護、地形適應。
- 室內 AMR 側重於在受控環境下利用精準感測器進行定位，而室外 AMR 則需具備強大的環境適應力、全天候硬體防護及依賴衛星定位的導航能力。

**關鍵技術術語**

	• LiDAR: 光學雷達 (Light Detection and Ranging) 。
	
	• RTK: 即時動態定位技術 (Real-Time Kinematic positioning)。
	
	• IMU: 慣性測量單元 (Inertial measurement unit) 。
    

---

## 🩺 3. 醫療與輔助機器人 (Medical & Assistive)

**核心目標：Minimize Risk**

### A. 達文西手術系統 (da Vinci Surgical System)

- **架構：** 主從控制 (Master and Slave)。
    
- **關鍵挑戰：** 延遲 (Latency)、視覺回饋 (Visual feedback)。
    

### B. 輔助機器人 (Assistive Robots)

- **特點：** 增強人類而非取代 (Augment, not replace)。
    
- **模式：** 人機協作 / 共享控制 (Human-in-the-loop)。
    
- **核心需求：** 安全、舒適、直覺互動。
    
- **類型：** 復健、外骨骼 (Exoskeleton)、義肢、助升設備。
    

---

## 🌾 4. 進階領域應用 (Specialized Domains)

### 🌿 農業機器人 (Agriculture)

**核心目標：Maximize Adaptability**

- **環境挑戰：** 髒污、多變、動態 (Hostile environment)。
    
- **關鍵技術：** * **軟性夾爪 (Soft grippers)**：處理易碎作物。
    
    - **視覺伺服 (Visual Servoing)**：在風中即時追蹤並採摘。
        

### 🚀 探索機器人 (Exploration)

**核心目標：Maximize Availability (Reliability over Performance)**

- **場景：** 太空 (Mars)、深海。
    
- **控制模式：** 監督式控制 (Supervisory control)。
    
    - 原因：高延遲 (Latency)，無法即時搖控 (Joystick impossible)。
        
    - 方式：人類設定目標 (Goal)，機器人自主規劃路徑。
        

---

## 📈 總結：機器人的價值評估

$$Value = Benefits - Lifecycle\ Costs - Risk\ Penalties$$

- **效益來源：** 速度、一致性、安全性。
    
- **價值失效點：** 意外狀況、高維護成本、用戶接受度低。
    
