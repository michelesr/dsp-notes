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
