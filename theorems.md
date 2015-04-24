# Teoremi

## Teorema del Campionamento (Nyquist-Shannon)

(Nota: per `ΩT` si intende la frequenza di campionamento, e non il prodotto di `Ω` e `T`

Sia `ga(t)` un segnale analogico a banda limitata con `Ga(iΩ) = 0`, per
`|Ω| > |Ωm|` `Ga(t)` è totalmente determinato dai suoi campioni ga(nt), e può
essere fedelmente ricostruito dai campioni ga(nt) per `n in [-inf,+inf]`, se la
frequenza angolare di campionamento `ΩT >= 2Ωm` con `ΩT >= 2π/T`.

In altre parole, se vogliamo che il segnale a banda limitata `ga(t)` sia
ricostruibile dai suoi campioni, dobbiamo campionarlo con frequenza di
campionamento almeno pari a due volte la larghezza di banda. Il segnale potrà
essere ricostruito generando:

![Digital->Analog](http://latex.codecogs.com/gif.latex?g_p%28t%29%20%3D%20%5Csum_%7Bn%20%3D%20-%5Cinfty%7D%5E%7B%5Cinfty%7Dg%28n%29%5Cdelta%28t%20-%20nt%29)

e filtrando il segnale con un passabasso ideale.

Per evitare distorsioni dovute all'aliasing, prima di campionare il segnale lo si filtra con un low-pass (detto `anti-aliasing`) che genera un segnale a banda limitata. Il segnale viene campionato poi con frequenza `|ΩT| > |2Ωm|`. Anche il segnale di uscita è filtrato con un low-pass detto `reconstruction-filter`.
