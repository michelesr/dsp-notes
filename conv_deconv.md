# Convoluzione e Deconvoluzione

## Risposta impulsiva

Per risposta impulsiva si intende la risposta del sistema a un impulso unitario.

    u(n): 1 if n == 0, else 0 

Per il sistema s vale:

    h(n) = s(u(n))

h(n) sarà quindi la risposta impulsiva del sistema s.

## Convoluzione

Il processo di convoluzione viene utilizzato nel calcolo dell'uscita di un
sistema di filtri digitali (FIR,IIR).

Sia X(n) il segnale d'ingresso ed H(n) la risposta impulsiva del sistema, entrambe
nel dominio temporale, abbiamo che il segnale di uscita è dato dalla seguente
relazione:

<!-- y(n) = conv(x(n), h(n)) = sum for k -> [-inf,+inf] : x(k)h(n-k) --->
    
![Convolution](http://latex.codecogs.com/gif.latex?y%28n%29%20%3D%20x%28n%29%20%5Cotimes%20h%28n%29%20%3D%20%5Csum_%7Bk%3D-%5Cinfty%7D%5E%7B%5Cinfty%7D%20x%28k%29h%28n-k%29)

Il processo di convoluzione gode delle seguenti proprietà:

 - distributiva
 - associativa
 - commutativa

![Convolution](https://upload.wikimedia.org/wikipedia/commons/b/b9/Convolution_of_spiky_function_with_box2.gif)

Vale la seguente relazione:

<!--- y(n) = conv(x(n),h(n)) = IDTFT(DTFT(x(n))DTFT(h(n))) --->
    
![Convolution and DTFT](http://latex.codecogs.com/gif.latex?y%28n%29%20%3D%20x%28n%29%20%5Cotimes%20h%28n%29%20%3D%20IDTFT%20%28X%28%5Ciota%20%5Comega%29H%28%5Ciota%20%5Comega%29%29)

DTFT(h(n)) è la risposta in frequenza del sistema, mentre DTFT(x(n)) è lo
spettro del segnale.

    octave:1> conv([1,1,1],[3,3,53,3])
    ans =

        3    6   59   59   56   3

Com'è possibile notare la lunghezza della sequenza di uscita è data dalla somma
delle lunghezze delle sequenze di input meno 1. (3+4-1 = 6) 

## Convoluzione circolare

La convoluzione circolare è un tipo di convoluzione che lavora con sequenze
periodiche.

A differenza della convoluzione lineare, quella circolare produce una sequenza
periodica che risente dei ritorni delle somme, per risolvere questo problema è
possibile rendere le sequenze di input periodiche di periodo (N+M-1) con N e M
le durate delle sequenze originali di input, tramite l'aggiunta di 0 in coda
alle sequenze di input stesse.

La convoluzione circolare veloce si ottiene tramite IFFT del prodotto delle FFT
delle sequenze periodiche ottenute aggiungendo zeri.

    octave:3> ifft(fft([1,1,1,0,0,0]).* fft([3,3,53,3,0,0]))
    ans =

    3    6   59   59   56    3

## Deconvoluzione 

Quando si conosce la risposta impulsiva causuale h(n) di un sistema e un segnale
di uscita y(n) prodotto attraverso il sistema, è possibile risalire al segnale di
ingresso x(n) tramite la seguente relazione:

<!-- x(n) = ( y(n) - ( sum for k -> [1,n] : h(k)x(n-k) ) ) / h(0) -->
    
![Deconvolution](http://latex.codecogs.com/gif.latex?x%28n%29%20%3D%20%5Cfrac%7By%28n%29%20-%20%5Csum_%7Bk%3D1%7D%5E%7Bn%7D%20h%28k%29x%28n-k%29%7D%5E%7Bh%280%29%7D)

Il processo viene chiamato deconvoluzione.

## Convoluzione per sezioni

Quando la sequenza x(n) ha durata infinita, è possibile spezzare x(n) in sezioni
che verranno elaborate tramite convoluzione (circolare). Esistono due metodi:

- overlap-add
- overlap-save

### Overlap-Add

Nel metodo overlap add si spezza X(n) in sequenze adiacenti Xm(n) di durata N,
si vanno poi ad aggiungere M-1 zeri per avere una sequenza di durata L = M+N-1
(M in questo caso si riferisce alla durata del h(n)), infine si calcola la
convoluzione tra Xm(n) e h(n) tramite fft, prodotto e ifft, e infine si sommano
gli M-1 campioni finali della Ym(n) ottenuta con i primi (M-1) campioni della
sequenza di uscita successiva.

![Overlap-Add](https://upload.wikimedia.org/wikipedia/commons/7/77/Depiction_of_overlap-add_algorithm.png)
 
    Yn     - - - + + +
    Yn+1         + + + - - -

### Overlap-Save

Nel metodo overlap save si spezza X(n) in sequenze adiacenti Xm(n) di durata L,
senza aggiungere zeri ma semplicemente considerando il valore dei campioni.

In questo modo, si ha che i primi (M-1) campioni di Xm(n) sono gli stessi (M-1)
ultimi campioni di Xm-1(n).

Applicando la convoluzione circolare in questa maniera abbiamo che i primi (M-1)
campioni della sequenza di output sono affetti da aliasing temporale, di
conseguenza li scartiamo a favore degli ultimi (M-1) campioni della sequenza
precedente.

![Overlap-Save](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ad/Overlap-save_algorithm.png/800px-Overlap-save_algorithm.png)

    Yn     / / / - - -
    Yn+1         / / / - - -



### Considerazioni sulla FFT e IFFT

Utilizzare una fft a decimazione nella frequenza e una ifft a decimazione nel
tempo permetterà di ottenere una sequenza di output ordinata correttamente.

Se si opera con sequenze reali conviene utilizzare una sola fft per calcolare 2
sezioni, costruendo la sequenza Xm(n) + iXm+1(n) che avrà come output della 
elaborazione la sequenza Ym(n) + iYm+1(n). 
