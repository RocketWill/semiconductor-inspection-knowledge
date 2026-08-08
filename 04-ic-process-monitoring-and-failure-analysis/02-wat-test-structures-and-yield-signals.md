# WAT Test Structures and Yield Signals

## 一個測試數值，要放回測試結構、分布與晶圓位置再看

> **Learning Context**
>
> Wafer maps already carried spatial information from inspection work. WAT added a question that was easier to miss: what structure produced the number? A threshold voltage, sheet resistance, or contact resistance value comes from a deliberately designed test structure, not from a complete product circuit.
>
> What became clearer was that the number only makes sense after I know the test structure, where it sits on the wafer, and what later happened at product level. A single pass point is only one part of the picture.

第一篇先把異常放回 FEOL、MOL、BEOL 與封裝的位置。接著要問的是：一個 WAT 數值到底量到了什麼？如果跳過 test structure，容易把 test-line device 當成 product device，也容易把單一測點的 Pass 當成整片晶圓都很穩定。

## 1. WAT 測的是 Test Structure，不是 Product Die

先把三種量測放在一起：

```text
Inline measurement / inspection → process result
WAT                              → test structure
CP                               → product die
```

WAT 會把複雜 IC 中的一部分抽出來量，例如 MOS device、resistor、contact chain、comb／serpentine 或 oxide monitor。這些結構可能放在 scribe line 或 monitor area，幾何、端點與量測條件都是刻意設計的。

![Product die、scribe line、test key 與切割方向的簡化位置圖](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/04-scribe-line-test-key-layout.svg)

> 圖 1：Product die 與 scribe-line test key 的概念位置；test key 可在 wafer 階段提供 probing 位置，尺寸與配置未按比例繪製。

Test structure 不是縮小版完整 IC。MOS test device 可以用固定的 `W/L` 觀察 `Vt` 或 `Idsat`；contact chain 把很多 contact 串起來，讓小電阻變得比較容易量到；comb／serpentine 則用來觀察 continuity、spacing 或 insulation。

![小黑把複雜產品電路拆成 MOS、電阻、接點與絕緣測試結構](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/05-wat-structure-decomposition.png)

> 圖 2：幾種簡化的 WAT test structure。它們把問題拆小，但沒有把所有耦合因素消除。

Test structure 的好處是把問題縮小，但它看得到的也只有被設計和取樣到的那一小塊。隨機 particle 如果只落在 product die，沒有落到 scribe-line test key，WAT 仍可能正常。

## 2. Pass／Fail 之外，還要看 Distribution

一個測點通過，只能說它在這次條件下沒有越過 spec。晶圓上的參數還要看 mean、spread、target 距離，以及是否出現空間 pattern。

假設某個薄層的 spec window 是 45–60 `Ω/□`：

| Lot | Mean `Rsh` | Observed range | 初步讀法 |
| --- | ---: | ---: | --- |
| Reference lot | 50 `Ω/□` | 48–52 `Ω/□` | 靠近 target，分布集中 |
| Current lot | 56 `Ω/□` | 49–61 `Ω/□` | 平均值上升，分布變寬，尾端越界 |

如果只看 current lot 的多數測點，可能會得到「大部分仍 Pass」的印象。但和 reference lot 放在一起，mean、spread 和 high-resistance tail 已經改變。這裡只談 spec window；control limit 和 product design margin 需要另外的統計背景。

![穩定、偏移但仍通過，以及部分超出規格的三種分布](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/06-spec-window-and-distribution-shift.svg)

> 圖 3：三個分布在相同 spec window 下的概念比較；曲線為學習示意，不代表實際製程資料。

## 3. 平均值相近，Wafer Map 仍可能完全不同

假設兩片 wafer 的平均 `Rsh` 都是 52 `Ω/□`。第一片的測點均勻散在 target 附近，第二片則是中心偏低、邊緣偏高。平均值一樣，空間結構卻不同。

常見 pattern 可以先描述成 center-to-edge gradient、wafer-edge ring、local cluster 或少數 outlier。這些名稱只是在說圖形長什麼樣，不直接指定原因。

WAT map 和 CP map 也要先對齊。兩者的空間單位、取樣密度和 orientation 可能不同，不能把兩張彩色圖放在旁邊，用肉眼覺得「很像」就結束。

![小黑對齊 WAT parameter map 與 CP fail-bin map，再標記重複的空間區域](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/07-wat-cp-map-alignment.png)

> 圖 4：WAT parameter map 與 CP fail-bin map 的概念對齊；先確認 orientation、座標與 sampling，再看是否有重複的空間區域。

比較前至少要先把 orientation、座標系統和 sampling resolution 對齊，不然兩張 map 看起來相似也可能只是視覺錯覺。對齊後若高阻區和某類 CP fail bin 重複出現在 wafer edge，可以支持進一步調查，但仍不能直接指定製程原因。

即使 WAT parameters 都在 spec 內，product die 仍可能在 CP fail，因為 product circuit 還包含 load、timing、interconnect 和多參數共同偏移。WAT 和 CP 不能互相取代。

## 4. 和我原本工作的連結

這一段和我原本的 wafer-inspection 工作最接近。Wafer-inspection systems 也需要保存 wafer orientation、coordinates、ROI、recipe version、camera context 和 measurement time，後面的 map comparison 才有共同基準。這些欄位可以讓 spatial pattern 被重新對齊，但不會自動判斷它來自 test structure、product die，還是某個後續量測條件。

## What I Would Check Next

- WAT sampling site 的數量與位置，會如何限制 wafer-map pattern 的判讀？
- WAT parameter 和 CP fail pattern 看起來相似時，要用什麼方法確認不是座標、sampling 或其他共變參數造成的假相關？

## References

1. Hsinchu Science Park Bureau–subsidized course, [*積體電路故障分析技術與良率提升*](https://saturn.sipa.gov.tw/edu/d013_new.jsp?pl_id=26A01&cs_id=15S359) (*IC Failure Analysis Technology and Yield Improvement*, course 15S359), delivered by the Tze-Chiang Foundation of Science & Technology, August 6–7, 2026. This note draws on the first day.
