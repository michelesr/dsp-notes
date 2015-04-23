# Convoluzione e Deconvoluzione

## Risposta impulsiva

Per risposta impulsiva si intende la risposta del sistema a un impulso unitario.

    u(n): 1 if n == 0, else 0 

Per il sistema s(n) vale:

    h(n) = s(u(n))

h(n) sarà quindi la risposta impulsiva del sistema s(n).

## Convoluzione

Il processo di convoluzione viene utilizzato nel calcolo dell'uscita di un
sistema di filtri digitali (FIR,IIR).

Sia X(n) il segnale d'ingresso ed H(n) la risposta impulsiva del sistema, entrambe
nel dominio temporale, abbiamo che il segnale di uscita è dato dalla seguente
relazione:

    y(n) = conv(x(n), h(n)) = sum for k -> [-inf,+inf] : x(k)h(n-k)

Il processo di convoluzione gode delle seguenti proprietà:

 - distributiva
 - associativa
 - commutativa

Vale la seguente relazione:

    y(n) = conv(x(n),h(n)) = IDTFT(DTFT(x(n))DTFT(h(n)))

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
