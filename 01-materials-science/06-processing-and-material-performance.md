# Processing, Phase Transformations, and Material Performance

## 製程、相變與材料性能：時間—溫度路徑如何留下可觀察的結果

> **Learning Context**
>
> In inspection work, I usually see a material only after several upstream steps have changed its surface, geometry, interfaces, or internal state. What I can trace most directly is the inspection configuration. The upstream material history is often less visible.
>
> Phase diagrams and transformation kinetics helped me separate two questions: what states are available, and which path the material actually followed. A repeated AOI pattern may justify checking composition, batch, or thermal history. It does not identify a phase or microstructure on its own.

## 1. Processing History and Material State

材料名稱和材料狀態需要分開看。即使成分相同，只要經歷的加熱、持溫、冷卻或加工方式不同，最後形成的相、晶粒、析出物和殘留應力都可能不同。材料性質不是掛在材料名稱旁邊的一組固定數字。

![相同成分經不同熱歷史形成不同微觀組織](../assets/06-processing-and-material-performance-illustrations/01-thermal-history-machine.png)

> 圖 1：相同成分經歷不同 time–temperature paths 後，可能形成不同 microstructures；結構為概念示意。

這條關係可以先簡化成：

```mermaid
flowchart LR
    A["成分與初始狀態"] --> B["成形、沉積、加熱、持溫與冷卻"]
    B --> C["相組成、晶粒、析出物、缺陷與殘留應力"]
    C --> D["機械、熱學、電學與光學性質"]
    D --> E["元件性能與檢測訊號"]
```

這張圖不是單向且不可逆的固定流程。製程設備、環境和量測方法也可能改變最後觀察到的訊號；檢測結果則可以回頭協助比較批次和製程條件，但不能直接取代相鑑定或微觀組織分析。

## 2. 相、組織與材料狀態並不是同一件事

閱讀相圖以前，需要先把幾個常被混用的詞分開：

| 名詞 | 這一章中的意思 | 例子 |
| --- | --- | --- |
| 成分（composition） | 材料中各元素或組成分的比例 | $0.76\ \mathrm{wt\%C}$ 的共析鋼 |
| 相（phase） | 具有相對均勻成分、結構和性質的區域 | 奧氏體、鐵素體、滲碳體 |
| 相分率（phase fraction） | 各相在材料中所占的比例 | $W_\alpha$、$W_\beta$ |
| 微觀組織（microstructure） | 各相、晶粒與缺陷的尺寸、形狀、分布和排列 | 粗波來鐵、細波來鐵、貝氏體 |
| 材料狀態（material state） | 成分、相、組織、殘留應力和製程歷史的綜合結果 | 退火、淬火或回火後的鋼 |

其中最容易混淆的是「相」和「微觀組織」。一開始看到波來鐵、貝氏體和麻田散鐵並列時，很容易把它們都當成相的名稱；不過波來鐵（pearlite，也常稱珠光體）其實是鐵素體與滲碳體形成的層狀混合組織。即使兩塊材料含有相同的兩個相，只要比例、尺寸和分布不同，機械性質仍可能出現明顯差異。

## 3. 相圖能回答什麼？

相圖將溫度、成分和穩定相的關係整理成一張地圖。對固定壓力下的二元合金，相圖通常以溫度為縱軸、成分為橫軸。

![簡化二元共晶相圖與槓桿定則](../assets/06-processing-and-material-performance-illustrations/02-binary-eutectic-and-lever-rule.svg)

> 圖 2：簡化 binary eutectic phase diagram 與 lever-rule 幾何關係；相界與成分位置只用於概念說明。

### 3.1 基本讀圖語言

- **液相線（liquidus）**：線以上為完全液態；冷卻穿過此線時，第一批固相開始形成。
- **固相線（solidus）**：線以下為完全固態；冷卻穿過此線時，最後一部分液體完成凝固。
- **溶解度線（solvus）**：分隔單一固溶體和兩個固相共存區。
- **單相區**：指定溫度與成分下只存在一個平衡相。
- **兩相區**：兩個相同時存在，例如 $L+\alpha$ 或 $\alpha+\beta$。
- **等溫連線（tie line）**：在兩相區畫出的水平線，用來讀取兩個相各自的成分。

實際讀圖時，我會依序確認：

1. 在橫軸找到材料總成分 $C_0$。
2. 在縱軸找到溫度 $T$。
3. 判斷交點位於單相區或兩相區。
4. 若位於兩相區，畫出等溫連線。
5. 由連線兩端讀取各相成分。
6. 若需要相比例，再使用槓桿定則。

相圖可以回答「在接近平衡的條件下，哪些相較穩定」。它通常不能單獨回答相變需要多久、晶粒多大、各相如何排列，也不能保證快速冷卻後仍然得到平衡組織。

## 4. 簡單例題：使用槓桿定則估算相比例

假設某二元合金位於 $\alpha+\beta$ 兩相區，等溫連線讀到：

$$
C_\alpha=20\ \mathrm{wt\%B},
\qquad
C_0=40\ \mathrm{wt\%B},
\qquad
C_\beta=80\ \mathrm{wt\%B}
$$

則 $\alpha$ 相分率為：

$$
W_\alpha
=
\frac{C_\beta-C_0}{C_\beta-C_\alpha}
=
\frac{80-40}{80-20}
=
\frac{2}{3}
$$

$\beta$ 相分率為：

$$
W_\beta
=
\frac{C_0-C_\alpha}{C_\beta-C_\alpha}
=
\frac{40-20}{80-20}
=
\frac{1}{3}
$$

檢查結果：

$$
W_\alpha+W_\beta=1
$$

這個例題最需要避免的錯誤，是把距離放在相同一側。$\alpha$ 相的比例要使用靠近 $\beta$ 端的線段，$\beta$ 相則使用靠近 $\alpha$ 端的線段。除了檢查兩者相加是否為 $1$，也可以先看總成分比較靠近哪一端，確認比例的大小關係是否合理。

這裡的橫軸使用重量百分比，因此 lever rule 得到的是重量分率；實際數值精度仍受到相圖讀值與平衡假設限制。如果相圖以原子百分比表示，分率的基準也會跟著改變；若需要體積分率，還要考慮各相密度並進一步換算。

算到這裡只有 phase fraction。組織形貌、晶粒尺寸、轉變時間與最終性能，都還沒有從這條 tie line 裡出現。

## 5. 共晶與共析：起始相不同

共晶和共析的名稱相近，但起始狀態不同：

| 反應 | 一般形式 | 起始相 | 生成結果 |
| --- | --- | --- | --- |
| 共晶（eutectic） | $L\rightarrow\alpha+\beta$ | 一個液相 | 兩個固相 |
| 共析（eutectoid） | $\gamma\rightarrow\alpha+\beta$ | 一個固相 | 兩個固相 |

鉛—錫焊料是常見的二元共晶相圖例子。以歷史上常用的鉛—錫系統而言，共晶反應約發生在 $183^\circ\mathrm C$ 與 $61.9\ \mathrm{wt\%Sn}$：

$$
L\rightarrow\alpha+\beta
$$

對偏離共晶成分的合金，冷卻時通常會先形成初生相，再由剩餘液體形成共晶組織。液相與固相共存的溫度區間會影響材料的流動、凝固和接頭形成。不過實際電子製造還會受到焊料系統、氧化、潤濕、加熱曲線和界面反應影響，不能只用一張二元平衡相圖判斷接頭品質。

鋼中的共析反應則完全發生在固態。以亞穩定鐵—滲碳體系統的近似共析成分為例：

$$
\gamma\rightarrow\alpha+Fe_3C
$$

其中：

- $\gamma$：奧氏體，FCC 結構；
- $\alpha$：鐵素體，BCC 結構；
- $Fe_3C$：滲碳體。

共析成分與溫度常近似寫為 $0.76\ \mathrm{wt\%C}$ 和 $727^\circ\mathrm C$。實際數值會依採用的相圖版本和合金元素而略有差異，因此這裡主要用來建立讀圖概念。

## 6. 為什麼還需要時間？

平衡相圖主要回答穩定狀態，但實際熱處理還包含加熱速度、持溫時間和冷卻路徑。當材料降到相變溫度以下時，會同時出現兩個方向相反的影響：

1. **熱力學驅動力增加**：過冷程度增加後，原相與新相之間的自由能差通常變大。
2. **原子擴散變慢**：溫度降低後，原子進行長距離移動的能力下降。

可以用前一章的 Arrhenius 關係理解第二點：

$$
D=D_0\exp\left(-\frac{Q_d}{RT}\right)
$$

接近平衡轉變溫度時，擴散速度較快，但形成新相的驅動力較小；溫度很低時，驅動力雖然增加，擴散卻可能慢到無法在有限時間內完成。兩者競爭，使擴散型相變常在某個中間溫度最快。

這也是 TTT 圖出現 C 形轉變曲線和「鼻尖」的原因。擴散快不代表相變一定快，驅動力大也不代表原子能及時完成重新分布。

## 7. TTT diagram：把等溫保持時間加入判斷

TTT（Time–Temperature–Transformation）圖描述材料先快速降至指定溫度，再在該溫度等溫保持時，相變何時開始、何時完成，以及可能形成什麼組織。

![共析鋼的簡化 TTT diagram](../assets/06-processing-and-material-performance-illustrations/03-eutectoid-steel-ttt.svg)

> 圖 3：簡化 eutectoid-steel TTT diagram，比較 pearlite、bainite 與 martensite 的轉變路徑；不能用來讀取特定鋼材的工業處理參數。

### 7.1 波來鐵（Pearlite）

共析奧氏體（eutectoid austenite）在較高溫度進行擴散型轉變時，碳需要從形成鐵素體（ferrite）的區域移向滲碳體（cementite），最後形成鐵素體與滲碳體交替排列的波來鐵（pearlite）。

- 較高轉變溫度：擴散距離較長，通常形成較粗的層片。
- 較低轉變溫度：成核位置增加、擴散距離縮短，通常形成較細的層片。

細波來鐵通常比粗波來鐵具有較高的強度和硬度，但具體性質仍受到成分、層片間距和先前奧氏體狀態影響。

### 7.2 貝氏體（Bainite）

在波來鐵轉變溫度以下、麻田散鐵開始溫度以上進行等溫轉變，可以形成貝氏體（bainite）。它同樣包含鐵素體與碳化物（carbides），不過形態不是規則的波來鐵層片。

貝氏體常被描述為具有較好的強度與韌性組合，但上貝氏體、下貝氏體和不同合金中的碳化物分布並不相同，因此不適合只用單一性質標籤概括。

### 7.3 麻田散鐵（Martensite）

如果冷卻速度足夠快，使奧氏體（austenite）避開擴散型轉變曲線並降至麻田散鐵開始溫度（martensite-start temperature）$M_s$ 以下，便可能形成麻田散鐵（martensite）：

$$
\gamma\ (\mathrm{FCC})
\rightarrow
\text{martensite}\ (\mathrm{BCT\text{-}like\ in\ carbon\ steels})
$$

更精確地說，主要是鐵晶格產生協同剪切式轉變；碳原子來不及長距離擴散，被困在新的晶格間隙中，使晶格產生明顯扭曲。這種結構會強烈阻礙差排移動，因此未回火麻田散鐵通常具有高硬度和高強度，但延性、韌性和殘留應力需要特別留意。

在含碳鋼中，麻田散鐵通常以過飽和的 BCT 結構描述；碳含量較低時，四方畸變可能不明顯。在一般碳鋼的熱處理脈絡下，martensitic transformation 通常近似 diffusionless，並常呈現 approximately athermal behavior。降至 $M_s$ 以下後，轉變量主要受到溫度下降程度、成分和原始奧氏體狀態控制，不是靠延長等溫保持時間完成。

$M_s$ 不是所有鋼都相同的固定溫度。它會受到碳含量、合金元素和奧氏體狀態影響；冷卻至室溫後，也可能保留部分未轉變的奧氏體（retained austenite）。

## 8. 三條熱處理路徑的簡單比較

假設同一批共析鋼先加熱至奧氏體區，再採用不同路徑：

| 路徑 | 路徑類型 | 可能組織 | 判讀重點 |
| --- | --- | --- | --- |
| 爐冷或緩慢連續冷卻 | 連續冷卻，較適合用 CCT 理解 | 以粗波來鐵為主 | 接近平衡，但仍受到實際冷卻速率影響 |
| 快速降至較高轉變溫度後等溫保持 | TTT 等溫路徑 | 粗或細波來鐵 | 溫度影響成核、擴散距離與層片間距 |
| 快速降至較低轉變溫度後等溫保持 | TTT 等溫路徑 | 貝氏體 | 需要讀取轉變開始與完成時間 |
| 淬火至 $M_s$ 以下 | 近似無擴散轉變 | 麻田散鐵與可能的殘留奧氏體 | 組織比例與降至的溫度、成分和初始狀態有關 |

這個比較說明，即使材料最後都回到室溫，微觀組織也不一定相同。只記錄最終溫度，會遺漏真正控制結果的時間—溫度路徑。

### TTT 與 CCT 不能直接互換

TTT 圖假設材料快速到達指定溫度後等溫保持；一般工業熱處理則經常持續冷卻，因此 CCT（Continuous Cooling Transformation）圖通常更接近實際冷卻過程。

TTT 圖仍然很有價值，因為它能把相變的時間尺度、轉變溫度與產物清楚分開。不過實際使用時，需要確認圖表對應的合金成分、先前奧氏體化條件、晶粒尺寸與量測方法，不能把一張共析鋼示意圖直接套用到其他鋼材。

鋼的例子把這項差異變得很具體。經過可比較的奧氏體化條件後，相同成分仍可能因後續 time–temperature path 不同，形成粗波來鐵、細波來鐵、貝氏體、麻田散鐵或混合組織。

## 9. Two Recipes Note: Manufacturing History and Inspection Settings

During a six-month on-site wafer-inspection assignment, the records available to me mainly described acquisition, inspection configuration, and result history. Trigger timing, wafer motion, camera streams, ROI and template settings were useful when a pattern appeared only under one configuration or stayed fixed in a particular coordinate system.

Phase transformations added a distinction I had not made clearly enough at the time. An inspection recipe describes how the equipment acquires and evaluates a signal. A manufacturing process recipe describes what the material experienced before it reached the inspection station. The names sound similar, but they answer different questions.

Those records were enough to investigate acquisition and coordinate-related behavior, but they did not reconstruct the wafer’s upstream thermal or material history. If an anomaly changes after an AOI threshold, illumination, or ROI update, the first explanation may belong to the measurement system. If it follows a process step, batch, thermal exposure, or spatial position on the wafer, an upstream material or process hypothesis becomes more reasonable.

But the image still does not identify a phase or microstructure. In that assignment, I did not have diffraction, cross-sectional analysis, or complete thermal-history evidence. A material transformation could not be inferred from the image.

This changes the information I would request during an investigation. I would keep the inspection configuration and manufacturing history as separate records, then compare both with the observed pattern. Otherwise, a stable model output may hide whether the repeated signal came from the material, the process, or the way the image was acquired.

## 10. Process Records and Inspection Evidence

![製程紀錄與 AOI 證據之間仍需材料驗證](../assets/06-processing-and-material-performance-illustrations/04-process-aoi-evidence-gap.png)

> 圖 4：製程紀錄與 AOI evidence 可以建立重複模式，但 phase、microstructure 與 material mechanism 仍需要材料分析或受控實驗驗證。

My platform work connects dataset management, training configurations, model evaluation, export, and machine-side deployment. In a separate wafer-inspection project, bright-field and dark-field results were combined before defect classification and measurement. Those systems preserved useful model and inspection context. They did not reconstruct the material’s upstream process history.

Inspection records explain how a signal was acquired. Process records describe what the material experienced upstream. Keeping the two records separate makes it possible to compare a repeated pattern with both measurement conditions and the recorded process path. Useful context may include the material or lot, process step and recipe version, thermal path, batch relationship, inspection configuration, and later verification result.

AI can compare these fields with defect distributions, identify drift, or show which recorded process variables repeatedly appear with a signal. That is useful for prioritizing an investigation. But correlation is not phase identification, and a model feature is not a transformation mechanism.

The gap is specific. Model versions and equipment settings explain how a result was produced. Upstream process steps, thermal exposure, batch genealogy, and later characterization help explain what may have happened to the material. Those fields were not fully available in the projects described here, so a verified explanation remained outside the image and software records.

## Current Scope

這篇先停在二元相圖、共晶與共析反應、lever rule，以及用共析鋼說明的 TTT、CCT 與 transformation kinetics。

完整 Fe–Fe₃C 相圖、析出強化、燒結、薄膜相形成與半導體熱製程都還沒有展開。鋼的例子用來理解成分與 time–temperature history 如何形成不同材料狀態，不能直接套到 silicon wafer 或 thin film。

這裡的工程案例描述 inspection acquisition、configuration 與 software records，不代表掌握 upstream manufacturing recipe。AOI pattern 可以和 process history 放在一起比較，但 phase 或 microstructure 仍需要適合的獨立證據。

## Learning Source

- James F. Shackelford, [*Materials Science: 10 Things Every Engineer Should Know*](https://www.coursera.org/learn/materials-science), University of California, Davis / Coursera.

## Additional References

- James F. Shackelford, *Introduction to Materials Science for Engineers*, 8th ed.
- William D. Callister Jr. and David G. Rethwisch, *Materials Science and Engineering: An Introduction*.
- University of Cambridge DoITPoMS, [*The Lever Rule*](https://eng.libretexts.org/Bookshelves/Materials_Science/TLP_Library_II/12%3A_Phase_Diagrams_and_Solidification/12.7%3A_The_Lever_Rule).
- National Bureau of Standards, [*Heat Treatment and Properties of Iron and Steel*](https://nvlpubs.nist.gov/nistpubs/Legacy/MONO/nbsmonograph88.pdf), NBS Monograph 88.
