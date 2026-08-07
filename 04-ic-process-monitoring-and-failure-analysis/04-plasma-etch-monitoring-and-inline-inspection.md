# Plasma Etch Monitoring and In-line Inspection

## 製程還在進行時，如何從訊號與缺陷分布判斷它是否偏離預期？

> **Learning Context**
>
> Most of my inspection experience begins after an image has already been captured. Plasma etching introduced an earlier layer of evidence: the process itself can leave a time-dependent optical signal before a finished structure is available for inspection. That signal may help identify a material transition or define an endpoint, while later in-line inspection records where visible defects appear.
>
> I wanted to separate these two views. One follows the reaction over time; the other preserves spatial evidence after a process step. Neither one, by itself, proves why the process changed or whether the product will eventually fail.

這一段課程原本看起來像是兩個主題：前半段用光譜監控 plasma etch，後半段改談 defect inspection。整理到一半才比較能把它們放在同一條線上。兩者都比 WAT 和 CP 更靠近製程，只是一個看時間訊號，另一個看空間分布。

先分開這兩種證據，後面的判斷會簡單很多。

## 1. 製程中的訊號和完成後的結果不同

前一篇已經把 [inline inspection、WAT 與 CP](./02-wat-test-structures-and-yield-signals.md) 放在不同量測層次。這裡再往前一步：plasma etch 還在進行時，腔體內的發光強度會隨氣體組成與反應產物改變；製程步驟完成後，inspection 才會留下 defect location、map 或 trend。

```text
Plasma process signal     → 反應隨時間是否改變？
In-line inspection       → 完成的表面在哪裡出現可見異常？
WAT                      → 測試結構的電性參數是否合理？
CP                       → Product die 是否通過功能與電性測試？
```

這四層可能互相呼應，不過不能互相替代。Endpoint signal 出現，不代表每個開口都已得到相同 profile；defect map 上沒有明顯異常，也不能保證後續電性一定通過。

## 2. 同一個 Recipe，局部 Etch Result 仍可能不同

一開始容易把 recipe 想成整片晶圓共用的答案：時間、氣體與功率相同，蝕刻結果應該也相同。但課堂的 micro-loading 例子提醒，局部開口大小與 pattern density 也會進入結果。

較小的開口裡，etchant 較難進入，reaction byproduct 也較難離開，因此 etch rate 可能低於較大的開口。講義另一個 layout 例子則顯示，名義尺寸相近的 poly pattern 經過製程後，實際寬度仍可能不同。這裡不把例子中的特定尺寸當成通用 design rule；它比較重要的作用，是修正「layout 畫得一樣，實體就會完全一樣」的直覺。

![局部開口與圖案密度可能改變蝕刻結果的概念圖](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/12-plasma-process-signal-chain.svg)

> 圖 1：作者依第二堂課程筆記重新繪製；相同的 process setting 進入不同局部 geometry 後，reactant transport、byproduct removal 與 etch result 可能不同。圖中結構不按比例，也不代表特定 recipe、材料堆疊或 design rule。

這個差異也替後面的 OES 留下一個限制：腔體訊號可以反映整體反應正在改變，但不一定能單獨說明某一個小開口是否已經清乾淨。

## 3. OES 量到的是 Plasma 發出的光

Optical Emission Spectrometry（OES）把腔體發出的光經 optical fiber 送入 spectrometer，再記錄不同 wavelength 的 intensity。課堂用「特定物種具有特定 emission peak」建立基本概念，因此可以同時觀察 spectrum，也可以追蹤選定訊號隨時間的變化。

```text
Plasma and surface reaction
        ↓
Excited species and reaction products
        ↓
Optical emission
        ↓
Spectrometer
        ↓
Intensity by wavelength and time
```

但 OES 不是直接量 film thickness，也不是拍下 wafer surface。它量到的是光。要把某條 intensity curve 解讀成材料轉換或 endpoint，仍要知道追蹤的是哪個物種、反應條件是否穩定，以及訊號變化是否能重複出現。

## 4. Endpoint 是一段時間判斷，不是一個神奇 Peak

課堂以 silicon 或 silicon dioxide 的蝕刻說明 End Point Detection（EPD）：當正在移除的 film 接近 clear，plasma 中的反應物或產物組成會改變，選定 emission signal 也跟著改變。控制系統便能利用這個時間變化送出 endpoint signal，停止 main etch 或切換到下一段操作。

![蝕刻訊號、film clear 與 over-etch window 的概念時間圖](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/13-endpoint-and-overetch.svg)

> 圖 2：作者依第二堂課程筆記重新繪製；上方曲線只示意被追蹤的 emission signal 在 film clear 附近改變，下方顯示 main etch、endpoint 與 over-etch window 的相對位置。訊號方向、時間與膜厚均為概念資料。

這裡曾經卡了一下：如果 endpoint 已經出現，為什麼還要 over-etch？重新對照 micro-loading 後就比較清楚。Endpoint 比較接近「整體訊號已顯示材料轉換」，但 wafer 內與局部 pattern 仍可能存在 etch-rate variation，因此製程會保留一段 over-etch margin，讓較慢的區域有機會完成。

不過 over-etch 也不是越久越安全。課堂把「何時停止 over-etch」留成一個控制問題；時間不足可能留下殘膜，時間過長則可能增加下層材料或結構受影響的風險。單看 endpoint curve，還不能替所有 geometry 找到唯一的最佳停止時間。

## 5. In-line Inspection 留下的是空間證據

OES 與 EPD 沿著 process time 追蹤訊號，in-line inspection 則把問題換成 wafer location。流程從 wafer inspection 產生 defect map 與 trend chart，接著用 microscope 或 SEM review 進行分類，再把選定位置送往後續 analysis and investigation。

![製程中檢查從缺陷分布走向針對性分析的回饋流程](../assets/04-ic-process-monitoring-and-failure-analysis-illustrations/14-inline-inspection-feedback-loop.svg)

> 圖 3：作者依第二堂課程筆記重新整理；inspection 先留下位置與分布，再由 review、classification 與 targeted analysis 逐步縮小問題。流程是概念示意，並不表示 defect class 已經等同 root cause。

這一段和既有 AOI 工作最熟悉的地方，是 coordinate、classification 與 history 都要保留下來。單張 defect image 能說明局部看到了什麼，map 和 trend 才能回答它是否集中在特定 wafer region、layer 或時間區段。後續若要和 process record、WAT 或 physical analysis 對齊，orientation、位置、recipe version 與 inspection condition 也不能丟掉。

但這種熟悉感也很容易讓判斷跑太快。模型標成 particle、scratch 或 bridge-like appearance，仍然只是 observation 或分類結果。它可以決定優先 review 哪些位置，不能只靠 label 指定 plasma chemistry 或某一道製程就是 root cause。

## 6. 兩種訊號把搜尋範圍縮小，但沒有完成診斷

整理完後，目前比較順手的判斷順序是：

1. 先確認異常來自 time signal 還是 spatial observation；
2. 若是 OES／EPD，查看追蹤物種、baseline、訊號轉折與 over-etch 設定；
3. 若是 defect map，先確認座標、layer、取樣與 classification 是否可重現；
4. 再比較兩者是否在相同 wafer、process step 與時間範圍內互相支持；
5. 最後提出需要的 CD、profile、electrical 或 physical verification。

如果 endpoint timing 漂移，同批 wafer 又出現相似的空間缺陷，兩組資料放在一起會讓 process hypothesis 變得更值得檢查。仍然不能直接寫成「plasma etch 已被證實造成缺陷」。中間還缺少局部結構、量測重現性，以及能排除 inspection artifact 或其他製程貢獻的證據。

再往下整理，就會碰到另一個問題：geometry variation 要怎麼和可接受的 electrical risk 接起來？這就要再看 design rule 如何替 lithography、etch 與 overlay 留下 process margin。

## References

1. Hsinchu Science Park Bureau–subsidized course, [*積體電路故障分析技術與良率提升*](https://saturn.sipa.gov.tw/edu/d013_new.jsp?pl_id=26A01&cs_id=15S359) (*IC Failure Analysis Technology and Yield Improvement*, course 15S359), delivered by the Tze-Chiang Foundation of Science & Technology, August 6–7, 2026. This note draws on the second day, especially the plasma etching, OES, EPD, over-etch, and in-line inspection material.
