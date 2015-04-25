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

## Modelli di colore

Partendo dal presupposto che il bianco e' il colore a massima intensita', e il nero quello a minore intensita', sono stati sviluppati diversi [modelli colore](https://it.wikipedia.org/wiki/Modello_di_colore), i cui principali sono RGB, CMYK e HSI.

### RGB

Nel modello [RGB](https://it.wikipedia.org/wiki/RGB), rosso (Red), verde (Green) e blu (Blue) sono i colori primari della [mescolanza additiva](https://it.wikipedia.org/wiki/Mescolanza_additiva), ed unendoli viene il bianco.

- colori primari: rosso, verde, blu
- colori secondari: ciano, magenta, giallo
- utilizzato nelle luci, ad esempio nei display di computer, TV, proiettori, scanner, etc
- la scala dei grigi consiste nei colori con la stessa intensita' di R, G e B

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/AdditiveColorMixiing.svg/200px-AdditiveColorMixiing.svg.png)

Due colori sono [complementari](https://it.wikipedia.org/wiki/Colori_complementari) quando sommati danno come risultato una luce acromatica (senza colore).  Visivamente, sono i colori in posizioni opposte:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Colorwheel.svg/220px-Colorwheel.svg.png)

### CMYK

Il modello [CMYK](https://it.wikipedia.org/wiki/CMYK) prende i nomi dai colori primari (Cyan, Magenta, Yellow) e dal nero (Key black) e si basa sulla [mescolanza sottrattiva](https://it.wikipedia.org/wiki/Mescolanza_sottrattiva), infatti unendo i primari si ottiene il nero.

- colori primari: ciano, magenta, giallo
- colori secondari: rosso, verde, blu
- utilizzando per i pigmenti, quindi inchiostro, tempere, stampanti, etc
- la scala dei grigi consiste nei colori con la stessa intensita' di C, M, Y

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/SubtractiveColorMixing.png/200px-SubtractiveColorMixing.png)

### HSI

[**HSI**](https://it.wikipedia.org/wiki/Hue_Saturation_Brightness): Hue, Saturation e Intensity, e' una scala alternativa che non prende i colori come base di riferimento

- la scala dei grigi ha saturazione (Saturation) nulla, mentre quando la saturazione e' massima abbiamo colori vivi
- la tonalita' (Hue) nulla equivale al rosso per convenzione (Hue = 0 -> rosso, Hue = 1/3 -> verde, Hue = 2/3 -> blu)
- la luminosita' (Intensity) nulla equivale al nero, quella massima al bianco, mentre valori intermedi corrispondono a grigio 50%, e i colori che comunemente chiamano come rosso, arancione, giallo, etc

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/HSL_color_solid_dblcone_chroma_gray.png/197px-HSL_color_solid_dblcone_chroma_gray.png)
