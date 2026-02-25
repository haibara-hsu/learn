
# ⚙️ Robotics: Dimension 2 (Kinematics)

## 📐 1. 運動學基礎 (Kinematics Fundamentals)

> **定義**：研究運動本身而不考慮產生運動的力 (The study of motion without forces)。

### 正向與逆向運動學

- **正向運動學 (Forward Kinematics, FK)**：
    
    - **輸入**：關節角度 $(\theta_1, \theta_2, ...)$
        
    - **輸出**：末端執行器位置 $(x, y, z)$
        
    - **特性**：簡單幾何問題，具備 **唯一解 (Unique solution)**。
        
- **逆向運動學 (Inverse Kinematics, IK)**：
    
    - **輸入**：目標位置 $(x, y, z)$
        
    - **輸出**：所需關節角度 $(\theta_1, \theta_2, ...)$
        
    - **特性**：困難且複雜，通常有 **多重解 (Multiple solutions)**。需程式判定最安全、路徑最短的解。
        

---

## 🏎️ 2. 移動域與環境 (Mobility Domains)

|**類型**|**全稱**|**核心物理限制**|**動態特性**|
|---|---|---|---|
|**UGV**|Unmanned Ground Vehicle|摩擦力 (Friction)|剛性動態 (Stiff dynamics)|
|**UAV**|Unmanned Aerial Vehicle|重力 (Gravity)|快速動態 (Fast dynamics)|
|**AUV**|Autonomous Underwater Vehicle|壓力 (Pressure)|緩慢動態 (Slow dynamics)|

### 穩定性 (Stability)

- **靜態穩定 (Statically Stable)**：3 輪以上。關閉電腦仍能站立。
    
- **動態穩定 (Dynamically Stable)**：2 輪（如平衡車）。需 100% 能源與運算維持平衡，斷電即倒。
    
- **越障能力**：被動輪無法爬過高度 $h$ 大於其半徑 $r$ 的垂直台階 ($h < r$)。
    

---

## 🎡 3. 輪式與履帶系統 (Wheeled & Tracked)

### A. 導航約束 (Holonomic vs. Non-holonomic)

- **全向 (Holonomic/Omni-directional)**：
    
    - **優點**：極高靈活性 (Agility)，可橫移。
        
    - **缺點**：輪組複雜、易打滑、負重能力低。
        
- **非全向 (Non-holonomic/Car-like)**：
    
    - **優點**：結構簡單、高抓地力與高負重。
        
    - **缺點**：靈活性受限、控制複雜、迴轉半徑大。
        

### B. 特殊輪組技術

1. **Mecanum wheels (麥克納姆輪)**：
    
    - 輥子與軸線呈 45°。
        
    - 優點：無需轉向馬達，靠軟體混合速度實現全向移動。
        
    - 缺點：輥子摩擦造成 **大量能量浪費**。
        
2. **Omni wheels (全向輪)**：
    
    - 輥子與軸線呈 90°。
        
    - 類型：Kiwi Drive (三角形佈局)、Killough Drive (正方形佈局)。
        
3. **Swerve drive (舵輪/轉向驅動)**：
    
    - 像可轉動 360° 的推車輪，具備機械轉向。
        
    - 優點：**最高效率**（無向量抵消），100% 能量轉換。
        
    - 缺點：極其昂貴，每輪需 2 個馬達（驅動+轉向）。
        

### C. 履帶系統 (Tracked)

- **能耗**：極高，30-40% 能量消耗在彎折履帶本身。
    
- **優勢**：接觸面積大 $\rightarrow$ **低壓強 (Low Pressure)** $\rightarrow$ 適合軟地、不易沉陷。
    
- **缺點**：靠「滑移轉向 (Skid steering)」，會破壞地面且極度耗電。
    

---

## 🦵 4. 足式與複合系統 (Legged & Hybrid)

- **足式機器人 (Legged)**：
    
    - **優點**：離散接觸點，可跨越障礙物。
        
    - **缺點**：能量效率低（站立即耗能）。
        
    - **常見形式**：四足 (Quadruped)、雙足 (Biped)。
        
- **輪足複合機器人 (Wheeled-legged)**：
    
    - 結合輪式的高效（平地）與足式的靈活性（越障）。
        
    - **代表作**：Hyundai MobED (Mobile Eccentric Droid) - 偏心輪設計，兼顧穩定與適應性。
        

---

## 🦾 5. 操作與末端執行器 (Manipulation & End-effectors)

### A. 自由度 (DoF) 與冗餘

- **低自由度 (SCARA/Delta)**：犧牲通用性換取極高速度與剛性。
    
- **冗餘機器人 (Redundant robot)**：自由度多於任務需求（如 7 軸手肘）。
    
    - 作用：繞過障礙物、避免奇異點 (Singularities)、優化力量姿勢。
        

### B. 抓取方式 (Holdings)

- **摩擦閉合 (Friction closure)**：靠壓力夾住（如夾硬幣）。風險高，壓力一失即掉落。
    
- **幾何閉合 (Form closure)**：靠幾何形狀鎖定（如勾住杯把）。安全性極高。
    

### C. 末端執行器類型

- **硬式夾爪 (Hard Grippers)**：精準但脆弱，需完美數據。
    
- **真空吸盤 (Suction Grippers)**：物流英雄，不看幾何只看表面積，但會留下痕跡。
    
- **軟性夾爪 (Soft Grippers)**：利用「機械智能」彎曲，適合處理食品或易碎品。
    

---

### 💡 評估重點

- **Fixed (固定式)**：確定性空間 (Deterministic)。
    
- **Mobile (移動式)**：機率性空間 (Probabilistic)，需面對 **里程計漂移 (Odometry Drift)**。
