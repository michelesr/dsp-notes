# Immagini

## Filtraggio immagini nel dominio della frequenza

Data un'immagine `f(x,y)` di dimensioni `MxN`, si ricavano i parametri di
padding `P` e `Q` a seconda delle dimensioni del filtro. Di solito si assume `P = 2M` e `Q = 2N`.

Si forma l'immagine padded, `fp(x,y)` di dimensioni `PxQ` estendendo la `f(x,y)`
con il necessario numero di zeri.

Si moltiplica `fp(x,y)` per `(-1)^(x+y)` per centrare la trasformata.

Si calcola la [DFT](https://en.wikipedia.org/wiki/Discrete_Fourier_transform),
`F(u,v)` dell'immagine `fp(x,y)`.

Si genera una funzione simmetrica reale `H(u,v)` di dimensioni `PxQ` con il
centro alle coordinate `(P/2, Q/2)`.

Si ottiene l'immagine `gp(x,y) = IDTF2D(H(u,v)F(u,v))*(-1)^(x+y)`

L'immagine finale `g(x,y)` si ottiene attraverso l'estrazione della regione
`MxN` del quadrante in alto a sinistra di `gp(x,y)`

L'uso di una funzione filtro `H(u,v)` preserva la fase dell'immagine nel
processo.

### Smoothing nel dominio della frequenza

![Smoothing-PIC](https://upload.wikimedia.org/wikipedia/en/thumb/3/3f/It_is_a_picture_that_has_been_edited_with_a_Bokeh_effect_with_a_gaussian_blur_effect.jpg/400px-It_is_a_picture_that_has_been_edited_with_a_Bokeh_effect_with_a_gaussian_blur_effect.jpg)

I contorni e le transizioni di intensità più nette (come il `rumore`), aumentano il contenuto di alte frequenze nella trasformata. Per applicare un effetto di [smoothing](https://en.wikipedia.org/wiki/Image_smoothing) (sfocamento) si applica un filtro passabasso.

#### Low-Pass ideale

Lascia passare tutte le frequenze all'interno di un circolo di raggio `D` centrato nell'origine, e taglia le frequenze al di fuori del cerchio.

Il filtro gode di simmetria radiale, ed è quindi completamente definito da una sezione trasversale radiale, dove il punto di transizione è detto `frequenza di taglio`. Tale filtraggio introduce l'effetto [ringing](https://en.wikipedia.org/wiki/Ringing_artifacts), che diventa meno evidente al crescere della frequenza di taglio.

#### Butterworth e Gaussiano

Altri tipi di filtri sono il filtro [Butterworth](https://en.wikipedia.org/wiki/Butterworth_filter), che riduce lo `smoothing` ma elimina l'effetto `ringing` e [Gaussiano](https://en.wikipedia.org/wiki/Gaussian_filter), la cui risposta in frequenza e antitrasformata hanno la forma di una [funzione gaussiana](https://en.wikipedia.org/wiki/Gaussian_function).

## Modelli di colore

Partendo dal presupposto che il bianco e' il colore a massima intensita', e il nero quello a minore intensita', sono stati sviluppati diversi [modelli colore](https://it.wikipedia.org/wiki/Modello_di_colore), i cui principali sono RGB, CMYK e HSI.

### RGB

[**RGB**](https://it.wikipedia.org/wiki/RGB): Red, Green e Blue sono i colori primari della [mescolanza additiva](https://it.wikipedia.org/wiki/Mescolanza_additiva), ed unendoli viene il bianco (es: luci, display)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/SubtractiveColorMixing.png/200px-SubtractiveColorMixing.png)

### CMYK

[**CMYK**](https://it.wikipedia.org/wiki/CMYK): Cyan, Magenta, Yellow e Key black sono i colori primari della [mescolanza sottrattiva](https://it.wikipedia.org/wiki/Mescolanza_sottrattiva), ed unendoli viene il nero (es: pigmenti, inchiostro)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/AdditiveColorMixiing.svg/200px-AdditiveColorMixiing.svg.png)

### HSI

[**HSI**](https://it.wikipedia.org/wiki/Hue_Saturation_Brightness): Hue, Saturation e Intensity, e' una scala alternativa che non prende i colori come base di riferimento

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/HSL_color_solid_dblcone_chroma_gray.png/197px-HSL_color_solid_dblcone_chroma_gray.png)

### Considerazioni

Da notare che RGB e CMYK hanno i colori primari e secondari esattamente alternati, infatti:
- rosso, verde e blu sono primari nell'additiva, e secondari nella sottrattiva
- ciano, magenta e giallo sono secondari nell'additiva, e primari nella sottrattiva
