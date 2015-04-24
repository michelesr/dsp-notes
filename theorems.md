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

Campionamo un segnale con frequenza di campionamento `ΩT = 200Hz`, il che significa che potremmo avere fedeltà fino a `100hz` di larghezza di banda. Il segnale analogico al tempo `2s` equivale al campione 200 della nostra sequenza campionata.

`ga(2) = g(2 * 200)` ovvero `ga(t) = g(t/T)`

### Aliasing

Per evitare distorsioni dovute all'aliasing, prima di campionare il segnale lo si filtra con un low-pass (detto `anti-aliasing`) che genera un segnale a banda limitata. Il segnale viene campionato poi con frequenza `|ΩT| > |2Ωm|`. Anche il segnale di uscita è filtrato con un low-pass detto `reconstruction-filter`.
