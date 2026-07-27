# p–n Junction and Diode I–V

## 從載子擴散、內建電場到真實量測曲線

> **Learning Context**
>
> Before studying this topic, I understood a diode mainly as a component that conducts in one direction. That description was useful in programming and system integration (and often enough for the task in front of me), but it skipped the part I wanted to understand: what changes inside the semiconductor before the current begins to rise.
>
> Drawing the p–n junction made the sequence clearer. Carrier diffusion leaves fixed charge near the interface, the fixed charge creates an internal field, and the field eventually limits further diffusion. The I–V curve is therefore not just a component specification. It is a measured response shaped by the junction, temperature, recombination, geometry, contacts, and series resistance.

## English Summary

This note connects p-type and n-type carrier distributions with depletion-region formation, built-in voltage, forward and reverse bias, and the diode I–V equation. It also looks at why a real CMOS diode departs from the ideal one-dimensional model. The main practical point is simple: the applied voltage is not always the junction voltage. At higher current, contact, bulk, spreading, and interconnect resistance can consume a noticeable part of it. The project reflection uses my inspection-runtime experience only as a data-context comparison; the system itself did not perform electrical characterization.

## 1. 接合以前，兩邊都接近電中性

上一則筆記已經整理過摻雜與載子濃度。這裡只保留形成接面需要的部分：

- N 型材料中，電子是多數載子，電洞是少數載子；
- P 型材料中，電洞是多數載子，電子是少數載子；
- 兩邊在接合以前都可以接近電中性，不是 N 型整塊帶負電、P 型整塊帶正電。

這一點容易被 P 與 N 的名稱誤導。摻雜改變的是自由載子的比例，材料內仍然同時存在帶電載子與固定的離化雜質。

在常用的完全游離與非簡併近似下：

$$
n_n\approx N_D
$$

$$
p_p\approx N_A
$$

少數載子則可由熱平衡關係估算：

$$
np=n_i^2
$$

這些近似不是本篇的重點，不過後面的內建電壓會再次用到 $N_D$、$N_A$ 與 $n_i$。

## 2. 接觸後，載子先因濃度差而擴散

P 型與 N 型半導體剛接觸時，接面兩側的載子濃度差很大：

- 電子傾向由 N 側擴散到 P 側；
- 電洞傾向由 P 側擴散到 N 側。

靠近接面的電子與電洞會復合。可移動載子離開後，原本被它們平衡的離化雜質留在晶格中：

- N 側留下帶正電的固定施體離子；
- P 側留下帶負電的固定受體離子。

這些固定電荷不會像自由載子一樣跨過接面，卻會建立電場。接面附近缺少可移動多數載子的區域，就是 depletion region。

![小黑在 p–n 接面中央拉起內建電場閘門](../assets/02-semiconductor-characterization-illustrations/03-pn-junction-depletion-region.png)

> 圖 1：作者依個人課程筆記設計並重新整理；載子擴散後留下固定離子，形成空乏區與由 N 側指向 P 側的內建電場。圖中閘門表示內建電場逐漸抵抗進一步擴散。

## 3. 平衡不是載子停止移動

固定電荷形成的內建電場，會推動載子產生與原本擴散方向相反的 drift。在熱平衡下，電子與電洞各自的 drift 與 diffusion contribution 互相抵消，合成後沒有淨電流。先用簡化的方式寫成：

$$
\text{diffusion current}+\text{drift current}=0
$$

這不代表電子與電洞完全靜止。這個差異對我很重要，因為「量到零」不一定表示系統內沒有任何活動，也可能是幾個相反作用剛好抵消。

熱平衡時，整個接面的 Fermi level 必須保持水平。P 側與 N 側原本不同的能帶位置會重新排列，並在接面附近發生彎曲。能帶圖中的高度代表電子能量，不是晶圓真的彎曲。

## 4. 內建電壓由哪些條件決定

在常用的突變接面、熱平衡與非簡併近似下，內建電壓可以寫成：

$$
V_{bi}
=
\frac{k_BT}{q}
\ln\left(
\frac{N_AN_D}{n_i^2}
\right)
$$

從這個式子可以先讀出幾個方向：

- $N_A$ 或 $N_D$ 增加時，$V_{bi}$ 通常增加；
- 溫度不只出現在 $k_BT/q$，也會影響 $n_i$；
- 換一種半導體材料時，$n_i$ 與能帶相關條件也會不同。

所以內建電壓不是只由「P 型和 N 型接在一起」決定。摻雜、溫度與材料都在裡面。

$V_{bi}$ 是接面內部的靜電位差，不是把普通電壓表接在未加偏壓的二極體兩端，就能直接讀到的 terminal voltage。內部模型參數與儀器讀值之間，仍然隔著接觸與完整的量測條件。

費米位勢則描述 Fermi level 相對本徵能階的位置。例如 N 型材料可寫成：

$$
\phi_{Fn}
=
\frac{k_BT}{q}
\ln\left(\frac{N_D}{n_i}\right)
$$

P 型費米位勢在不同教材中可能使用不同正負號慣例。實際畫能帶圖以前，我會先確認符號是表示帶方向的位勢，還是只表示能量差的大小。

## 5. 外加偏壓改變的是原本的能障

### Forward bias

對 p–n 接面施加正向偏壓時，外加電場會抵消一部分內建電場。結果是：

- 有效能障降低；
- 空乏區變窄；
- 多數載子更容易跨越接面；
- 正向電流快速增加。

這比單純記成「正向偏壓會導通」多了一個中間步驟：不是電壓碰到某個數字後突然把門打開，而是偏壓逐漸降低原本的勢壘。

### Reverse bias

反向偏壓會加強原有的電場，使空乏區變寬，多數載子更難跨越接面。在理想擴散模型中，反向電流主要和少數載子有關；真實元件還可能包含空乏區生成電流、表面漏電與邊緣效應。

這一篇先停在 breakdown 以前。反向電壓夠高之後出現的其他機制，需要另外處理，不能繼續把反向電流視為固定不變。

## 6. 常用的二極體 I–V 模型在描述什麼

在最簡單、由理想擴散電流主導的模型中，$n=1$。實際整理量測曲線時，常加入 ideality factor $n$，用來表示接面復合與其他非理想效應造成的偏離：

$$
I
=
I_0
\left[
\exp\left(
\frac{qV_D}{nk_BT}
\right)-1
\right]
$$

也可以先定義 thermal voltage：

$$
V_T=\frac{k_BT}{q}
$$

再寫成：

$$
I
=
I_0
\left[
\exp\left(
\frac{V_D}{nV_T}
\right)-1
\right]
$$

這裡需要分清楚幾個量：

| 符號 | 筆記中的理解 |
| --- | --- |
| $I_0$ | 在簡化模型中對應反向飽和電流，也設定正向指數區的電流尺度 |
| $V_D$ | 真正落在 p–n 接面上的電壓 |
| $n$ | ideality factor，用來表示簡單模型沒有完整描述的復合與非理想效應 |
| $V_T$ | thermal voltage，會隨絕對溫度改變 |

課程把 $n$ 稱為一種 “fudge factor”。我覺得這個說法很好記，但不能因此把它當成沒有物理意義的任意數字。它反映的是量測曲線和最簡單模型之間的差距，而擬合區間選得不合適，也會讓結果失去解釋價值。

$I_0$ 也不是脫離條件後仍然固定的數字。材料、摻雜、接面面積和溫度改變時，它也會跟著改變。當 $n$ 與 $I_0$ 由量測曲線擬合而來，我還需要記錄選用的電流範圍；數值擬合得很好，不代表同一個機制主導整條曲線。

## 7. 為什麼半對數圖比較容易看

在正向偏壓足夠大、而且 $-1$ 項可以忽略的範圍：

$$
I\approx I_0
\exp\left(\frac{V_D}{nV_T}\right)
$$

取自然對數後：

$$
\ln I
=
\ln I_0+\frac{V_D}{nV_T}
$$

因此在半對數圖上，中等正向電流區通常接近直線。這讓斜率、$n$ 和 $I_0$ 比在線性座標中更容易觀察。

不過「看起來像直線」還不等於整條曲線都能用同一組參數解釋。低電流區可能受到漏電或復合影響；電流變大後，串聯電阻又會開始主導。

這裡可以做一個不太複雜的斜率檢查。若電流增加十倍：

$$
\Delta V_D=nV_T\ln 10
$$

室溫 $300\ \mathrm{K}$ 時，$V_T$ 約為 $25.9\ \mathrm{mV}$，因此：

$$
\Delta V_D\approx59.6n\ \mathrm{mV/decade}
$$

例如 $n=1.5$，電流每增加一個 decade，大約需要增加：

$$
\Delta V_D\approx89\ \mathrm{mV}
$$

這個數值不是用來判斷所有二極體都應該長得一樣，而是拿來檢查半對數曲線的斜率是否落在合理方向。若不同區段算出的結果差很多，就不應勉強用同一組 $n$ 解釋整條曲線。

## 8. 真實二極體多了一個串聯電阻

課程中的 CMOS diode 不是一塊理想的一維結構。它需要離子佈植區、金屬接點與實際的三維電流路徑。電流可能經過接面底部和側壁，也可能在接點附近發生 current crowding。

這些額外影響通常先合併成等效串聯電阻 $R_s$：

$$
V=V_D+IR_s
$$

所以真正的接面電壓是：

$$
V_D=V-IR_s
$$

代回二極體方程式：

$$
I
=
I_0
\left[
\exp\left(
\frac{V-IR_s}{nV_T}
\right)-1
\right]
$$

![小黑在真實二極體模型中分配串聯電阻與接面電壓](../assets/02-semiconductor-characterization-illustrations/04-diode-series-resistance.png)

> 圖 2：作者依個人課程筆記設計並重新整理；外加電壓會分配在串聯電阻與 p–n 接面上。半對數 I–V 曲線在中等電流區接近理想直線，高電流時則因 $IR_s$ 壓降而逐漸偏離。

這個式子中的 $I$ 同時出現在等號兩側，通常不能像最簡單的指數式一樣直接代入一次就得到答案。更重要的是，高正向電流時 $IR_s$ 變大，外加電壓不會全部落在接面上。

這裡先把 $R_s$ 當成簡化的線性參數。實際接觸、current crowding、自熱與材料電阻仍可能隨電流或溫度改變，不一定能由一個固定常數完整描述。

## 9. A Small Project Connection: Why Measurement Context Matters

While reading the diode I–V section, I kept thinking about the wafer runtime I had built.

In that system, a defect result was not stored as one isolated number. It belonged to a camera, a wafer session, a trigger event, and one or more timed samples. I kept those fields mainly for debugging and traceability because the same measurement could mean something different when it came from another camera, ROI, or point in the runtime.

The connection to diode characterization is limited, but useful to me. A current value is also incomplete without the device, applied voltage, temperature, sweep direction, and measurement setup. And when series resistance becomes important, even the voltage recorded at the terminals is not identical to the voltage across the junction. That difference matters.

The Vision Console and wafer runtime did not perform electrical characterization. This is only a reminder from my previous software work: a curve is easier to trust when the conditions that produced it remain attached to the data.

## 10. 寫在公式旁邊的檢查

- 現在畫的是電子移動方向，還是 conventional current direction？
- 接面處於熱平衡、正向偏壓，還是反向偏壓？
- $V$ 是儀器施加的電壓，還是真正的接面電壓 $V_D$？
- 使用的 $n$ 與 $I_0$ 是從哪一段曲線擬合出來的？
- 目前看到的是 linear plot 還是 semi-log plot？
- 高電流偏離理想直線時，$IR_s$ 是否已經不能忽略？
- 不同曲線的溫度、元件面積與量測條件是否一致？
- $V_{bi}$ 是模型中的內部勢壘，還是儀器可以直接量到的 terminal voltage？
- 現在只有 electrical anomaly，還是已有材料、製程或結構證據？

這些檢查不能取代正式的參數提取，不過可以避免把整條曲線都塞進同一個簡單模型，也能提醒自己不要把一個異常數值直接寫成失效原因。

## Current Scope

This note stays with equilibrium junction formation, basic forward and reverse bias, the ideal diode equation, and a simple series-resistance correction. It does not yet cover detailed recombination models, breakdown extraction, capacitance–voltage behavior, contact-resistance measurement, or full parameter-fitting procedures.

## Sources

1. Arizona State University, [*Fundamentals of Semiconductor Characterization*](https://www.coursera.org/learn/fundamentals-of-semiconductor-characterization), Coursera.

## Project Context

The project reflection is based on my implementation experience with a multi-camera Vision Console and an event-driven wafer-inspection runtime. It is included to explain traceability and measurement context, not to claim electrical-characterization experience.
