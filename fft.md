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

La scomposizione applicata in maniera ricorsiva ci porta al calcolo di `N/2` FFT
di sequenze a durata `2`.

Ci son due metodi applicabili:

- decimazione nel tempo
- decimazione nella frequenza

## Decimazione nel tempo

## Decimazione nella frequenza
