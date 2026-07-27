# Semiconductor Electrical Behavior and Inspection Evidence

## 半導體電性與檢測證據：從能帶、摻雜與載子行為理解工業影像的邊界

> **Learning Context**
>
> My inspection work has connected cameras, defect models, runtime software, dataset management, equipment records, and production-facing workflows. These systems can detect and organize visible abnormalities.
>
> Before studying this topic, I was already familiar with terms such as doping, leakage, wafer defects, and electrical yield from project discussions. However, I could not clearly explain how carrier concentration, mobility, defect states, and interfaces were connected.
>
> I studied semiconductor conductivity to build that missing connection. The goal is not to infer electrical properties from an AOI image. It is to understand what the image can support, what remains unknown, and what should be measured next.

## English Summary

This chapter connects basic semiconductor electrical behavior with industrial inspection. Energy bands explain why carrier populations in semiconductors can be changed by temperature and doping. Conductivity depends on both carrier concentration and mobility, while defects and interfaces may introduce trapping, recombination, or leakage-related behavior.

These mechanisms also set a boundary for image interpretation. An optical category can describe contrast, geometry, position, and distribution, but it does not establish an electrical diagnosis. I use anonymized project experience in dataset design, multi-camera inspection, event-driven runtime software, and model deployment to outline a materials-aware evidence chain that links observations with inspection context, process history, engineering hypotheses, and later verification.

---

## 1. 這一章要整理的問題

前六章分別整理了材料分類、鍵結與晶體結構、缺陷、機械性質、破壞行為，以及製程歷史對材料狀態的影響。到了半導體，這些概念開始和實際檢測工作更直接地重疊：晶體缺陷、摻雜、界面、污染和溫度都可能影響電性，不過 AOI 最先取得的仍然是光學訊號。

這一章主要想釐清一個問題：

> **半導體的材料與電性知識，如何改善工業檢測資料的解讀，同時避免把光學標籤直接當成電性或材料根因？**

這個問題包含兩個層次。第一個層次是理解半導體為什麼能透過摻雜和溫度改變導電行為；第二個層次則是判斷 AOI、電性測試、製程紀錄和材料分析各自能提供什麼證據。

## 2. 半導體為什麼不同於金屬與絕緣體？

從能帶角度來看，材料能否導電和電子可使用的能態有關。以下比較刻意簡化，只保留理解後續內容需要的差異：

| 材料 | 簡化能帶狀態 | 常見導電特徵 |
| --- | --- | --- |
| 金屬 | 能帶部分填滿，或價帶與導帶重疊 | 通常已有大量可移動電子 |
| 半導體 | 價帶與導帶之間存在較小能隙 | 載子濃度可受到溫度、光照與摻雜控制 |
| 絕緣體 | 能隙較大 | 常溫下能進入導帶的電子通常很少 |

半導體的特殊之處不只是導電率介於金屬和絕緣體之間，而是它的載子濃度可以被工程化控制。製程可以在晶格中引入特定摻雜原子，也能透過氧化、沉積、退火和界面設計形成元件需要的電性行為。

不過「可以控制」不代表材料性質只由一個參數決定。摻雜濃度、實際活化程度、載子遷移率、溫度、缺陷和界面狀態都可能改變最後量到的結果。

## 3. 能帶、能隙與費米能階

![本徵與摻雜半導體的簡化能帶示意](../assets/07-semiconductor-inspection-reflection-illustrations/01-semiconductor-band-and-doping.svg)

> 圖 1：作者依個人課程筆記重新整理；圖中比較本徵、n 型與 p 型半導體的簡化能帶、摻雜能階與費米能階位置。這是一張概念示意圖，能階距離未按比例繪製。

理解半導體導電行為時，幾個基本名詞需要先分開：

- **價帶（valence band）**：在低溫基態下，主要由價電子占據的能帶。
- **導帶（conduction band）**：電子進入後，可以在外加電場下參與導電的能帶。
- **能隙（band gap, $E_g$）**：導帶底與價帶頂之間沒有允許能態的區域。
- **電子（electron）**：位於導帶中的負電載子。
- **電洞（hole）**：價帶缺少電子後形成的等效正電載子。
- **費米能階（Fermi level, $E_F$）**：用來描述電子占據能態機率的能量基準。

費米能階不是一條實際存在的電子軌道。它比較像統計判斷的參考位置：在熱平衡下，$E_F$ 的位置會影響導帶和價帶附近能態被占據的機率。對本徵半導體，它通常位於能隙中間附近；加入施體或受體後，位置會分別向導帶或價帶方向移動。

整理這一段時，最容易產生的誤解是把能帶圖看成電子在空間中的高度。圖中的縱軸代表能量，不是晶圓厚度，也不是缺陷在影像中的位置。

## 4. 本徵半導體、n 型與 p 型摻雜

### 4.1 本徵半導體

理想的本徵半導體不依靠刻意加入的摻雜原子提供載子。當部分價帶電子獲得足夠熱能跨越能隙時，導帶會增加一個電子，價帶則留下相對應的電洞。在熱平衡下：

$$n=p=n_i$$

其中 $n$ 和 $p$ 分別為電子與電洞濃度，$n_i$ 為本徵載子濃度。

在常用的非簡併近似下，本徵載子濃度可以寫成：

$$n_i=\sqrt{N_C N_V}\exp\left(-\frac{E_g}{2kT}\right)$$

$N_C$ 與 $N_V$ 是導帶和價帶的有效態密度，$k$ 是波茲曼常數，$T$ 是絕對溫度。這個式子再次出現了前面章節多次看到的指數溫度關係，不過這裡描述的是載子激發，不應和空位生成、擴散或相變速率混成同一個機制。

### 4.2 n 型半導體

在矽中加入具有較多價電子的施體原子，例如磷，可以在導帶附近形成施體能階。少量能量便能使施體電子進入導帶，因此電子成為多數載子，電洞則為少數載子。

在施體大致完成游離、且本徵激發尚未主導的條件下，可以近似寫成：

$$n\approx N_D$$

這個近似仍有條件。摻雜是否完全游離、補償摻雜、高濃度下的簡併效應和缺陷造成的載子捕捉，都可能讓實際結果偏離簡單關係。

### 4.3 p 型半導體

加入價電子較少的受體原子，例如硼，會在價帶附近形成受體能階。價帶電子可以進入受體能階，原本的位置留下電洞，因此電洞成為多數載子。

在相似的近似條件下：

$$p\approx N_A$$

n 型或 p 型並不代表材料只剩下一種載子。兩種載子仍然同時存在，只是多數與少數的比例不同。在熱平衡及非簡併條件下，它們也受到質量作用定律限制：

$$np=n_i^2$$

## 5. 載子濃度、遷移率與導電率

半導體導電率可以用下式整理：

$$\sigma=q\left(n\mu_n+p\mu_p\right)$$

其中：

- $q$：基本電荷量；
- $n$、$p$：電子與電洞濃度；
- $\mu_n$、$\mu_p$：電子與電洞遷移率。

電阻率則為：

$$\rho=\frac{1}{\sigma}$$

這個公式提供了一個很重要的檢查方式：導電率不只取決於「有多少載子」，還取決於這些載子能否移動。提高摻雜濃度通常會增加多數載子，不過摻雜原子、晶格振動和其他散射來源也可能降低遷移率。因此，不能只看到摻雜增加，就直接判斷導電率會按照相同比例持續上升。

### 簡單判斷例題

假設某 n 型半導體在特定溫度區間內，電洞導電貢獻可以忽略。若電子濃度增加為原本的兩倍，而電子遷移率因散射下降為原本的 $70\%$，則：

$$\frac{\sigma_2}{\sigma_1}
=\frac{(2n)(0.7\mu_n)}{n\mu_n}
=1.4$$

載子濃度增加兩倍，導電率只增加約 $40\%$。這個例題不是特定製程的預測，只是用來確認濃度與遷移率需要一起考慮。

## 6. 溫度、缺陷、表面與界面

### 6.1 溫度效應不是單一方向

對本徵半導體而言，溫度升高會使更多電子跨越能隙，因此載子濃度快速增加。不過溫度也會提高晶格振動，使載子受到更多聲子散射，遷移率可能隨之下降。

對摻雜半導體，可以概略分成三個區域：

1. **凍結區（freeze-out）**：溫度較低，部分摻雜原子尚未游離。
2. **外質區（extrinsic region）**：摻雜提供的載子占主導。
3. **本徵區（intrinsic region）**：溫度升高後，本徵激發產生的載子逐漸超過摻雜貢獻。

這三個區域主要用來整理不同主導機制，並沒有適用所有半導體的固定溫度界線。材料種類、摻雜濃度和量測條件不同，各區域出現的溫度範圍也會改變。

因此，「半導體溫度越高，電阻一定越低」只在特定材料與溫度區間內可能成立。真正量到的導電率取決於載子濃度增加和遷移率下降之間的競爭。

### 6.2 缺陷與界面可能改變載子行為

晶體缺陷、污染、氧化層和薄膜界面可能在能隙中引入額外能態。依缺陷類型與能階位置不同，它們可能：

- 捕捉電子或電洞；
- 增加載子復合；
- 改變少數載子壽命；
- 影響表面電位與通道遷移率；
- 可能參與漏電、崩潰或長期可靠度退化。

這些影響仍取決於缺陷位置、能階、密度、元件結構和偏壓條件，不能只看到缺陷存在便直接推論電性後果。

不過材料中的缺陷能態和 AOI 使用的 defect label 不是同一個概念。影像中的亮點、暗點、haze、ring、particle 或 scratch 可以是穩定且有用的光學分類，但不能單獨證明 trap density、recombination center 或 leakage mechanism。

![小黑帶著光學觀察停在仍待驗證的閘門前](../assets/07-semiconductor-inspection-reflection-illustrations/03-optical-label-verification-gate.png)

> 圖 2：作者依個人課程筆記設計並重新整理；光學觀察可以建立工程假設，不過要進一步形成電性或材料判斷，仍需要製程紀錄、電性量測與材料分析。

## 7. Optical, Electrical, Process, and Material Evidence

![光學、電性、製程與材料分析的證據邊界](../assets/07-semiconductor-inspection-reflection-illustrations/02-four-evidence-layers.svg)

> 圖 3：作者依個人課程筆記重新整理；四種證據各自回答不同問題，需要彼此連結，但不應互相取代。

| 證據類型 | 通常可以回答 | 通常不能單獨回答 |
| --- | --- | --- |
| Optical evidence | 位置、形貌、大小、分布、對比與重複模式 | 載子濃度、缺陷能階、漏電或復合機制 |
| Electrical evidence | 電阻、漏電、載子壽命、I–V 或 C–V 行為 | 缺陷的確切表面形貌與來源 |
| Process evidence | 批次、設備、recipe、溫度、時間與製程步驟 | 材料是否真的形成特定缺陷或電性機制 |
| Material characterization | 成分、晶相、應力、界面與微觀結構 | 不一定能單獨重建完整製程因果鏈 |

實際問題往往不是缺少所有資料，而是資料彼此沒有連接。例如模型保存了 class、box 和 confidence，設備紀錄保存了 camera 與 recipe，製程系統保存了批次和處理條件，後續電性測試又存在另一個資料庫。每一份資料單獨看都合理，不過如果無法回到同一片 wafer、同一個位置或同一段時間，就很難把它們組成可驗證的工程推論。

## 8. Label Note: A Wafer Category Is Not an Electrical Diagnosis

In an anonymized wafer-inspection project, the dataset contained wafer-level appearance categories as well as localized particles and scratches. Both had originally been represented with bounding boxes. I reviewed the annotation semantics and separated tasks according to what the labels actually described: a property of the whole image or a local object with a meaningful position.

That change improved the relationship between the annotation and the model objective. Semiconductor physics adds another boundary. None of those optical categories, however consistent, establishes carrier concentration, trap density, leakage behavior, or a recombination mechanism.

A haze-like condition may follow a process change and remain an optical observation. A particle may later correlate with yield or electrical performance, but the relationship needs evidence outside the AOI label. The model can report whether a pattern exists, where it occurs, and how it is distributed across wafers or batches. It cannot determine the electrical consequence from the image alone.

This distinction is useful because an operational label does not need to be physically complete to have value. It does need to remain honest about what was observed.

## 9. Runtime Note: A Defect Record Needs Context

Looking back at the wafer runtime, I realized that it preserved more context than a simple defect result. A passing wafer was treated as a session rather than a collection of unrelated frames. Camera identity, trigger reason, direction, sample timing, measurements, and final aggregation could be traced through that session.

At the time, I mainly designed this structure for runtime stability, debugging, and traceability. After studying semiconductor materials, I see another use for it: these fields describe how an observation was produced. The Vision Console adds related context through stream identity, ROI shape, image-processing settings, and camera parameters.

But they still do not describe what the wafer experienced before inspection. Upstream process steps, thermal exposure, material specification, electrical tests, and later characterization would need separate links. A runtime record can explain the inspection path; it cannot fill in the missing material history.

![匿名化的 wafer inspection runtime 即時操作畫面](../assets/07-semiconductor-inspection-reflection-illustrations/06-wafer-runtime-live-anonymized.png)

> 圖 4：作者開發的 wafer inspection runtime 匿名化展示畫面。系統使用 mock 影片呈現多相機狀態、ROI、trigger、session 與即時量測資訊；Logo 與本機路徑已移除。這張圖用來說明觀察如何產生，不代表畫面本身已經確認材料或電性原因。

## 10. Looking Back at the Tools I Have Built

While writing this chapter, I noticed that several systems I had built covered different parts of the same evidence chain, even though they were developed for different projects:

- a model platform for dataset management, training configuration, evaluation, visualization, export, and machine-side deployment;
- a Vision Console for multi-camera streaming, ROI processing, camera controls, presets, and captured-result review;
- an event-driven wafer runtime for trigger handling, per-camera state, inspection sessions, result aggregation, history, and report export;
- data and agent workflows for retrieving records and summarizing operational information.

These systems were not integrated into a complete materials-analysis platform. That boundary matters. The model platform manages visual evidence and model versions; the runtime records how an observation was acquired; data tools can retrieve equipment or production context. None of them automatically supplies wafer genealogy, electrical measurements, or material characterization.

The connection appeared only after I placed the projects beside the material concepts in this chapter. Together they cover useful parts of an evidence workflow, but several links are still missing.

## 11. A Practical Evidence Record

![匿名化的 wafer inspection history 與結果彙整畫面](../assets/07-semiconductor-inspection-reflection-illustrations/07-wafer-runtime-history-anonymized.png)

> 圖 5：作者開發的 wafer inspection runtime 匿名化展示畫面。History 將 session、wafer、時間、檢測結果與量測欄位保留在同一筆紀錄中；畫面資料來自 mock 影片，不包含客戶生產資料。

![材料導向檢測的 evidence chain 架構](../assets/07-semiconductor-inspection-reflection-illustrations/05-materials-aware-evidence-architecture.svg)

> 圖 6：作者依個人課程筆記與系統實作經驗重新整理；這張圖是學習後畫出的 evidence chain 草圖，不是已部署的 production architecture。Agent 可以協助查詢和整理，但不替代驗證。

我不預期每個專案一開始就具備所有欄位。不過在把 inspection result 當成工程證據以前，至少會檢查以下幾個層次：

| 層次 | 例子 | 為什麼需要 |
| --- | --- | --- |
| Observation | image、label、confidence、box／mask、校正後尺寸 | 記錄實際觀察到什麼 |
| Inspection context | camera、illumination、ROI、trigger、recipe、model version | 說明訊號如何產生 |
| Product context | wafer ID、lot、coordinate、orientation、process stage | 連接實體對象、位置和製程節點 |
| Process context | upstream step、equipment、time、temperature、material state | 支持製程與材料假設 |
| Verification | electrical test、metrology、characterization、review status | 區分關聯和受到證據支持的結論 |

未知欄位應該維持未知。如果用一個看起來肯定的 defect name 補上缺口，紀錄會顯得完整，卻同時失去真正有用的不確定資訊。

### Where Industrial AI Can Help

Industrial AI can compare defect distributions across batches, retrieve related equipment and process records, and identify repeated associations. An agent can also help engineers find similar cases or prepare a list of missing checks.

Its output should remain traceable. If the system reports an association, it should show the batches, time range, model version, and comparison conditions used. Without electrical or material verification, the conclusion should remain a correlation or hypothesis.

## 12. What I Would Record Differently Now

My original map of an inspection system was mostly a software map: camera acquisition, defect models, runtime services, dataset management, history records, and deployment tools. It was useful for implementation, but it did not describe how an engineering conclusion should be supported.

The same modules now look more like different layers of evidence. An optical pattern may be repeatable. Its association with one process step may also be strong. The electrical effect can still remain unverified.

This changes what a complete defect record means to me. It is not simply an image, a class, and a confidence score. It should preserve the observation, the conditions under which it was produced, the related product and process context, the proposed explanation, and the result of later verification (when that evidence exists).

But the system should also preserve an unresolved state. Filling every field with a confident answer would make the record look complete while removing the most important engineering information: what is still unknown.

## 13. Questions Left Open

This chapter helped me connect optical evidence with basic semiconductor electrical behavior, but several questions are still open:

- How should spatial AOI coordinates be aligned with electrical test data when their measurement resolutions are very different?
- Which measurements are most useful for separating surface contamination, interface traps, bulk defects, and process-induced stress?
- How much repeated correlation is enough before a process variable becomes a serious engineering hypothesis?
- How should unresolved or conflicting verification results be represented in a production dataset?

These are not details I can settle from the current course notes. They point toward the next subjects I need to study and, in some cases, toward questions that require device, process, or materials specialists.

## 14. Notes to Keep Beside the Evidence Record

- Optical contrast may be useful without revealing carrier concentration, lifetime or leakage.
- Doping changes carrier concentration, while conductivity still depends on mobility.
- Temperature can affect carrier concentration and mobility in competing directions.
- A semiconductor defect state and an AOI defect label are different things.
- Camera, ROI, trigger, recipe, coordinate, model and session describe how the observation was produced. They do not reconstruct the upstream material history.
- Unknown evidence should remain unknown. An Agent can retrieve and organize records, but it should not fill the missing cause with a confident answer.

This chapter is still an introductory connection rather than a device-physics treatment. PN junction derivations, transistor operation, quantum transport and advanced reliability models remain outside the current notes.

The model platform, Vision Console, wafer runtime and data-agent workflows were also separate projects. The evidence-chain diagram is a sketch made while connecting those experiences; it is not a production architecture that has already been deployed. That distinction is worth leaving in the note, especially because the diagram looks more complete than the systems were in practice.

## References

1. James F. Shackelford, [*Materials Science: 10 Things Every Engineer Should Know*](https://www.coursera.org/learn/materials-science), University of California, Davis / Coursera.
2. James F. Shackelford, *Introduction to Materials Science for Engineers*, 8th ed.
3. William D. Callister Jr. and David G. Rethwisch, *Materials Science and Engineering: An Introduction*.
4. Ben G. Streetman and Sanjay Kumar Banerjee, *Solid State Electronic Devices*.
5. Donald A. Neamen, *Semiconductor Physics and Devices*.
6. National Bureau of Standards, [*Semiconductor Measurement Technology*](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nbsspecialpublication400-8.pdf), NBS Special Publication 400-8, Section 5: Oxide Film Characterization.

## Future Reading

- S. M. Sze and Kwok K. Ng, *Physics of Semiconductor Devices*: reserved as a reference for future device-specific questions rather than a primary source for this chapter.
