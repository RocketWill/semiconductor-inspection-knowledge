# Carriers, Transport, and Optical Response

## 從能帶、載子移動到光學檢測訊號

> **Learning Context**
>
> I had encountered energy bands, doping, mobility, and conductivity in project discussions, but I still held them as separate facts. The part I had missed was simple: having more carriers does not say how easily they move. Putting concentration and mobility into the same conductivity equation finally connected those ideas.
>
> This also changed how I read camera data. Exposure, illumination, surface condition, optics, and processing all contribute to the recorded image. An optical pattern and an electrical change are still different evidence until their measurement contexts are aligned and the relationship is independently checked.

## 1. Carrier Concentration、Mobility 和 Conductivity

剛開始接觸半導體導電行為時，很容易把「自由電子比較多」直接理解成「導電率比較高」。方向沒有完全錯，不過只看到了載子數量。載子除了要存在，也要能在電場下移動。

先把三個容易混在一起的量拆開：

| Quantity | 符號 | 這裡的理解 |
| --- | --- | --- |
| Carrier concentration | $n$、 $p$ | 單位體積內可以參與導電的電子或電洞數量 |
| Mobility | $\mu_n$、 $\mu_p$ | 載子在電場下移動的容易程度 |
| Conductivity | $\sigma$ | 載子數量和移動能力共同形成的傳導結果 |

摻雜可以增加主要載子濃度，缺陷、散射和溫度則會影響 mobility。最後量到的 conductivity，才是這些 contribution 疊在一起後的結果。

## 2. 從 Energy Bands 到 Carrier Concentration

許多原子形成固體後，原本離散的能階彼此接近並展開成能帶。對半導體而言，最常用到的是 valence band、conduction band，以及兩者之間的 bandgap：

```math
E_g=E_C-E_V
```

電子取得足夠能量並跨越 bandgap 後，conduction band 多出一個可以參與傳導的電子，valence band 則留下可以用電洞描述的空缺。電洞不是另一種基本粒子，而是價帶中未被電子占據狀態的準粒子描述。第一次看到這個說法不太直觀，放進電流與載子輸運的計算後才比較好用。

Fermi level $E_F$ 也不是某一顆電子所在的位置，而是描述能態占據機率的參考。Fermi–Dirac distribution 為：

```math
f(E)
=
\frac{1}
{1+\exp\left(\frac{E-E_F}{k_BT}\right)}
```

在非簡併、熱平衡的近似下，電子與電洞濃度可以寫成：

```math
n
=
N_C\exp\left(-\frac{E_C-E_F}{k_BT}\right)
```

```math
p
=
N_V\exp\left(-\frac{E_F-E_V}{k_BT}\right)
```

現階段先看指數項的方向就很有用： $E_F$ 越接近 $E_C$， $n$ 越高；越接近 $E_V$， $p$ 越高。 $N_C$、 $N_V$ 也會隨溫度變化，所以溫度的影響不只藏在指數項裡。

對本徵半導體， $n=p=n_i$。在相同近似下：

```math
np=n_i^2
```

摻入 donor 後，電子通常成為多數載子；摻入 acceptor 後，電洞通常成為多數載子。不過 n 型或 p 型不代表材料只剩下一種載子。電子與電洞仍然同時存在，只是濃度可能差很多。

## 3. 載子存在之後，還要能夠移動

沒有外加電場時，載子仍進行隨機熱運動，平均後不形成固定方向的淨電流。施加電場 $\mathcal{E}$ 後，在低電場、近似線性的範圍內：

```math
|v_d|=\mu|\mathcal{E}|
```

電子的實際漂移方向與電場相反，電洞則與電場同方向。工程計算通常先把 mobility $\mu$ 當成正值，方向另外處理。

Mobility 可能受到晶格振動、ionized impurity scattering、缺陷、界面、載子濃度與電場強度影響。這也是為什麼增加摻雜雖然通常會增加主要載子數量，卻可能同時加強雜質散射並降低 mobility。

![載子濃度、mobility 與 conductivity 之間的關係](../assets/02-semiconductor-characterization-illustrations/01-carrier-density-and-mobility.png)

> 圖 1：Conductivity 同時受到 carrier concentration 與 mobility 影響；增加載子數量不代表 conductivity 必然等比例增加。

在均勻材料、低電場，而且載子輸運可以用 drift mobility 近似時：

```math
\sigma=q\left(n\mu_n+p\mu_p\right)
```

接著可得到：

```math
J=\sigma\mathcal{E},\qquad \rho=\frac{1}{\sigma}
```

這裡的 $\rho$ 是材料 resistivity，不是某個元件直接量到的 resistance。元件的幾何、接點和接面還沒放進來。

單位可以順手驗一次。若 $\mu_n=1000\ \mathrm{cm^2/(V\cdot s)}$、 $\mathcal{E}=100\ \mathrm{V/cm}$：

```math
|v_d|
=
\left(1000\ \mathrm{cm^2/(V\cdot s)}\right)
\left(100\ \mathrm{V/cm}\right)
=
1.0\times10^5\ \mathrm{cm/s}
```

算式很短，留下它主要是確認最後真的得到速度單位。這個線性關係到了高電場、速度飽和或明顯非均勻結構時，就不應繼續直接套用。

## 4. 溫度改變時，兩個方向可能同時發生

溫度升高時，更多電子可能跨越 bandgap，使本徵載子濃度增加；另一方面，晶格振動也會增加，mobility 可能下降。因此 conductivity 的溫度變化不能只記成「溫度越高，載子移動越快」。這句話太省略了。

在 freeze-out regime，可用載子仍受摻雜原子游離程度限制。進入 extrinsic regime 後，主要載子濃度大致由摻雜控制，mobility 的變化會更明顯。溫度再升高到 intrinsic regime，熱生成的 electron–hole pairs 才逐漸主導。

這三個區段只是看趨勢時的順序，不是所有材料共用的固定溫度表。真正拿到資料後，還是要先確認材料、摻雜濃度與量測範圍。

## 5. Bandgap 和 Optical Response

光子能量為：

```math
E_{\mathrm{ph}}
=
h\nu
=
\frac{hc}{\lambda}
```

若波長使用 nm、能量使用 eV，可用：

```math
E_{\mathrm{ph}}(\mathrm{eV})
\approx
\frac{1240}{\lambda(\mathrm{nm})}
```

例如 $620\ \mathrm{nm}$ 對應約 $2.0\ \mathrm{eV}$。當光子能量足以跨越 bandgap 時，可能產生 electron–hole pair。不過能量足夠只是第一個條件，不代表每個入射光子都會被吸收；材料厚度、表面反射和允許的 transition 仍然會改變結果。

光子的動量相對較小，因此 transition 還要考慮 crystal momentum：

- direct bandgap 的 valence-band maximum 與 conduction-band minimum 位於近似相同的 crystal momentum；
- indirect bandgap 的兩者位置不同，transition 通常還需要 phonon 協助提供或吸收動量。

![Direct 與 indirect bandgap 的簡化 E-k 關係](../assets/02-semiconductor-characterization-illustrations/02-direct-and-indirect-bandgap.svg)

> 圖 2：Direct transition 可在近似相同的 crystal momentum 下進行；indirect transition 通常還需要 phonon 協助。能帶曲率與能量距離未按比例繪製。

矽是 indirect-bandgap semiconductor；GaAs 等材料則具有 direct bandgap。不過 bandgap 類型不能直接拿來解釋 AOI 影像中的每個亮點、暗點或紋理。可見影像的對比往往更直接受到表面形貌、反射、散射、薄膜干涉、污染與照明幾何影響。

## 6. Why a Camera Signal Is Not a Carrier Measurement

In the Vision Console, I implemented controls for exposure, gain, white balance, gamma, frame rate, ROI configuration, and image-processing pipelines. A separate wafer-inspection runtime retained camera identity, ROI measurements, grayscale differences, motion state, and trigger context.

Those fields were useful for operation, debugging, and result reproduction. After working through carrier transport, I read them a little differently. An image is a response shaped by the surface, illumination, optics, sensor settings, and processing. Increasing exposure or gain can make the same region brighter, but it does not mean the material's bandgap, carrier concentration, mobility, or conductivity has changed.

An optical pattern can still be useful evidence. Before comparing it with an electrical result, I would want the camera and illumination settings, ROI, focus, scale, wafer position, timestamp, bias, temperature, test structure, and process context to remain traceable. A repeated spatial relationship can support another check. It does not verify a material mechanism by itself.

## Current Scope

This note stays with basic carrier statistics, low-field transport, and optical-response concepts. The project connection is limited to measurement context; the camera systems did not measure semiconductor carrier properties directly. Junction behavior and parameter extraction are left to the notes that follow; Hall measurement remains outside the current scope.

## Learning Source

- Arizona State University, [*Fundamentals of Semiconductor Characterization*](https://www.coursera.org/learn/fundamentals-of-semiconductor-characterization), Coursera.
