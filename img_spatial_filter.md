# Filtraggio immagini nel dominio spaziale

Il `filtraggio spaziale` consiste nell'applicare una operazione su ogni singolo
pixel prendendo come riferimento un `intorno` di quel pixel per calcolare il valore di intensità finale.

Il filtraggio crea quindi un nuovo pixel con le stesse coordinate del centro
dell'intorno, e il valore di intensità del pixel invece viene determinato sulla
base di un operazione applicata sui valori dei pixel nell'intorno.

Il fitraggio spaziale di un immagine `MxN` con un filtro `mxn` è dato da:

![Spatial-Filter](http://latex.codecogs.com/gif.latex?g%28x%2Cy%29%20%3D%20%5Csum_%7Bs%20%3D-a%7D%5E%7Ba%7D%5Csum_%7Bt%3D-b%7D%5E%7Bb%7Dw%28s%2Ct%29f%28x&plus;s%2Cy&plus;t%29)

Come è possibile intuire dalla formula, non si tratta di
[convoluzione](conv_deconv.md) ma di [correlazione](https://en.wikipedia.org/wiki/Correlation).

Calcolare la `correlazione` equivale a calcolare la `convoluzione` su una
funzione `maschera` `w(s,t)` ruotata di `180°`.

Valgono le seguenti relazioni:

![Spatial-Corr](http://latex.codecogs.com/gif.latex?corr%28w%28x%2Cy%29%2Cf%28x%2Cy%29%29%20%3D%20%5Csum_%7Bs%20%3D-a%7D%5E%7Ba%7D%5Csum_%7Bt%3D-b%7D%5E%7Bb%7Dw%28s%2Ct%29f%28x&plus;s%2Cy&plus;t%29)

![Spatial-Conv](http://latex.codecogs.com/gif.latex?conv%28w%28x%2Cy%29%2Cf%28x%2Cy%29%29%20%3D%20%5Csum_%7Bs%20%3D-a%7D%5E%7Ba%7D%5Csum_%7Bt%3D-b%7D%5E%7Bb%7Dw%28s%2Ct%29f%28x-s%2Cy-t%29)

L'utilizzo della `correlazione` o `convoluzione` per il `filtraggio spaziale` è
`indifferente` a patto di `ruotare` la `maschera` di `180 gradi`.

Il concetto che sta dietro a queste operazioni è di `sommare` i `prodotti` tra i
valori dei pixel vicini e il valore della `maschera` per quei pixel (e quindi
possiamo vederla anche come una somma di `coefficienti` per i valori dei pixel
vicini). Naturaolmente si considera pure il valore del pixel stesso.

## Filtro di media ponderata

Questo filtro assegna il valore del pixel centrale sulla base di una `media
pesata` dei valori del pixel centrale e dei vicini.

## Filtro di media (Box)

Simile alla `media ponderata` ma con `pesi` uguali.

## Filtri non lineari

Un esempio di filtro `non lineare` è il filtro `mediano` che sostituisce il pixel centrale con il valore mediano delle intensità della regione intorno al pixel.

Il `filtro mediano` è molto comodo per la `eliminazione dei rumori`.

Un altro filtro che si usa è il `max`.
