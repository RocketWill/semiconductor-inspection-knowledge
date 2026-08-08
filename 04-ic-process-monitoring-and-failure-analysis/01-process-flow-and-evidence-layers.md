# From Process Flow to Evidence Layers

## 先找到異常位於哪一層，再討論可能是哪一道製程

> **Learning Context**
>
> Wafer maps, inspection results, and runtime history were already familiar from inspection work. The less familiar part was what sat behind an observation: which structure had been formed there, which later steps could still affect it, and which measurement might separate the possibilities.
>
> The two-day course helped connect those layers. This note keeps a first working map for placing WAT, CP, process signals, and physical evidence before making a process hypothesis.

這一篇原本只是想把 IC 製造流程重新畫一次，後來才發現真正缺的是「位置感」：看到一個異常時，它比較接近 device、contact、interconnect，還是後段測試？如果連 evidence 在哪一層都還沒放對，直接猜 process step 幾乎沒有意義。

## 1. 先把 IC 放回完整產品流程

從設計到可以交付的產品，中間大致會經過：

```text
Circuit design
    ↓
Layout and mask
    ↓
Wafer fabrication
    ↓
WAT
    ↓
CP
    ↓
Dicing and packaging
    ↓
Final test
    ↓
Failure analysis when needed
```

這條路徑先幫忙分開幾個容易混在一起的詞。Wafer fabrication 逐層形成元件與互連；WAT 讀 test structure 的參數；CP 在晶圓尚未切割時測 product die；封裝和 final test 則把問題帶到更後面的產品狀態。Failure analysis 是從異常結果往回找證據，不是取代前面的製程監控與測試。

![小黑拖著晶圓依序經過晶圓製造、WAT、CP、封裝與最終測試](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/01-manufacturing-and-test-journey.png)

> 圖 1：晶圓製造、WAT、CP、封裝與 final test 的概念流程。各階段留下的資料不同。

WAT 不等於 CP。WAT 比較接近製程與元件參數的監控，CP 則回答 product die 在指定條件下是否通過功能與電性測試。兩者可以互相提供線索，但不回答同一個問題。

## 2. 一張剖面圖裡，證據分在不同工作區域

製程不是只走一次的直線。材料會反覆經過 grow／deposit、pattern、etch／implant、clean、measure，再進入下一層。相同的操作名稱，可能在 STI、gate、contact 或 metal 上留下完全不同的結構結果；真正要追的是「這一次在形成什麼」。

為了先建立位置感，可以把剖面分成三個工作區域：

```text
Passivation and top connection
──────────────────────────────
Metal lines and vias                  BEOL
Interlayer dielectric
──────────────────────────────
Contact and local interconnect        MOL
Silicide
──────────────────────────────
Gate, source, drain, well and STI     FEOL
Silicon substrate
```

| 區域 | 代表性結構 | 先想到的問題 |
| --- | --- | --- |
| FEOL | well、STI、gate、source、drain | 隔離、摻雜、oxide 與元件電性 |
| MOL | silicide、contact、local interconnect | 界面、對準與局部串聯電阻 |
| BEOL | via、metal、interlayer dielectric | open、short、via resistance 與互連完整性 |

![小黑操作升降台，在 FEOL、MOL 與 BEOL 之間定位異常](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/02-feol-mol-beol-evidence-layers.png)

> 圖 2：FEOL、MOL 與 BEOL 的簡化剖面定位圖，未按比例繪製。

STI 是一個很適合練習這種讀法的例子。Layout 上看到 active-area spacing，不代表已經知道 trench fill、sidewall 或 CMP 狀態；問題可能藏在表面影像看不到的位置。MOS 的 `Idsat` 也一樣，不是某一道製程的直接 proxy。同一個 shift 可能同時包含 `Vt`、mobility、geometry、oxide 與 series resistance 的貢獻，詳細基礎留在既有的 MOS 與電性 characterization notes。

## 3. 同樣是 High Resistance，位置可能完全不同

元件做好後，導通問題至少要先分 contact、via 和 metal line：

| Structure | Location | Possible symptom |
| --- | --- | --- |
| Contact | device ↔ local interconnect | high-R、open |
| Via | metal ↔ metal | high-R、open |
| Metal line | same interconnect layer | open、short |

把它們全部叫成「線路不通」很方便，但對後面的 localization 幾乎沒有幫助。假設某批晶圓出現 high-resistance warning，還要先確認量到的是哪個 test structure：sheet resistance 偏高比較接近 doped layer 或 thin film；contact-chain resistance 偏高要看 contact 和相鄰 layer；metal continuity fail 則要找 BEOL metal 或 via 的位置。

Contact-chain 的總電阻也不一定等於單一 contact 的電阻，還可能混入薄層電阻、線寬與 test-key geometry。這部分可回到 [Contact Resistance and the Transfer Length Method](../03-electrical-characterization-and-process-monitoring/02-contact-resistance-and-transfer-length-method.md)；sheet resistance 的基礎則整理在 [Resistivity, Sheet Resistance, and Four-Point Probe](../03-electrical-characterization-and-process-monitoring/01-resistivity-sheet-resistance-and-four-point-probe.md)。

## 4. Evidence 到哪裡，結論就先停在哪裡

製程條件和後面的結果之間，至少隔著幾層不同資料：

```text
Process condition
    ↓
In-line signal / inspection
    ↓
Fabricated structure
    ↓
WAT distribution
    ↓
CP result
    ↓
Failure hypothesis
    ↓
Physical verification
```

可能只有 AOI 的局部異常，也可能只有 WAT edge drift 或 CP fail bin。它們都能縮小下一個檢查，但資料停在哪裡，結論就先停在哪裡。Observation、electrical result、spatial correlation 和 physical evidence 不應該被當成同一層。

![小黑補上電性與物理證據，避免從可見異常直接跳到原因](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/03-evidence-chain-no-shortcut.png)

> 圖 3：從觀察、電性與空間資料走向 failure hypothesis，再接 physical verification 的概念鏈。

## 5. A Small Project Connection

這裡和原本的 wafer-inspection 工作最有連結。軟體可以保存 coordinate、ROI、camera context、recipe、model result 和 runtime history，讓後面的 wafer-map comparison 有共同座標；但它不會自動告訴我異常是在 STI、contact 還是 metal layer。

## What I Would Check Next

- 如果 wafer-level spatial pattern 同時出現在 in-line inspection、WAT 和 CP，怎麼判斷它們是真的相關，而不是只是長得像？
- 同樣的 high-resistance symptom，要用哪一個額外量測最快把 FEOL、MOL、BEOL 的候選範圍縮小？

## References

1. Hsinchu Science Park Bureau–subsidized course, [*積體電路故障分析技術與良率提升*](https://saturn.sipa.gov.tw/edu/d013_new.jsp?pl_id=26A01&cs_id=15S359) (*IC Failure Analysis Technology and Yield Improvement*, course 15S359), delivered by the Tze-Chiang Foundation of Science & Technology, August 6–7, 2026. This note draws on the first day.
