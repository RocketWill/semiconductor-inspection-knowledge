# Contact Resistance and the Transfer Length Method

## 同樣叫接觸電阻，先別混在一起

> **Learning Context**
>
> The previous note used four-point sensing to reduce resistance from the measurement leads and probe contacts. This chapter deals with a different problem: the metal–semiconductor contact is part of the device itself, so its resistance cannot simply be removed by changing the meter connection.
>
> What confused me at first was the intercept. I kept reading it as one contact resistance until I realized that the measured path contains two contacts. After that, changing the gap while keeping the contact dimensions fixed made more sense: the slope follows the semiconductor layer, while the intercept keeps both contacts.

## 1. Measurement Contact 和 Device Contact

前一篇提到，探針碰到試片時會多帶入一些 contact resistance。四點量測把送電和量電壓分開，主要是在降低量測接點與導線的影響。

這一篇又遇到「接觸電阻」，不過問題已經換了位置：這次的界面在金屬電極與半導體之間，而且本來就是元件的一部分。

| 情況 | 接觸發生在哪裡 | 主要問題 |
| --- | --- | --- |
| Measurement contact | 探針與測試表面之間 | 量測路徑額外帶入的電阻 |
| Device contact | 金屬與半導體之間 | 元件本身需要承擔的接觸電阻 |

換成四條導線，可以降低第一種影響；第二種不會因為換了接線方式就消失。它要靠另外設計的測試結構，從總電阻裡慢慢拆出來。

## 2. 接觸面積不是全部：Current Crowding

某一個實際接點造成的電阻以 $R_c$ 表示，單位是 $\Omega$。但只比較 $R_c$ 會遇到尺寸問題：大接點和小接點不能直接放在一起看，因此還需要 specific contact resistivity $\rho_c$：

$$
\rho_c=R_cA
$$

$\rho_c$ 的常用單位是 $\Omega\cdot\mathrm{cm^2}$。這裡的平方公分來自接觸面積，和材料電阻率 $\rho$ 的 $\Omega\cdot\mathrm{cm}$ 不一樣。幾個符號排在一起時，先看單位通常比硬背名字快一點。

若接點接近 ohmic、使用小訊號斜率，而且先假設電流均勻穿過整個接觸面，可以近似寫成：

$$
R_c\approx\frac{\rho_c}{A}
$$

照這個式子看，面積變大，$R_c$ 應該下降。方向沒有錯，但算到這裡還不能停。電流會先沿半導體薄層水平移動，靠近接點後才轉向進入金屬。接點前緣的路徑比較短，於是電流容易擠在那一帶，整塊物理面積並不會被同樣程度地使用。

![金屬—半導體接點中的 current crowding 與 transfer length](../assets/03-electrical-characterization-illustrations/03-current-crowding-and-transfer-length.png)

> 圖 1：電流由半導體薄層轉入金屬時，較集中在接點前緣；實際有效區域和完整接觸面積並不相同。概念示意，不按比例。

這就是 current crowding。原本的面積公式適合先抓方向，真正要描述電流用了接點的哪一段，還要再往 transfer length 走。

## 3. Transfer Length 描述主要用到的接觸區域

Transfer length 以 $L_T$ 表示，可以先把它想成：電流從半導體薄層轉移進入金屬時，主要使用的接觸距離。

在標準 TLM 模型下：

$$
L_T=\sqrt{\frac{\rho_c}{R_{\mathrm{sh}}}}
$$

這個式子把界面和薄層放在一起。$\rho_c$ 較高時，電流比較不容易向上進入金屬，$L_T$ 會增加；$R_{\mathrm{sh}}$ 較高時，電流也不容易沿薄層往接點深處分布，$L_T$ 反而縮短。

所以 $L_T$ 不是接點面積換一種寫法。接點就算做得很長，若 $L_T$ 很短，大部分電流仍然集中在前緣。繼續把接點往後拉長，$R_c$ 也不會照著面積等比例下降。

## 4. TLM：用不同間距分開 Layer 和 Contact

TLM 的做法其實很像控制變因：在同一層材料上製作幾何相同的金屬接點，只改變相鄰接點之間的距離 $D$。接點寬度 $Z$、接點長度 $L_c$ 和製程條件先盡量維持一致。

在薄層接近均勻、接點接近 ohmic，而且 $L_c$ 相對 $L_T$ 足夠大的標準線性近似下，兩個接點之間量到的總電阻可以拆成：

$$
R_{\mathrm{total}}
=R_c+R_{\mathrm{layer}}+R_c
$$

中間薄層的電阻為：

$$
R_{\mathrm{layer}}
=R_{\mathrm{sh}}\frac{D}{Z}
$$

因此：

$$
R_{\mathrm{total}}
=\frac{R_{\mathrm{sh}}}{Z}D+2R_c
$$

接點尺寸不變，只把 $D$ 拉長，理想上增加的是中間的 layer resistance。把不同間距的結果畫在一起後，原本混在總電阻裡的 layer 和 contact contribution 才有機會被分開。

![TLM 接點間距與線性擬合的參數讀取方式](../assets/03-electrical-characterization-illustrations/04-tlm-spacing-and-line-fit.png)

> 圖 2：依序改變接點間距 $D$，再從 $R_{\mathrm{total}}$ 對 $D$ 的直線讀取薄層與接點資訊。圖中只強調間距變化；$Z$、$L_c$ 與其他結構尺寸未按比例繪製。

這條線有三個位置要看，但不用把它們拆成三套故事。

斜率為：

$$
m=\frac{R_{\mathrm{sh}}}{Z},\qquad R_{\mathrm{sh}}=mZ
$$

所以斜率還不是 sheet resistance，本身要再乘上接點寬度 $Z$。

縱軸截距 $b$ 保留的是兩個接點：

$$
b=2R_c,\qquad R_c=\frac{b}{2}
$$

直線往左外推到橫軸時：

$$
D_x=-2L_T,\qquad L_T=\frac{|D_x|}{2}
$$

負號只是外推位置落在原點左側，不是負的 transfer length。這幾個讀值裡，最容易順手看錯的反而不是斜率，而是忘記縱軸截距包含兩個接點。

對每個 $D$，$R_{\mathrm{total}}$ 最好由選定線性偏壓區的 I–V 斜率取得，而不是只拿單一 $V/I$。若 I–V 本身已經彎掉，後面的 TLM 直線即使 fit 得出來，也少了原本的 ohmic 前提。

## 5. 一組小型 Extraction Example

假設一組 TLM 結果經線性擬合後得到：

$$
R_{\mathrm{total}}
\approx
\left(0.429\ \Omega/\mu\mathrm{m}\right)D
+2.6\ \Omega
$$

若接點寬度 $Z=48\ \mu\mathrm{m}$，先從截距得到單一接點電阻：

$$
R_c\approx\frac{2.6}{2}=1.3\ \Omega
$$

再由斜率得到 sheet resistance：

$$
R_{\mathrm{sh}}
\approx
\left(0.429\ \Omega/\mu\mathrm{m}\right)
\left(48\ \mu\mathrm{m}\right)
\approx20.6\ \Omega/\square
$$

橫軸截距約為：

$$
D_x\approx-\frac{2.6}{0.429}\approx-6.1\ \mu\mathrm{m}
$$

因此：

$$
L_T\approx\frac{6.1}{2}\approx3.0\ \mu\mathrm{m}
$$

在這組標準 TLM 近似下，specific contact resistivity 還可以由下面的關係取得：

$$
\rho_c=R_{\mathrm{sh}}L_T^2
$$

這裡的長度要先換成公分：$3.0\ \mu\mathrm{m}=3.0\times10^{-4}\ \mathrm{cm}$。代回後：

$$
\rho_c
\approx
\left(20.6\ \Omega/\square\right)
\left(3.0\times10^{-4}\ \mathrm{cm}\right)^2
\approx1.9\times10^{-6}\ \Omega\cdot\mathrm{cm^2}
$$

算到這裡已經能把 slope、intercept 和三個參數接起來。前面的圖表讀值本來就是近似值，結果保留約兩位有效數字就夠了；多留幾位看起來比較精確，實際上沒有多帶回什麼資訊。

## 6. Linearity Does Not Guarantee a Physical Result

TLM 很像一個普通的 linear regression，因此很容易先看「線有沒有 fit 出來」。但只要給一組點，幾乎都能畫出一條線。真正麻煩的是，那條線不一定還有原本期待的物理意義。

如果 fit 看起來怪，會先回頭看幾件事：

- contact I–V 有沒有真的接近 ohmic；
- spacing range 和 $L_c/L_T$ 是否足以使用目前的近似；
- 不同接點或薄層有沒有明顯不均；
- self-heating、探針不穩定、儀器 offset 或 residual pattern 有沒有異常。

$R_{\mathrm{sh}}$ 主要來自斜率，$R_c$ 則依賴外推到 $D=0$ 的截距。當距離範圍太窄、資料點太少或散布偏大時，截距通常比斜率更不穩。只看 $R^2$ 不太夠，原始點和 residual 還是要留著。

若擬合得到負的縱軸截距，也不應直接報告一個負接觸電阻。這比較像是在提醒：量測 offset、接點幾何、薄層均勻性或模型假設，至少有一項還沒處理好。

原始點、I–V 線性、殘差和量測條件都要先站得住腳，直線才有物理上的意義。

## Keeping the Fit Reviewable

One part of TLM did feel familiar from my own engineering work: I do not trust a fitted number very much if I cannot trace it back to the data and settings that produced it.

When I worked on model evaluation, a final score was not enough if the dataset version, threshold, configuration, and raw predictions were missing. A fitted contact resistance has the same problem if the original spacing and resistance points, contact geometry, current range, fitting window, residuals, temperature, or sample identity are gone.

I would want the fitted value and its measurement context to stay together here too.

## What I Would Check Next

- 接點不接近 ohmic 時，不同 bias window 取得的 $R_{\mathrm{total}}$ 會怎麼改變 TLM fit？
- residual 出現固定方向時，還需要哪些比較才能區分薄層不均勻、接點差異與量測問題？

## References

- Arizona State University, [*Electrical Characterization: Diodes*](https://www.coursera.org/learn/electrical-characterization-diodes), Coursera.
