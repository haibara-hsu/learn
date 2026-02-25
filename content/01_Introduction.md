Robot Def:
Type
1. Spherical or polar
2. Cylindrical
3. Cartesian or gantry
4. Articulated:have three or more rotary joints
	1. 4-axis
	2. 3-axis
	3. 6-axis 如 YAMAHA、KUKA（已被中國收購）等品牌。
	4. 7-axis 具冗餘關節，逆向運動學有無窮多解。
	- **6軸關節功能：**
		- **S軸：** 基座水平旋轉。
		- **L軸：** 機身前後移動。
		- **U軸：** 手臂上下移動。
		- **R軸：** 手臂旋轉。
		- **B軸：** 末端上下擺動。
		- **T軸：** 末端旋轉。
5. Wrist design 方便逆向運動學計算
	1. spherical wrist
	2. non-spherical wrist
	-   The last three joint axes are often designed to  intersect at a common point called the wrist center.  
	- This arrangement leads to complete decoupling of  the position from the orientation problem. The arm  delivers the wrist center anywhere in its primary  workspace, while the wrist controls the orientation  of the end-effector.
- 開環：正向運動學簡單 逆向運動學難
- 閉環：相反
1. Parallel:has a closed loop structure
2. SCARA: two parallel rotary joints to provide compliance in a selected plane
		serial
		parallel
3. wearable
4. legged
5. 
