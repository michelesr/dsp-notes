# Modelli di colore

Partendo dal presupposto che il bianco e' il colore a massima intensita', e il nero quello a minore intensita', sono stati sviluppati diversi [modelli colore](https://it.wikipedia.org/wiki/Modello_di_colore), i cui principali sono RGB, CMYK e HSI.

## RGB

Il modello [RGB](https://it.wikipedia.org/wiki/RGB) viene utilizzato per le luci, ad esempio nei display di computer, TV, proiettori, scanner, etc.

- colori primari: rosso, verde, blu
- colori secondari: ciano, magenta, giallo
- si basa sulla [mescolanza additiva](https://it.wikipedia.org/wiki/Mescolanza_additiva), per cui unendo i colori primari si ottiene il bianco
- la scala dei grigi consiste nei colori con la stessa intensita' dei colori primari

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/AdditiveColorMixiing.svg/200px-AdditiveColorMixiing.svg.png)

Due colori sono [complementari](https://it.wikipedia.org/wiki/Colori_complementari) quando sommati danno come risultato una luce acromatica (senza colore).  Visivamente, sono i colori in posizioni diametralmente opposte:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Colorwheel.svg/220px-Colorwheel.svg.png)

## CMYK

Il modello [CMYK](https://it.wikipedia.org/wiki/CMYK) viene utilizzando per i pigmenti, quindi inchiostro, tempere, stampanti, etc. Prende il nome dai colori primari (Cyan, Magenta, Yellow) e dal nero (Key black).

- colori primari: ciano, magenta, giallo
- colori secondari: rosso, verde, blu
- si basa sulla [mescolanza sottrattiva](https://it.wikipedia.org/wiki/Mescolanza_sottrattiva), per cui unendo i colori primari si ottiene il nero
- la scala dei grigi consiste nei colori con la stessa intensita' dei colori primari
- il fattore di conversione rispetto all'RGB e' lineare

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ac/SubtractiveColorMixing.png/200px-SubtractiveColorMixing.png)

## HSI

Il modello [HSI](https://it.wikipedia.org/wiki/Hue_Saturation_Brightness) (Hue, Saturation e Intensity) e' una scala alternativa che non prende i colori come base di riferimento.

- la scala dei grigi ha saturazione (Saturation) nulla, mentre quando la saturazione e' massima abbiamo colori vivi
- la tonalita' (Hue) nulla equivale al rosso per convenzione (`Hue=0 -> red`, `Hue=1/3 -> green`, `Hue=2/3 -> blue`)
- la luminosita' (Intensity) nulla equivale al nero, quella massima al bianco, mentre valori intermedi corrispondono a grigio 50%, e i colori che comunemente chiamano come rosso, arancione, giallo, etc
- il fattore di conversione rispetto ai modelli RGB e CMYK e' un po' macchinoso:
  - la luminosita' e' datto dalla media di R, G e B
  - la saturazione e la tonalita' sono piuttosto complicati

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/HSL_color_solid_dblcone_chroma_gray.png/197px-HSL_color_solid_dblcone_chroma_gray.png)

## CIELAB

Infine, il modello [CIELAB](https://it.wikipedia.org/wiki/Spazio_colore_Lab) ha come componenti principali `L`, la luminosita', ed `a` e `b`, componenti colore relative a `L`.

Si basa sulla percezione dell'occhio umano e quindi rimane piu' fedele, e' indipendente dal dispositivo di rappresentazione dell'immagine, e include totalmente gli spazi colore RGB e CMYK al punto che viene in genere utilizzato per la conversione tra questi spazi colore.
