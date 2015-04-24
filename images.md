# Immagini

## Filtraggio immagini nel dominio della frequenza

Data un'immagine `f(x,y)` di dimensioni `MxN`, si ricavano i parametri di
padding `P` e `Q` a seconda delle dimnesioni del filtro. Di solito si assume `P = 2M` e `Q = 2N`.

Si forma l'immagine padded, `fp(x,y)` di dimensioni `PxQ` estendendo la `f(x,y)`
con il necessario numero di zeri.

Si moltiplica `fp(x,y)` per `(-1)^(x+y)` per centrare la trasformata.

Si calcola la [DFT](https://en.wikipedia.org/wiki/Discrete_Fourier_transform),
`F(u,v)` dell'immagine `fp(x,y)`.

Si genera una funzione simmetrica reale `H(u,v)` di dimensioni `PxQ` con il
centro alle coordinate `(P/2, Q/2)`.

Si ottiene l'immagine `gp(x,y) = IDTF2D(H(u,v)F(u,v))*(-1)^(x+y)

L'immagine finale `g(x,y)` si ottiene attraverso l'estrazione della regione
`MxN` del quadrante in alto a sinistra di `gp(x,y)`

L'uso di una funzione filtro `H(u,v)` preserva la fase dell'immagine nel
processo.
