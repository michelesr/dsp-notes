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

### Sharpening nel dominio della frequenza

![Sharpening-PIC](https://upload.wikimedia.org/wikipedia/commons/4/43/Unsharped_eye.jpg)

Lo [sharpening](https://en.wikipedia.org/wiki/Sharpen_(digital_image)) nel dominio della frequenza si ottiene con l'applicazione di filtri `passa-alto`, che vanno a tagliare le frequenze al di fuori della `frequenza di taglio`.

## Modelli di colore

Partendo dal presupposto che il bianco e' il colore a massima intensita', e il nero quello a minore intensita', sono stati sviluppati diversi [modelli colore](https://it.wikipedia.org/wiki/Modello_di_colore), i cui principali sono RGB, CMYK e HSI.

### RGB

Il modello [RGB](https://it.wikipedia.org/wiki/RGB) viene utilizzato per le luci, ad esempio nei display di computer, TV, proiettori, scanner, etc.

- colori primari: rosso, verde, blu
- colori secondari: ciano, magenta, giallo
- si basa sulla [mescolanza additiva](https://it.wikipedia.org/wiki/Mescolanza_additiva), per cui unendo i colori primari si ottiene il bianco
- la scala dei grigi consiste nei colori con la stessa intensita' dei colori primari

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/AdditiveColorMixiing.svg/200px-AdditiveColorMixiing.svg.png)

Due colori sono [complementari](https://it.wikipedia.org/wiki/Colori_complementari) quando sommati danno come risultato una luce acromatica (senza colore).  Visivamente, sono i colori in posizioni diametralmente opposte:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Colorwheel.svg/220px-Colorwheel.svg.png)

### CMYK

Il modello [CMYK](https://it.wikipedia.org/wiki/CMYK) viene utilizzando per i pigmenti, quindi inchiostro, tempere, stampanti, etc. Prende il nome dai colori primari (Cyan, Magenta, Yellow) e dal nero (Key black).

- colori primari: ciano, magenta, giallo
- colori secondari: rosso, verde, blu
- si basa sulla [mescolanza sottrattiva](https://it.wikipedia.org/wiki/Mescolanza_sottrattiva), per cui unendo i colori primari si ottiene il nero
- la scala dei grigi consiste nei colori con la stessa intensita' dei colori primari
- il fattore di conversione rispetto all'RGB e' lineare

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/SubtractiveColorMixing.png/200px-SubtractiveColorMixing.png)

### HSI

Il modello [HSI](https://it.wikipedia.org/wiki/Hue_Saturation_Brightness) (Hue, Saturation e Intensity) e' una scala alternativa che non prende i colori come base di riferimento.

- la scala dei grigi ha saturazione (Saturation) nulla, mentre quando la saturazione e' massima abbiamo colori vivi
- la tonalita' (Hue) nulla equivale al rosso per convenzione (Hue = 0 -> rosso, Hue = 1/3 -> verde, Hue = 2/3 -> blu)
- la luminosita' (Intensity) nulla equivale al nero, quella massima al bianco, mentre valori intermedi corrispondono a grigio 50%, e i colori che comunemente chiamano come rosso, arancione, giallo, etc
- il fattore di conversione rispetto ai modelli RGB e CMYK e' un po' macchinoso:
  - la luminosita' e' datto dalla media di R, G e B
  - la saturazione e la tonalita' sono piuttosto complicati

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/HSL_color_solid_dblcone_chroma_gray.png/197px-HSL_color_solid_dblcone_chroma_gray.png)

### CIELAB

Infine, il modello [CIELAB](https://it.wikipedia.org/wiki/Spazio_colore_Lab) ha come componenti principali `L`, la luminosita', ed `a` e `b`, componenti colore relative a `L`.

Si basa sulla percezione dell'occhio umano e quindi rimane piu' fedele, e' indipendente dal dispositivo di rappresentazione dell'immagine, e include totalmente gli spazi colore RGB e CMYK al punto che viene in genere utilizzato per la conversione tra questi spazi colore.
