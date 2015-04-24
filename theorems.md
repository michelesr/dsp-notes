# Teoremi

## Teorema del Campionamento (Nyquist-Shannon)

(Nota: per `ΩT` si intende la frequenza di campionamento, e non il prodotto di `Ω` e `T`)

Sia `ga(t)` un segnale analogico a banda limitata con `Ga(iΩ) = 0`, per
`|Ω| > |Ωm|` `Ga(t)` è totalmente determinato dai suoi campioni `ga(nT)`, e può
essere fedelmente ricostruito dai campioni `ga(nT)` per `n in [-inf,+inf]`, se la
frequenza angolare di campionamento `ΩT >= 2Ωm` con `ΩT >= 2π/T`.

In altre parole, se vogliamo che il segnale a banda limitata `ga(t)` sia
ricostruibile dai suoi campioni, dobbiamo campionarlo con frequenza di
campionamento almeno pari a due volte la larghezza di banda. Il segnale potrà
essere ricostruito generando:

![Digital->Analog](http://latex.codecogs.com/gif.latex?g_p%28t%29%20%3D%20%5Csum_%7Bn%20%3D%20-%5Cinfty%7D%5E%7B%5Cinfty%7Dg%28n%29%5Cdelta%28t%20-%20nT%29)

e filtrando il segnale con un passabasso ideale.

### Considerazioni

    delta(n) = 1 if x == 0, 0 otherwise

Come potete vedere, l'argomento della funzione delta si annulla per `t - nT = 0` ovvero per `n = t/T`, in questo modo "selezionamo" `n` in modo da restituirci il campione relativo all'istante `t`.

#### Un piccolo esempio

Campionamo un segnale con frequenza di campionamento `ΩT = 200Hz`, il che significa che potremmo avere fedeltà fino a `100hz` di larghezza di banda. Il segnale analogico al tempo `2s` equivale al campione `400` della nostra sequenza campionata.

`ga(2) = g(2 * 200)` ovvero `ga(t) = g(t/T)`

### Aliasing

Per evitare distorsioni dovute all'aliasing, prima di campionare il segnale lo si filtra con un low-pass (detto `anti-aliasing`) che genera un segnale a banda limitata. Il segnale viene campionato poi con frequenza `|ΩT| > |2Ωm|`. Anche il segnale di uscita è filtrato con un low-pass detto `reconstruction-filter`.

## Teorema di Parseval

Il teorema di Parseval è presente in diverse forme e principalmente ci dice che la somma (o integrale) di una funzione nel dominio principale è uguale alla somma (o integrale) della funzione nel dominio trasformato.

### CTFT

![Parseval-CTFT](http://latex.codecogs.com/gif.latex?%5Cint_%7B-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7D%7Cx_a%28t%29%7C%5E2dt%20%3D%20%5Cfrac%7B1%7D%7B2%5Cpi%7D%7B%7D%5Cint_%7B-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7D%7CX_a%28%5Ciota%5COmega%29%7C%5E2d%5COmega)

### DTFT

![Parseval-DTFT-2](http://latex.codecogs.com/gif.latex?%5Csum_%7Bn%20%3D%20-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7Dg%28n%29h%5E*%28n%29%20%3D%20%5Cfrac%7B1%7D%7B2%5Cpi%7D%7B%7D%5Cint_%7B-%5Cpi%7D%5E%7B&plus;%5Cpi%7DG%28e%5E%7B%5Ciota%5Comega%7D%29H%5E*%28e%5E%7B%5Ciota%5Comega%7D%29d%5Comega)

![Parseval-DTFT](http://latex.codecogs.com/gif.latex?%5Csum_%7Bn%20%3D%20-%5Cinfty%7D%5E%7B&plus;%5Cinfty%7D%7Cx%28n%29%7C%5E2%20%3D%20%5Cfrac%7B1%7D%7B2%5Cpi%7D%7B%7D%5Cint_%7B-%5Cpi%7D%5E%7B&plus;%5Cpi%7D%7CX%28e%5E%7B%5Ciota%5Comega%7D%29%7C%5E2d%5Comega)

Queste sommatorie dei quadrati delle funzioni ci danno le "energie" dei vari segnali.

## Teorema di convoluzione

[Teorema di Convoluzione](conv_deconv.md#teorema-di-convoluzione)
