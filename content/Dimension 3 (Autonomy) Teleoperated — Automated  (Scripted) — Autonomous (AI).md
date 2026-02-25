
# 🤖 Robotics: Dimension 3 (Autonomy)

## 🧠 1. 自主性階層 (Levels of Autonomy)

> **定義**：機器人在沒有人類持續控制的情況下，獨立運作、做出決策並執行任務的能力。

### A. 遙控 (Teleoperated)

- **特點**：人類在迴路中 (Human-in-the-loop)，實時控制每一個動作。
    
- **應用**：達文西手術機器人、拆彈機器人、深海探索。
    
- **挑戰**：延遲 (Latency) 是最大的敵人。
    

### B. 自動化 (Automated / Scripted)

- **特點**：基於腳本與預設路徑。
    
- **邏輯**：`If X, then Y`。
    
- **環境**：高度受控且靜態的環境（如汽車組裝線）。
    
- **缺點**：缺乏靈活性，環境稍有變動即失效。
    

### C. 自主化 (Autonomous / AI)

- **特點**：具備感知、規劃與決策能力。
    
- **邏輯**：基於目標 (Goal-oriented)，而非路徑。
    
- **權衡**：**Intelligence vs. Speed**。
    
    - 規劃 (Planning) 需要運算時間，會降低反應速度 (Reaction)。
        

---

## 🛡️ 2. 安全規範與標準 (Safety Standards)

### 關鍵標準

- **ISO 10218**：工業機器人安全要求。
    
- **ISO/TS 15066**：協作機器人 (Cobots) 運作規範，定義了人機共存的技術細節。
    

### 協作機器人的四種安全模式 (Four Modes of Collaboration)

1. **安全級停機 (Safety Monitored Stop, SMS)**：
    
    - 當人類進入協作區域時，機器人完全停止。
        
    - 機器人仍保持上電狀態，但無任何運動。
        
2. **手動引導 (Hand Guiding, HG)**：
    
    - 機器人只有在操作員手動控制（如握住把手）時才會移動。
        
    - 常見於示教 (Teaching) 或重物搬運輔助。
        
3. **速度與距離監控 (Speed & Separation Monitoring, SSM)**：
    
    - 機器人會根據與人的距離自動調整速度。
        
    - **距離愈近，速度愈慢**；進入危險區則停止。
        
4. **功率與力量限制 (Power & Force Limiting, PFL)**：
    
    - 核心觀念：機器人可以接觸人類，但其力量與壓力被限制在受傷閾值以下。
        
    - 機器人通常具有圓潤的外型與碰撞感測器。
        

---

## 🏗️ 3. 工業標準補充 (Specific ISOs)

- **ISO 9283**：性能衡量標準（精度與重複精度）。
    
- **ISO 10218 / 15066**：安全性標準。
    

> [!TIP] 價值模型與風險
> 
> 在自主性高的系統中：
> 
> $Value = Benefits - (Maintenance + Risk\ Penalties)$
> 
> 當自主決策導致意外時，Risk Penalties 會大幅增加，這也是為何工業界對完全自主 (Full AI) 仍持謹慎態度的原因。
