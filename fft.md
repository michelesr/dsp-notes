# Fast Fourier Transform

L'`FFT` è un algoritmo utilizzato per il calcolo della `DFT`:

![DFT](http://latex.codecogs.com/gif.latex?X%28k%29%20%3D%20%5Csum_%7Bn%3D0%7D%5E%7BN-1%7Dx%28n%29e%5E%7B-%5Ciota%5Cfrac%7B2%5Cpi%20%7D%7BN%7D%20nk%7D%20%3D%20%5Csum_%7Bn%3D0%7D%5E%7BN-1%7Dx%28n%29W_N%5E%7Bnk%7D)

La premessa per l'utilizzo della `fft` è avere sequenze che hanno per durata
una potenza di `2`. 

Il principio fondamentale che sta sulla base dell'algoritmo di Cooley e Turkey
consiste nello spezzare la computazione di una `fft` in più `fft` su sequenze di
durata inferiore.

Infatti, il calcolo di tutti i valori della sequenza `X(k)` richiede `N^2` prodotti complessi e `N(N-1)` somme
complesse, ma se spezziamo il calcolo in sequenze dimezzate avremo `2(N/2)^2` e
`2(N/2)(N/2-1)` somme complesse. 

La scomposizione applicata in maniera ricorsiva ci porta al calcolo di `N/2` `fft`
di sequenze a durata `2`.

D'ora in poi useremo questa relazione:

![WN](http://latex.codecogs.com/gif.latex?W_N%5E%7Bk%7D%20%3D%20e%5E%7B-%5Ciota%20%5Cfrac%7B2%5Cpi%7D%7BN%7D%20%7D)

Ci son due metodi applicabili:

- decimazione nel tempo
- decimazione nella frequenza

## Decimazione nel tempo

Separiamo `x(n)` in due sequenze `x(2n)` e `x(2n+1)`, ovvero la prima ha gli elementi che nella sequenza originale avevano gli indici pari, mentre la seconda ha quelli con gli indici dispari.

La `DFT` `X(k)` è la somma di `2` `DTF` di lunghezza `N/2`:

![FFT(k)](http://latex.codecogs.com/gif.latex?X%28k%29%20%3D%20X_1%28k%29%20&plus;%20W_N%5E%7Bk%7DX_2%28k%29)

![FFT2(k)](http://latex.codecogs.com/gif.latex?X%28k&plus;%20%5Cfrac%7BN%7D%7B2%7D%29%20%3D%20X_1%28k%29%20-%20W_N%5E%7Bk%7DX_2%28k%29)

con `k` nell'intervallo `[0, N/2 - 1]`

![Time-decimation](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cb/DIT-FFT-butterfly.png/738px-DIT-FFT-butterfly.png)

Com'è possibile notare dal disegno, la sequenza trasformata ha gli indici
permutati, dunque come troviamo l'indice che ci serve? Basta invertire (leggerli
al contrario e non prenderne la negazione!) i bit del
nostro indice!

    0 = 000 -- 000 = 0
    1 = 001 -- 100 = 4
    2 = 010 -- 010 = 2
    3 = 011 -- 110 = 6
    4 = 100 -- 001 = 1
    5 = 101 -- 101 = 5
    6 = 110 -- 011 = 3
    7 = 111 -- 111 = 7

Questa tecnica prende il nome di `bit-reversal`.

## Decimazione nella frequenza

TODO
