目標：在微米到奈米尺度的先進製造中，一套可追溯且具公信力的品質控制系統得以量化量測不確定度，得以確保零件互換性並支持摩爾定律演進。

- 為達成成本效應與環境永續是當代先進製造的目標，因此必須發展具有可追溯性的品質控管。
	Traceability is the property of the result of a measurement whereby it can be related to stated references, usually national or international standards, through a documented unbroken chain of comparisons all having stated uncertainties.
- 在統計層面上，另一個核心原理是**沒有任何量測是完美的**；因此，量測學不再追求絕對的「真值」，而是追求量化**不確定度（Uncertainty）**。
	Even if an ideal instrument and measurement set-up were available, all measure-ments are ultimately subject to Heisenberg’s Uncertainty Principle, a consequence of quantum mechanics that puts a natural limit on measurement accuracy.
	errors can appear as random or systematic dependent on how they are treated.
- 因為所有觀測都會受到環境干擾（如振動、電磁場）或設備解析度限制，所以我們必須使用高斯分佈（Gaussian Distribution來描述測量值的機率分佈。there are different methods for either correcting errors or accounting for them in uncertainty analyses  Accuracy, precision, resolution, error and uncertainty
	![[Pasted image 20260225153938.png]]
	A “precise” measurement means that the measurement data are close to each other. 離散程度
	An “accurate” measurement means that the measurement data are close to the “true” value of the measurement target, which is a known reference.接近程度
	Type I and Type II errors
	the lower specification limit (LSL) and the upper specification limit (USL)
	Random errors
	Systemic errors
- 在實際操作中，我們利用**高斯分佈（Gaussian Distribution）** **不確定度評估框架（如 GUM 或蒙地卡羅法）**，我們能將測量風險量化為可管理的統計數據。	
	A Monte Carlo method A Monte Carlo method for uncertainty evaluation is based on the following consideration. The estimate y of Y is conventionally obtained, as in the previous section, by evaluating the model for the estimates xi of Xi. However, since each Xi is described by a probability distribution, a value as legitimate as xi can be obtained by drawing a value at random from the distribution.
	In the GUM uncertainty framework, the information about an input quantity Xi takes the form of an estimate xi, a standard uncertainty u(xi) associated with the estimate, and the degrees of freedom νiattached to the standard uncertainty.

實務應用：半導體製程中的極限挑戰
- 在半導體製造領域，量測學的應用被推向了極限，這是因為摩爾定律要求電晶體特徵尺寸持續縮小，目前已進入奈米級的**量子機制領域**。 這裡的核心原理演變為對**製程變異的極致監控**，特別是在自動化量測系統（如 CD-SEM）中。
	When the minimal feature of IC devices (normally referring to a device gate width) was larger than 1 mm, a linewidth (or a spacewidth), called critical dimension (CD), was measured with optical-microscope-based measurement instruments (Optical CD tools). In late 1980s, when the IC device gate width shrank to less than 1 mm, optical CD tools were close to their resolution limits (directly related to the light wavelength for illumination) and had a hard time resolving features edges. CD measurement systems based on scanning electron microscopy (here denoted as CD-SEMs) (CD-SEM) were introduced into IC manufacturing. Over the next 5–6 years, as it became more and more mature, CD-SEMs had completely replaced optical CD tools in IC fabs. In 1990s, the CD-SEM became fully automated with robust pattern recognition technology for wafer alignment and measurement location navigation. From then on, the CD-SEM has experienced tremendous progress in image quality, advanced measurement algorithms, higher throughput, and ease of use. It has been a critical part of IC process development and control in IC manufacturing.
- 因為在高速、自動化的晶圓廠中，任何量測誤差都可能導致嚴重的**決策風險**，例如將合格品誤判為廢品的「α 風險（假陰性）」或漏檢壞片的「β 風險（假陽性）」。
	Due to measurement uncertainties and the statistical nature of measure-ments, there is always the chance that the “actual” value of a monitored parameter of a product is within the specification but the measurement result says otherwise; even though such a chance is small, it is called a “false negative” or “alpha error” in statistics.
	A Type I error will result in false rejecting a good part due to measurement uncertainty, whereas a Type II error will result in failure to identify a bad part due to measurement uncertainty. Both error types should be avoided by minimizing measurement uncertainties.

- 為了支持這些高精度的要求，產業開發了如機台比對（Tool-to-Tool Matching）等支持性技術，確保整座晶片廠內數十台設備的量測數據能相互匹配，不因設備差異而造成誤導。
	
- 雖然傳統的光學顯微鏡已因解析度限制而被電子束或 X 射線技術取代，但量測學的本質依然是為了在製程中建立「可預測性」，以解決 GAA 或 FinFET 等複雜三維結構帶來的幾何檢測難題。