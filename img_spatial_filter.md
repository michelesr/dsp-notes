# Filtraggio immagini nel dominio spaziale

Il **filtraggio spaziale** consiste nell'applicare un'operazione su ogni singolo
pixel prendendo come riferimento un *intorno* di quel pixel per calcolare il valore di intensità finale.

Il filtraggio crea quindi un nuovo pixel con le stesse coordinate del centro
dell'intorno, e il valore di intensità del pixel invece viene determinato sulla
base di un operazione applicata sui valori dei pixel nell'intorno.

Il fitraggio spaziale di un immagine `MxN` con un filtro `mxn` è dato da:

![Spatial-Filter](http://latex.codecogs.com/gif.latex?g%28x%2Cy%29%20%3D%20%5Csum_%7Bs%20%3D-a%7D%5E%7Ba%7D%5Csum_%7Bt%3D-b%7D%5E%7Bb%7Dw%28s%2Ct%29f%28x&plus;s%2Cy&plus;t%29)

    m = 2a+1
    n = 2b+1

Come è possibile intuire dalla formula, non si tratta di
[convoluzione](conv_deconv.md) ma di [correlazione](https://en.wikipedia.org/wiki/Correlation).

Calcolare la **correlazione** equivale a calcolare la *convoluzione* su una
funzione *maschera* `w(s,t)` ruotata di `180°`.

Valgono le seguenti relazioni:

![Spatial-Corr](http://latex.codecogs.com/gif.latex?corr%28w%28x%2Cy%29%2Cf%28x%2Cy%29%29%20%3D%20%5Csum_%7Bs%20%3D-a%7D%5E%7Ba%7D%5Csum_%7Bt%3D-b%7D%5E%7Bb%7Dw%28s%2Ct%29f%28x&plus;s%2Cy&plus;t%29)

![Spatial-Conv](http://latex.codecogs.com/gif.latex?conv%28w%28x%2Cy%29%2Cf%28x%2Cy%29%29%20%3D%20%5Csum_%7Bs%20%3D-a%7D%5E%7Ba%7D%5Csum_%7Bt%3D-b%7D%5E%7Bb%7Dw%28s%2Ct%29f%28x-s%2Cy-t%29)

L'utilizzo della *correlazione* o *convoluzione* per il **filtraggio spaziale** è
*indifferente* a patto di *ruotare* la *maschera* di `180°`.

Il concetto che sta dietro a queste operazioni è di *sommare i prodotti* tra i
valori dei pixel vicini e il valore della *maschera* per quei pixel (e quindi
possiamo vederla anche come una *somma di coefficienti* per i valori dei pixel
vicini). Naturalmente si considera pure il valore del pixel stesso.

## Filtro di media ponderata

Questo filtro assegna il valore del pixel centrale sulla base di una *media
pesata* dei valori del pixel centrale e dei vicini.

## Filtro di media (Box)

Simile alla *media ponderata* ma con *pesi uguali*.

## Filtri non lineari

Un esempio di filtro *non lineare* è il **filtro mediano** che sostituisce il pixel centrale con il valore mediano delle intensità della regione intorno al pixel.

Il *filtro mediano* è molto comodo per l'*eliminazione dei rumori*.

Altri filtri utilizzati sono il **max** e il **min**.

## Smoothing

![Smoothing](https://images.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.planetsourcecode.com%2FUpload_PSC%2FScreenShots%2FPIC20101271922318024.jpg&f=1)

Lo **smoothing** è ottenibile tramite *filtri lineari* come le *medie* o con
*filtri non lineari* come i *mediani*.

## Sharpening

![Sharpening](http://media-cache-ak0.pinimg.com/736x/7a/bb/24/7abb24b40effe4b85dfb75f7de73d8d6.jpg)

Lo **sharpening** nel dominio spaziale avviene tramite metodi che utilizzano *derivate* del primo e secondo ordine, in modo da amplificare i punti dove si hanno le massime variazioni di intensità.

## Unsharp Masking

Un tipico processo utilizzato dall'industria grafica e pubblicitaria per
applicare lo *sharpening* è l'**unsharp masking**.

Sfochiamo l'immagine originale (*smoothing*) e creiamo una *maschera* a partire dalla differenza tra l'immagine originale e la sfocata.

A questo punto avremo una maschera del tipo:

![m(x,y) = f(x,y) -
fsm(x,y)](http://latex.codecogs.com/gif.latex?m%28x%2Cy%29%20%3D%20f%28x%2Cy%29%20-%20f_%7Bsm%7D%28x%2Cy%29)

Il filtro si applica infine in questo modo:

![g(x,y) = f(x,y) +
km(x,y)](http://latex.codecogs.com/gif.latex?g%28x%2Cy%29%20%3D%20f%28x%2Cy%29%20&plus;%20k%20m%28x%2Cy%29)

* per `k = 1` abbiamo un *unsharp masking*
* per `k > 1` abbiamo un effetto *high-boost*, ovvero un'amplificazione delle altre frequenze (e quindi delle alte differenze di intensità)
* per `k < 1` il contributo di *sharpening* si riduce
