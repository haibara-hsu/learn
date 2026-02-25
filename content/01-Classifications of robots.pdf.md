# Summary

這份總結架構將機器人學拆解為「目的、身體、大腦」三個核心維度，定義了機器人系統的設計邊界與核心權衡 (Trade-offs)。
## 🎯 Dimension 1: Function (The "Why")

**核心邏輯：用途決定設計。**

- **工業機器人 (Industrial)**：
    
    - **核心目標**：**Maximize Performance**。
        
    - 追求極致的重複精度與循環時間 (Cycle time)。
        
- **物流與探索機器人 (Logistics / Exploration)**：
    
    - **核心目標**：**Maximize Availability**。
        
    - 強調在非結構化環境中的生存與持續運作能力。
        
- **服務與醫療機器人 (Service / Medical)**：
    
    - **核心目標**：**Minimize Risk**。
        
    - 安全性高於一切，確保在與人互動時零傷害。
        

---

## 🦾 Dimension 2: Kinematics (The "Body")

**核心邏輯：形態決定運動。**

### A. 移動能力 (Locomotion)

- **效率 vs. 靈活性 (Efficiency vs. Agility)**：
    
    - **輪式 (Wheels)**：高效率，但在崎嶇地形無力。
        
    - **足式 (Legs)**：極高靈活性（跨越障礙），但站立即耗能。
        
- **底座類型**：
    
    - **固定式 (Fixed)**：定義明確的工作空間 (Workspace)。
        
    - **移動式 (Mobile)**：無邊界的配置空間 (Configuration space)。
        

### B. 操作能力 (Manipulation)

- **自由度對接**：必須將機器人的 **DoF (Degrees of Freedom)** 與現實空間的 **6 DoF** 進行匹配。
    
- **冗餘 (Redundancy)**：超過 6 軸的設計可提供繞過障礙與避免奇異點的能力。
    

---

## 🧠 Dimension 3: Autonomy (The "Brain")

**核心邏輯：感知決定決策。**

### A. 控制架構

- **智能 vs. 速度 (Intelligence vs. Speed)**：
    
    - **審慎式 (Deliberative/Planning)**：高智能，但反應慢（適合複雜路徑規劃）。
        
    - **反應式 (Reactive)**：極速反應，但缺乏長遠規劃（適合避障）。
        

### B. 人機協作與安全 (Safety Standards)

- **法規基石**：依循 **ISO 10218** 與 **ISO/TS 15066**。
    
- **共存技術**：
    
    - 從「完全隔離」演進到「動態監測 (SSM)」與「力量限制 (PFL)」，實現真正的 **Shared Workspace**。
        

---

## 📊 綜合對比表 (Systematic Overview)

|**維度**|**關鍵字**|**核心權衡 (Trade-off)**|
|---|---|---|
|**D1: Function**|目的 (Purpose)|效能 (Performance) vs. 風險 (Risk)|
|**D2: Kinematics**|物理 (Physics)|效率 (Efficiency) vs. 靈活 (Agility)|
|**D3: Autonomy**|智能 (Intelligence)|規劃 (Planning) vs. 反應 (Reaction)|

---

### 🔗 關聯筆記

- [[Dimension 1 (Function) Industrial — Service — Medical]]

- [[Dimension 2 (Kinematics) Fixed — Wheeled — Legged —  Aerial ]]

- [[Dimension 3 (Autonomy) Teleoperated — Automated  (Scripted) — Autonomous (AI)]]


![[Pasted image 20260225112748.png]]


## kinematics

![[Pasted image 20260225113210.png]]

![[Pasted image 20260225113658.png]]

![[Pasted image 20260225114140.png]]
![[Pasted image 20260225114612.png]]


![[Pasted image 20260225114838.png]]

## autonomy
iso 9283 16066
Trade-off between intelligence (planning) and speed (reaction).
Autonomy refers to a robot's ability to operate independently, making  
decisions and performing tasks without continuous human control
  
ISO 10218 (Industrial Robots) and ISO/TS 15066 (Collaborative  
Operation) regulate industrial robot safety.
![[Pasted image 20260225115639.png]]
Safety Monitored Stop (SMS):
Hand Guiding (HG)
Speed & Separation Monitoring (SSM):
Power & Force Limiting (PFL):

