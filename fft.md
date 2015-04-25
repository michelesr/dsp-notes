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

![WN](http://latex.codecogs.com/gif.latex?W_N%5E%7D%20%3D%20e%5E%7B-%5Ciota%20%5Cfrac%7B2%5Cpi%7D%7BN%7D%20%7D)

Ci son due metodi applicabili:

- [decimazione nel tempo](fft.md#decimazione-nel-tempo)
- [decimazione nella frequenza](fft.md#decimazione-nella-frequenza)

Vedremo che nella decimazione nel tempo le sequenze vengono separate in sequenze a indici pari e dispari `2n` e `2n+1` nel dominio del tempo, e saranno sequente adiacenti nel dominio della frequenza `n` e `n+1`, mentre nella decimazione nella frequenza avremo il contrario.

In entrambi i casi la complessità computazionale è `O(N logN)`.

## Decimazione nel tempo

Separiamo `x(n)` in due sequenze `x(2n)` e `x(2n+1)`, ovvero la prima ha gli elementi che nella sequenza originale avevano gli indici pari, mentre la seconda ha quelli con gli indici dispari.

La `DFT` `X(k)` è la somma di `2` `DTF` di lunghezza `N/2`:

![FFT(k)](http://latex.codecogs.com/gif.latex?X%28k%29%20%3D%20X_1%28k%29%20&plus;%20W_N%5E%7Bk%7DX_2%28k%29)

![FFT2(k)](http://latex.codecogs.com/gif.latex?X%28k&plus;%20%5Cfrac%7BN%7D%7B2%7D%29%20%3D%20X_1%28k%29%20-%20W_N%5E%7Bk%7DX_2%28k%29)

con `k` nell'intervallo `[0, N/2 - 1]`.

![Time-decimation](http://cnx.org/resources/657717c02db3efbef5dd37729d676ba1/image4.png)

Com'è possibile notare dal disegno, la sequenza originale ha gli indici
permutati, dunque come troviamo l'indice corrispondente nella trasformazione? Basta invertire i bit del
nostro indice!

Per invertire si intende leggere al contrario, e non prendere la negazione del bit.

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

Questa volta spezziamo la sequenza `x(n)` in due sequenze `adiacenti`:

    x1(n) = x(n)        for n in [0, N/2-1]
    x2(n) = x(n + N/2)  for n in [0, N/2-1]
    
Per queste sequenze valgono le sequenti relazioni:

![X(2k)](http://latex.codecogs.com/gif.latex?X%282k%29%20%3D%20%5Csum_%7Bn%3D0%7D%5E%7B%5Cfrac%7BN%7D%7B2%7D-1%7D%5BX_1%28n%29&plus;X_2%28n%29%5DW_%7BN/2%7D%5E%7Bkn%7D)

![X(2k+1)](http://latex.codecogs.com/gif.latex?X%282k&plus;1%29%20%3D%20%5Csum_%7Bn%3D0%7D%5E%7B%5Cfrac%7BN%7D%7B2%7D-1%7D%5BX_1%28n%29-X_2%28n%29%5DW_N%5EnW_%7BN/2%7D%5E%7Bkn%7D)

Le due espressioni sopra sono le `DTF` su `N/2` campioni delle sequenze `f(n)` e `g(n)` definite come:

![F(n)](http://latex.codecogs.com/gif.latex?f%28n%29%20%3D%20x_1%28n%29%20&plus;%20x_2%28n%29)

![G(n)](http://latex.codecogs.com/gif.latex?g%28n%29%20%3D%20%28x_1%28n%29%20-%20x_2%28n%29%29%20W_N%5En)

Abbiamo infine le seguenti relazioni:

![1](http://latex.codecogs.com/gif.latex?x_1%28n%29%20%3D%20g%28n%29%3D%20%28x_1%28n%29%20-%20x_2%28n%29%29%20W_N%5E%7Bn%7D)

![2](http://latex.codecogs.com/gif.latex?x_2%28n%29%20%3D%20f%28n%29%3D%20x_1%28n%29%20&plus;%20x_2%28n%29)

con `n` nell'intervallo `[0, N/2 - 1]`.

Le trasformate `DFT` delle sequenze `f(n)` e `g(n)` ci danno dunque i termini pari e dispari, relativamente. Il procedimento viene iterato fino ad operare con sequenze di `2` campioni.

![Frequency-Decimation](http://www.transtutors.com/Uploadfile/CMS_Images/21120_Twiddle%20factor.JPG)

Come potete vedere nel disegno, le moltiplicazioni con le `W` vengono fatte dopo le somme (o differenze quando abbiamo `-1`). 

Inoltre possiamo notare che mentre nella decimazione nel tempo partivamo con
indici permutati, qui partiamo con indici ordinati e finiamo con indici
permutati sempre con la stessa regola del `bit-reversal`.

## FFT di sequenze reali

Se la nostra sequenza è reale, possiamo sfruttare la proprietà di simmetria per
ridurre il numero di operazioni necessarie.

### Con una sola sequenza reale

Costruiamo la sequenza `z(n)`:

    z(0) = x(0) + ix(1)
    z(1) = x(2) + ix(3)
    ...
    x(N/2-1) = x(N-2) + ix(N-1)

Per la nostra sequenza vale la seguente relazione:

![FFT-Real-1](http://latex.codecogs.com/gif.latex?X_1%28k%29%20%3D%20%5Cfrac%7BZ%28k%29%20&plus;Z%5E*%28%5Cfrac%7BN%7D%7B2%7D-k%29%7D%7B2%7D)

![FFT-Real-2](http://latex.codecogs.com/gif.latex?X_2%28k%29%20%3D%20%5Cfrac%7BZ%28k%29%20-Z%5E*%28%5Cfrac%7BN%7D%7B2%7D-k%29%7D%7B2%5Ciota%7D)

### Con due sequenze reali

Combiniamo le due sequenze reali `x(n)` e `y(n)` nella sequenza:

    z(n) = x(n) + iy(n)

Avremo la seguente relazione:

![FFT-Real-3](http://latex.codecogs.com/gif.latex?X%28k%29%20%3D%20%5Cfrac%7BZ%28k%29%20&plus;%20Z%5E*%28N-k%29%7D%7B2%7D)

![FFT-Real-4](http://latex.codecogs.com/gif.latex?Y%28k%29%20%3D%20%5Cfrac%7BZ%28k%29%20-Z%5E*%28N-k%29%7D%7B2%5Ciota%7D)

## Inverse FFT

L'algoritmo per calcolare la `ifft` è lo stesso utilizzato per il calcolo della
`fft` con l'accorgimento di sostituire i vari `Wk` con `(Wk)^(-1)` e di dividere
il risultato finale per `N`.
