# Immagini nel dominio della frequenza

## Spettro delle Immagini

### CTFT

Sia `(f(x,y))` una funzione continua di variabili continue, la sua *trasformata
a tempo continuo di Fourier* si definisce come:

![CTFT-2d](http://latex.codecogs.com/gif.latex?F%28%5Cmu%2C%5Cnu%29%20%3D%20%5Cint_%7B-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7D%5Cint_%7B-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7Df%28x%2Cy%29%20e%5E%7B-%5Ciota%202%5Cpi%28%5Cmu%20x%20&plus;%20%5Cnu%20y%29%7Ddxdy)

Mentre la trasformata inversa invece è data da:

![ICTFT-2d](http://latex.codecogs.com/gif.latex?f%28x%2Cy%29%3D%20%5Cint_%7B-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7D%5Cint_%7B-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7DF%28%5Cmu%2C%5Cnu%29%20e%5E%7B%5Ciota%202%5Cpi%28%5Cmu%20x%20&plus;%20%5Cnu%20y%29%7Dd%5Cmu%20d%5Cnu)

Il dominio trasformato viene definito *dominio della frequenza*, e le variabili
indipendenti, nel caso delle immagini, hanno l'unità di misura definita in
`cicli/m`.

Come abbiamo visto per lo spettro dei segnali, anche quà il lobo principale
tende a contrarsi all'aumentare delle dimensioni dell'immagine originale.

### DFT

Per un immagine `MxN` viene così definita:

![DFT-2d](http://latex.codecogs.com/gif.latex?F%28%5Cmu%2C%20%5Cnu%29%20%3D%20%5Csum_%7B%5Cmu%20%3D%200%7D%5E%7BM-1%7D%5Csum_%7B%5Cnu%20%3D%200%7D%5E%7BN-1%7Df%28x%2Cy%29e%5E%7B-%5Ciota%202%5Cpi%28%5Cfrac%7B%5Cmu%20x%7D%7BM%7D%20&plus;%20%5Cfrac%7B%5Cmu%20y%7D%7BN%7D%29%7D)

L'inversa è:

![IDFT-2d](http://latex.codecogs.com/gif.latex?f%28x%2Cy%29%20%3D%20%5Cfrac%7B1%7D%7BMN%7D%5Csum_%7B%5Cmu%20%3D%200%7D%5E%7BM-1%7D%5Csum_%7B%5Cnu%20%3D%200%7D%5E%7BN-1%7DF%28%5Cmu%2C%5Cnu%29e%5E%7B%5Ciota%202%5Cpi%28%5Cfrac%7B%5Cmu%20x%7D%7BM%7D%20&plus;%20%5Cfrac%7B%5Cmu%20y%7D%7BN%7D%29%7D)

Lo spettro è periodico sulle dimensioni `MxN`, quindi al di fuori di quella
sezione i valori si ripetono.

Per funzioni reali, lo spettro è a *simmetria coniugata*, per le immaginarie
(quelle con `Re(f(x,y))=0`) è ad *antisimmetria coniugata*.

### Interpetazione dello spettro delle immagini (facoltativo)

A differenza del caso dei segnali, lo spettro delle immagini risulta meno
leggibile e interpretabile. In parole povere, non ci si può aspettare di
interpretare facilmente l'informazione contenuta nello spettro.

Allo stesso modo, non è consigliabile il design di filtri nel dominio della
frequenza. Infatti, la caratteristica principale delle immagini sono i bordi,
che son composti da un range vasto di frequenze. Di solito è meglio lavorare nel
*dominio spaziale* e ragionare in termini di *smoothing* e *sharpening*
piuttosto che di filtraggi *high-pass* e *low-pass*.

Modificare un immagine nel dominio della frequenza in generale non è produttivo,
ma d'altro canto, il dominio trasformato ha delle particolari proprietà, tra cui
il fatto che la *convoluzione* nel dominio spaziale è un *prodotto* nel dominio della frequenza (per il [teorema di convoluzione](https://en.wikipedia.org/wiki/Convolution_theorem)). Questa proprietà introduce quindi una semplificazione delle operazioni.

Fonte: http://www.dspguide.com/ch24/5.htm

## Filtraggio immagini nel dominio della frequenza

Data un'immagine `f(x,y)` di dimensioni `MxN`, si ricavano i parametri di
padding `P` e `Q` a seconda delle dimensioni del filtro. Di solito si assume `P = 2M` e `Q = 2N`.

* si forma l'immagine padded, `fp(x,y)` di dimensioni `PxQ` estendendo la `f(x,y)`
con il necessario numero di zeri
* si moltiplica `fp(x,y)` per `(-1)^(x+y)` per centrare la trasformata
* si calcola la [DFT](https://en.wikipedia.org/wiki/Discrete_Fourier_transform),
`F(u,v)` dell'immagine `fp(x,y)`
* si genera una funzione simmetrica reale `H(u,v)` di dimensioni `PxQ` con il
centro alle coordinate `(P/2, Q/2)`
* si ottiene l'immagine `gp(x,y) = IDTF2D(H(u,v)F(u,v))*(-1)^(x+y)`
* l'immagine finale `g(x,y)` si ottiene attraverso l'estrazione della regione
`MxN` del quadrante in alto a sinistra di `gp(x,y)`

L'uso di una funzione filtro `H(u,v)` preserva la fase dell'immagine nel
processo.

### Smoothing nel dominio della frequenza

![Smoothing-PIC](https://upload.wikimedia.org/wikipedia/en/thumb/3/3f/It_is_a_picture_that_has_been_edited_with_a_Bokeh_effect_with_a_gaussian_blur_effect.jpg/400px-It_is_a_picture_that_has_been_edited_with_a_Bokeh_effect_with_a_gaussian_blur_effect.jpg)

I contorni e le transizioni di intensità più nette (come il *rumore*), aumentano il contenuto di alte frequenze nella trasformata. Per applicare un effetto di [smoothing](https://en.wikipedia.org/wiki/Image_smoothing) (sfocamento) si applica un filtro passabasso.

#### Low-Pass ideale

Lascia passare tutte le frequenze all'interno di un circolo di raggio `D` centrato nell'origine, e taglia le frequenze al di fuori del cerchio.

Il filtro gode di simmetria radiale, ed è quindi completamente definito da una sezione trasversale radiale, dove il punto di transizione è detto *frequenza di taglio*. Tale filtraggio introduce l'effetto [ringing](https://en.wikipedia.org/wiki/Ringing_artifacts), che diventa meno evidente al crescere della frequenza di taglio.

#### Butterworth e Gaussiano

Altri tipi di filtri sono il filtro [Butterworth](https://en.wikipedia.org/wiki/Butterworth_filter), che riduce lo *smoothing* ma elimina l'effetto *ringing* e [Gaussiano](https://en.wikipedia.org/wiki/Gaussian_filter), la cui risposta in frequenza e antitrasformata hanno la forma di una [funzione gaussiana](https://en.wikipedia.org/wiki/Gaussian_function).

### Sharpening nel dominio della frequenza

![Sharpening-PIC](https://upload.wikimedia.org/wikipedia/commons/4/43/Unsharped_eye.jpg)

Lo [sharpening](https://en.wikipedia.org/wiki/Sharpen_(digital_image)) nel dominio della frequenza si ottiene con l'applicazione di filtri *passa-alto*, che vanno a tagliare le frequenze al di fuori della *frequenza di taglio*.
