# Contact Resistance and the Transfer Length Method

## 同樣叫接觸電阻，先別混在一起

> **Learning Context**
>
> The previous note used four-point sensing to reduce resistance from the measurement leads and probe contacts. This chapter deals with a different problem: the metal–semiconductor contact is part of the device itself, so its resistance cannot simply be removed by changing the meter connection.
>
> TLM became easier to follow once I treated it as a separation problem. The contact dimensions stay the same while the gap between contacts changes. That produces a line whose slope describes the semiconductor layer and whose intercept keeps the contribution of the two contacts.

## Short English Note

This note follows current crowding, transfer length, and the assumptions behind a linear TLM fit.

## 1. 先把兩種接觸問題分開

前一篇提到，探針碰到試片時會多帶入一些 contact resistance。四點量測把送電和量電壓分開，主要是在降低量測接點與導線造成的影響。

這一篇又出現「接觸電阻」，不過已經不是同一件事。這次的界面在金屬電極與半導體之間，而且它本來就是元件的一部分：

| 情況 | 接觸發生在哪裡 | 主要問題 |
| --- | --- | --- |
| Measurement contact | 探針與測試表面之間 | 量測路徑額外帶入的電阻 |
| Device contact | 金屬與半導體之間 | 元件本身需要承擔的接觸電阻 |

換成四條導線，可以降低第一種影響；第二種不會因為換了接線方式就消失。它要靠另外設計的測試結構，從總電阻裡慢慢拆出來。

## 2. 看起來接上了，電流不一定走得順

金屬和半導體已經碰在一起，不代表電流就能毫無阻礙地通過。表面氧化、污染、能障、界面粗糙度，以及接點下方的摻雜，都可能改變結果。除此之外，電流實際怎麼分布也很重要。

某一個實際接點造成的電阻以 $R_c$ 表示，單位是 $\Omega$。不過只比較 $R_c$ 會遇到尺寸問題：大接點和小接點不能直接放在一起看。因此還需要 specific contact resistivity：

$$
\rho_c
=R_cA
$$

在電流近似均勻通過接觸面、接點接近 ohmic，而且使用小訊號斜率的簡化條件下：

$$
R_c
\approx\frac{\rho_c}{A}
$$

$\rho_c$ 常用的單位是：

$$
\Omega\cdot\mathrm{cm^2}
$$

這裡的平方公分來自面積，和材料電阻率 $\rho$ 的 $\Omega\cdot\mathrm{cm}$ 不同。幾個電阻相關的量放在一起時，先看單位通常比先背公式有效：

| Quantity | 符號 | 常見單位 |
| --- | --- | --- |
| Resistance | $R$ | $\Omega$ |
| Resistivity | $\rho$ | $\Omega\cdot\mathrm{cm}$ |
| Sheet resistance | $R_{\mathrm{sh}}$ | $\Omega/\square$ |
| Specific contact resistivity | $\rho_c$ | $\Omega\cdot\mathrm{cm^2}$ |

本篇使用 $R_{\mathrm{sh}}$ 表示 sheet resistance，避免和二極體模型中的 series resistance $R_s$ 混淆。

## 3. 先用面積公式抓方向，但不要停在這裡

若：

$$
\rho_c=1.0\times10^{-6}\ \Omega\cdot\mathrm{cm^2}
$$

接點面積為：

$$
A=1.0\times10^{-4}\ \mathrm{cm^2}
$$

暫時假設電流分布均勻：

$$
\begin{aligned}
R_c
&=\frac{\rho_c}{A}\\
&=\frac{1.0\times10^{-6}}{1.0\times10^{-4}}\\
&=1.0\times10^{-2}\ \Omega
\end{aligned}
$$

若面積縮小為原本的十分之一，接觸電阻會增加十倍。這個方向很直觀，不過先把它當成面積變化的第一個近似就好。

真正讓前面的簡單面積公式開始不夠用的是 current crowding。電流先沿著半導體薄層水平移動，靠近接點後才轉向進入金屬。接點前緣的路徑比較短，因此整塊幾何面積不會被同樣程度地使用。

這種現象稱為 current crowding。

![小黑從半導體薄層擠進金屬接點邊緣](../assets/03-electrical-characterization-illustrations/03-current-crowding-and-transfer-length.png)

> 圖 1：作者依個人課程筆記設計並重新整理；電流由半導體薄層進入金屬時，主要集中在接點前緣，較深處的物理面積不一定被同等使用。

## 4. Transfer length 大概就是主要用到的那一段

Transfer length 以 $L_T$ 表示，可以先理解成：

> 電流從半導體薄層轉移進入金屬時，主要使用的有效接觸距離。

若接點本身很長，但 $L_T$ 很短，大部分電流仍然擠在邊緣附近。這時繼續把接點往後延長，接觸電阻也不會照著物理面積等比例下降。

在標準 TLM 模型下：

$$
L_T
=\sqrt{\frac{\rho_c}{R_{\mathrm{sh}}}}
$$

這個關係把界面與薄層放在一起：

- $\rho_c$ 較高，電流較不容易向上進入金屬，$L_T$ 會增加；
- $R_{\mathrm{sh}}$ 較高，電流較不容易沿薄層向內分布，$L_T$ 會縮短。

所以 $L_T$ 不是接點面積的另一種寫法。它同時受到接觸界面和半導體薄層片電阻影響。

## 5. TLM 為什麼要做不同間距

TLM 的做法其實很像控制變因：在同一層材料上製作幾何相同的金屬接點，只刻意改變接點之間的距離 $D$。

這裡先把幾個容易畫反的方向留下來：

| 符號 | 意義 |
| --- | --- |
| $D$ | 相鄰接點之間的間距 |
| $Z$ | 垂直於電流方向的接點寬度 |
| $L_c$ | 電流進入接點方向上的接點長度 |
| $L_T$ | 電流由薄層轉移進入金屬的特徵長度 |

圖 2 主要表達 $D$ 的改變，$Z$ 與 $L_c$ 沒有按比例畫出。真正解讀測試結構時，這三個方向仍然需要回到版圖或尺寸圖確認。

在薄層均勻、接點接近 ohmic、接點寬度一致，而且 $L_c$ 相對 $L_T$ 足夠大的標準線性 TLM 近似下，兩個接點之間量到的總電阻可以先拆成：

$$
R_{\mathrm{total}}
=R_c+R_{\mathrm{layer}}+R_c
$$

若接點寬度為 $Z$，中間薄層的電阻為：

$$
R_{\mathrm{layer}}
=R_{\mathrm{sh}}\frac{D}{Z}
$$

因此：

$$
R_{\mathrm{total}}
=\frac{R_{\mathrm{sh}}}{Z}D+2R_c
$$

接點尺寸和製程先保持不變，只改中間距離：

- 距離增加時，薄層電阻增加；
- 左右兩個接觸電阻理想上保持不變。

把不同間距的總電阻放到同一張圖後，薄層和接點的貢獻才有機會被分開。

對每一個接點間距，$R_{\mathrm{total}}$ 最好由選定線性偏壓區的 I–V 斜率取得，而不是只使用單一電壓與電流點。若 I–V 本身已經明顯彎曲，一個 $V/I$ 數值就不能代表穩定的歐姆電阻，後面的直線擬合也失去原本的前提。

![小黑改變接點間距並從直線讀取薄層與接點資訊](../assets/03-electrical-characterization-illustrations/04-tlm-spacing-and-line-fit.png)

> 圖 2：作者依個人課程筆記設計並重新整理；只改變接點間距後，直線斜率對應薄層電阻，縱軸截距保留兩個接點的影響，向左外推則可取得傳輸長度。圖中只表達間距變化，接點寬度與長度未按比例繪製。

## 6. 一條直線，分別看三個位置

若將 $R_{\mathrm{total}}$ 放在縱軸，接點距離 $D$ 放在橫軸，線性式可以和：

$$
y=mx+b
$$

對照。

### 斜率：先找片電阻

斜率為：

$$
m=\frac{R_{\mathrm{sh}}}{Z}
$$

所以：

$$
R_{\mathrm{sh}}=mZ
$$

若橫軸直接使用距離，斜率不是片電阻本身。還要乘上接點寬度 $Z$，才能得到 $R_{\mathrm{sh}}$。

### 縱軸截距：留下兩個接點

當距離外推到零：

$$
R_{\mathrm{total}}=2R_c
$$

因此縱軸截距 $b$ 對應兩個接點：

$$
R_c=\frac{b}{2}
$$

把截距直接當成單一接點電阻，會多算一倍。這個地方看圖時很容易順手讀錯。

### 橫軸截距：得到 transfer length

將直線向左外推到總電阻為零，理想 TLM 模型下：

$$
D_{\mathrm{x}}=-2L_T
$$

所以：

$$
L_T
=\frac{\left|D_{\mathrm{x}}\right|}{2}
$$

負號不是說傳輸長度小於零，只是直線往左外推後落在座標軸負方向。

## 7. 用一組課程數據重新算一次

課程示例中的接點距離和總電阻約為：

| 接點距離 $D$ | 總電阻 $R_{\mathrm{total}}$ |
| ---: | ---: |
| $10\ \mu\mathrm{m}$ | $7.0\ \Omega$ |
| $20\ \mu\mathrm{m}$ | $11.0\ \Omega$ |
| $30\ \mu\mathrm{m}$ | $15.5\ \Omega$ |
| $40\ \mu\mathrm{m}$ | $19.8\ \Omega$ |

直線擬合後，可以近似寫成：

$$
R_{\mathrm{total}}
\approx
\left(0.429\ \Omega/\mu\mathrm{m}\right)D
+2.6\ \Omega
$$

這裡 $D$ 使用 $\mu\mathrm{m}$。斜率的單位是 $\Omega/\mu\mathrm{m}$，和距離相乘後才會回到總電阻的 $\Omega$。

### 接觸電阻

縱軸截距約為：

$$
2R_c\approx2.6\ \Omega
$$

所以單一接點：

$$
R_c\approx1.3\ \Omega
$$

### 片電阻

若接點寬度為：

$$
Z=48\ \mu\mathrm{m}
$$

則：

$$
\begin{aligned}
R_{\mathrm{sh}}
&=mZ\\
&\approx
\left(0.429\ \Omega/\mu\mathrm{m}\right)
\left(48\ \mu\mathrm{m}\right)\\
&\approx20.6\ \Omega/\square
\end{aligned}
$$

### Transfer length

橫軸截距約為：

$$
D_{\mathrm{x}}
=-\frac{2.6\ \Omega}
{0.429\ \Omega/\mu\mathrm{m}}
\approx-6.1\ \mu\mathrm{m}
$$

因此：

$$
L_T
\approx\frac{6.1}{2}
\approx3.0\ \mu\mathrm{m}
$$

這個結果可以先讀成：大部分電流主要由接點邊緣約 $3\ \mu\mathrm{m}$ 的範圍進入金屬。不是說後面的接點完全沒有電流，只是貢獻會很快減少。

### Specific contact resistivity

在這組標準 TLM 近似下：

$$
\rho_c
=R_{\mathrm{sh}}L_T^2
$$

先換算：

$$
3.0\ \mu\mathrm{m}
=3.0\times10^{-4}\ \mathrm{cm}
$$

代入後：

$$
\begin{aligned}
\rho_c
&\approx
\left(20.6\ \Omega/\square\right)
\left(3.0\times10^{-4}\ \mathrm{cm}\right)^2\\
&\approx1.85\times10^{-6}\ \Omega\cdot\mathrm{cm^2}
\end{aligned}
$$

前面的圖表讀值和直線係數本來就是近似值，因此保留約兩位有效數字已經夠了。再多幾位看起來比較精確，實際上沒有增加多少資訊。

## 8. 線畫得出來，不代表截距就可信

TLM 的計算看起來很像簡單的 linear regression，因此很容易把注意力放在「線有沒有 fit 出來」。不過量測點若明顯彎曲或散布很大，強行畫一條直線仍然會有截距，只是那個截距不一定代表可靠的 $R_c$。

看到線不太漂亮時，會先回頭看：

- 接點沒有呈現近似 ohmic 的 I–V；
- 不同接點的尺寸或製程狀態不一致；
- 薄層片電阻沿測試結構改變；
- 接點間距太短，兩側電流轉移區域互相影響；
- 接點長度相對 $L_T$ 不夠長；
- 探針接觸不穩定；
- 量測電流造成自熱；
- 選擇的擬合範圍只留下看起來較直的點。

$R_{\mathrm{sh}}$ 主要來自斜率，$R_c$ 則要靠外推到 $D=0$ 的截距。距離範圍太窄、資料點太少或電阻散布較大時，截距通常比斜率更不穩定。這時只看 $R^2$ 不太夠，截距的信賴區間和 residual pattern 也要一起看。

若擬合得到負的縱軸截距，也不應直接報告一個負接觸電阻。這比較像是在提醒：儀器 offset、接點幾何、薄層均勻性或模型假設，至少有一項還沒處理好。

這一段最後留下來的重點，不只是斜率和截距公式。原始點、I–V 線性、殘差和量測條件都要先站得住腳，直線才有物理上的意義。

## 9. A Small Note on Keeping Fits Reviewable

TLM is not closely related to the optical inspection systems I built, so I would not treat it as a direct project example. But one part felt familiar: keeping a result reviewable.

In model evaluation, a final score was not enough if the dataset version, threshold, configuration, and raw predictions were missing. A fitted contact resistance has a similar limitation: the value is much less useful without the original spacing and resistance points, contact geometry, current range, fitting window, residuals, temperature, and sample identity.

The connection is simply the habit of keeping a fitted parameter attached to the data that produced it.

## 10. 先寫在圖旁邊，避免下次又讀錯

1. 目前討論的是量測接點，還是元件內部的金屬—半導體接點？
2. $\rho_c$ 的單位是否包含面積，而且沒有和 $\rho$、$R_{\mathrm{sh}}$ 或 series resistance $R_s$ 混在一起？
3. TLM 斜率是否已乘上接點寬度 $Z$？
4. 縱軸截距代表兩個接點，還是已經除以 2？
5. 橫軸截距的負號是否只被當成外推位置？
6. 擬合前是否先確認各組 I–V 接近線性？
7. 原始量測點、幾何、擬合範圍與 residual 是否仍然保留？
8. 接點長度 $L_c$ 相對 $L_T$ 是否足以使用標準 TLM 近似？

這一篇先停在接觸電阻、current crowding 和 TLM。下一篇再回到 diode I–V，整理理想因子、串聯電阻，以及 process monitor 可以支持哪些判斷。

## Questions Left Open

- 接點不是 ohmic 時，TLM 圖會先在哪一個區域偏離直線？
- 接點間距接近 transfer length 時，兩側電流分布要如何修正？
- 若殘差具有固定方向，如何區分薄膜不均勻、接點製程差異與量測問題？

## References

1. Arizona State University, [*Electrical Characterization: Diodes*](https://www.coursera.org/learn/electrical-characterization-diodes), Coursera.
