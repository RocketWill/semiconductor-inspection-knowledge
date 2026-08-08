# Diode Parameter Extraction and Measurement Limits

## 先把曲線分段，再決定讀哪個參數

> **Learning Context**
>
> After learning the basic p–n junction model, I still tried to read a diode I–V curve as one result: normal or abnormal. What took longer to sort out was where each parameter came from. The exponential region can support estimates of saturation current and ideality factor, while the high-current region brings series resistance and self-heating into view.
>
> The fitting window is therefore part of the result. A clean straight line is useful, but only if the original I–V data, temperature, differentiation method, and measurement limits still support it.

## 1. 從 I–V 開始

空乏區、內建電場，以及順向與逆向偏壓下的基本行為，已經放在 [P–N Junction and Diode I–V](../02-semiconductor-characterization-fundamentals/02-pn-junction-and-diode-iv.md)。這一篇不再重畫接面，而是從拿到 I–V curve 之後開始：哪一段曲線可以拿來讀哪個參數？

理想二極體方程式為：

```math
I
=
I_0
\left[
\exp\left(\frac{qV}{nkT}\right)-1
\right]
```

$I_0$ 是反向飽和電流， $n$ 是 ideality factor， $T$ 則是絕對溫度。公式本身不難認，麻煩的是實際曲線不會從頭到尾都照著同一組近似走。若沒有先選區間，最後雖然能 fit 出參數，卻不一定說得清楚它們代表哪一段行為。

## 2. 同一條 I–V，要分區看

順向 I–V 可以先粗略看成三段：

- 低電流區的訊號比較弱，漏電、儀器解析度和接觸狀態都可能混進來；
- 中間指數區在半對數圖上比較接近直線， $I_0$ 和 $n$ 主要從這裡估；
- 高電流區開始看得見 series resistance，電流再往上時還要留意 self-heating。

![二極體 I–V 曲線的低、中與高電流區](../assets/03-electrical-characterization-illustrations/05-diode-iv-regions.png)

> 圖 1：低電流區先留意弱訊號與非理想效應，中間指數區用來估計 $I_0$ 與 $n$，高電流區則逐漸受到 $R_s$ 與自熱影響。區間邊界為概念示意，不代表固定偏壓。

這三段沒有固定分界。先切開只是避免把一條方程式硬套到整條曲線；真正使用哪一段，還是要回頭看元件、溫度、儀器範圍和原始資料。

## 3. Exponential Region：Saturation Current 和 Ideality Factor

當順向電壓相對熱電壓已經夠大，指數項遠大於 1，可以先寫成：

```math
I
\approx
I_0
\exp\left(\frac{qV}{nkT}\right)
```

取自然對數後：

```math
\ln I
\approx
\ln I_0
+
\frac{q}{nkT}V
```

換成 $\ln I$ 對 $V$ 後，中間那一段應該接近直線。往 $V=0$ 外推的截距可用來估計 $I_0$；若圖上讀到的量級約為 $10^{-10}\ \mathrm{A}$，保留這個量級通常比多寫幾位小數有意義。

這裡曾經卡了一下：外推到 $V=0$，不代表二極體在零偏壓下真的持續流過同樣大小的淨電流。它只是由選定直線區估出來的模型參數。Fitting window 一換，截距也可能跟著移動。

同一條直線的斜率為：

```math
\frac{d\ln I}{dV}
=
\frac{q}{nkT}
```

因此：

```math
n
=
\frac{q}{kT}
\left(
\frac{d\ln I}{dV}
\right)^{-1}
```

在室溫附近， $kT/q\approx25.8\ \mathrm{mV}$。 $n$ 接近 1 時，選定區間通常較接近 diffusion-dominated behavior；接近 2 時，depletion-region recombination 可能較明顯。但這只提供判斷方向，不是單一機制的證明。

剛接觸 $n$ 時，很容易把它看成另一個「越接近 1 越好」的分數。其實它比較像某一段曲線呈現出的行為。若 $n$ 明顯小於 1 或大於 2，先回頭檢查 fitting window、 $R_s$、漏電、溫度和量測設定，比直接替它指定原因穩妥。

## 4. High-Current Region：Series Resistance

實際二極體不只有接面。接觸、半導體區域與金屬導線都會帶入 series resistance。把 $R_s$ 放進模型後：

```math
I
=
I_0
\left[
\exp\left(
\frac{q\left(V-IR_s\right)}{nkT}
\right)-1
\right]
```

外加電壓可以先拆成：

```math
V=V_D+IR_s
```

電流還小時， $IR_s$ 不明顯，外加電壓大多落在二極體接面上。電流拉高後，series resistance 分走的電壓增加，半對數曲線也就慢慢離開中段直線。

這裡的符號要順手分開： $R_s$ 是 diode series resistance，前兩篇的 $R_{\mathrm{sh}}$ 是 sheet resistance。長得很像，但不是同一個量。

## 5. Conductance Transformation

只靠肉眼看高電流區彎了多少，很難穩定估計 $R_s$。先定義 differential conductance：

```math
G_D=\frac{dI}{dV}
```

在順向指數項遠大於 1 的近似下，可以整理成：

```math
\frac{I}{G_D}
=
\frac{nkT}{q}
+
IR_s
```

把 $I$ 放在橫軸、 $I/G_D$ 放在縱軸後，斜率對應 $R_s$，縱軸截距則是 $nkT/q$。

![二極體 I–V 資料的 conductance transformation](../assets/03-electrical-characterization-illustrations/06-conductance-transformation.png)

> 圖 2：由原始 I–V 計算 $G_D=dI/dV$，再將 $I/G_D$ 對 $I$ 作圖；斜率與截距可分別估計 $R_s$ 與 $n$。微分會放大量測雜訊，因此轉換後的直線不能脫離原始資料解讀。

假設擬合斜率約為 $0.01\ \mathrm{V/mA}$：

```math
R_s
=
0.01\ \mathrm{V/mA}
=
10\ \Omega
```

若截距約為 $0.0295\ \mathrm{V}$，室溫下：

```math
n
\approx
\frac{0.0295}{0.0258}
\approx1.14
```

原始數值是從圖上近似讀取，最後寫成約 $1.1$ 至 $1.2$ 反而比較誠實。算到很多小數位，不會讓圖上的讀值突然變得更準。

## 6. 直線變好看了，雜訊不會跟著消失

第一次看到 conductance transformation，很容易先注意到「曲線終於變成直線」。但 $G_D=dI/dV$ 需要對量測資料做微分，局部雜訊也會一起被放大。

如果 fit 看起來怪，會先回頭看幾件事：原始 I–V 是否平順、電壓步距與掃描方向是否合理、微分或 smoothing 方法有沒有改變局部斜率，以及擬合區間是否已經碰到 self-heating 或儀器 compliance。Residual pattern 也要留著，只看 $R^2$ 很容易漏掉固定方向的偏差。

高電流有助於把 $R_s$ 顯示出來，不代表電流越高越好。接面一旦開始升溫，原本固定 $T$ 的假設也會鬆動。能用的區間通常落在訊號已經明顯、但自熱還沒太嚴重的中間位置。

## 7. A Bridge to Process Monitoring

一個 polysilicon monitor 的 resistance 若比 target 低約 40%，不能直接翻譯成「doping 增加 40%」。因為：

```math
R
=
\rho\frac{L}{Wt}
```

量到的 $R$ 同時包含平面幾何 $L/W$、薄膜厚度 $t$ 和材料電阻率 $\rho$。原本例子裡， $L/W$ 下降、 $t$ 增加、 $\rho$ 降低，三項剛好都把 resistance 往下推；其中最大的 contribution 與 $\rho$ 的變化一致。

![Polysilicon monitor resistance shift 的可能 contributions](../assets/03-electrical-characterization-illustrations/07-process-monitor-resistance-drift.png)

> 圖 3：幾何、薄膜厚度與材料電阻率都可能使 monitor resistance 下降；多個 contribution 同方向疊加時，單一電阻值仍不能指出唯一製程原因。

這個小例子留在這裡，只是提醒 parameter shift 裡可能混著哪些 contribution。Monitor value 可以顯示「有東西變了」，但它本身不能指出是哪一個 process variable 造成變化。後續如何把 electrical abnormality 分成可驗證的 process hypotheses，接到 [Electrical Anomalies and Process Hypotheses](../04-ic-process-monitoring-and-failure-analysis/03-electrical-anomalies-and-process-hypotheses.md)。

## What I Would Keep with the Fit

- 使用的 fitting window，以及為什麼選這一段；
- 原始 I–V、溫度、掃描方向與量測步距；
- differentiation 或 smoothing 方法；
- residual，以及是否已出現 self-heating 或 compliance limitation。

選了哪一段曲線，本來就是結果的一部分，不只是前處理細節。

## References

- Arizona State University, [*Electrical Characterization: Diodes*](https://www.coursera.org/learn/electrical-characterization-diodes), Coursera.
