# Funzioni di trasferimento

Questa e' la parte piu' pratica relativa agli esercizi.

## Zeri e poli

In breve:

- zeri (o radici):  valori per cui si annulla il numeratore
- poli:  valori per cui si annulla il denominatore

## Metodi di risoluzione

- fattorizzazione (regole imparate alle superiori)
- scomposizione in fratte parziali (vedi sotto)
- long division:  divisione tra 2 polinomi con metodo in colonna, affinche' l'esponente del numeratore sia inferiore a quello del denominatore
- calcolo tra coefficienti della scomposizione (da vedere)
- residui:  TODO
- stabilita' BIBO:  verificare che tutti i resiqui (o zeri?) abbiano modulo `< 1` (nota: `<`, non `<=`)

Consigli:

- `i^2 = -1` e quindi se hai `-1` puoi manipolare i segni e fare scomposizioni e fattorizzazioni ulteriori
- con `i` al denominatore, si puo' moltiplicare per `i / i` per portare `i` al numeratore
- TODO funzioni Octave per verificare gli esercizi (es: scomposizione in fratte parziali bidirezionali)

### Scomposizione in fratte parziali

Per scomporre un polinomio in frazioni parziali, mi è stato molto utile il corso [Partial Fractions: Khan Academy](https://www.khanacademy.org/math/algebra2/polynomial_and_rational/partial-fraction-expansion/).

## Tipologie

Tipi di realizzazione:

- diretta II
- diretta II trasposta
- parallela di 2 filtri del secondo ordine, con diretta II
- parallela di 2 filtri del secondo ordine, con diretta II trasposta
- traliccio
- traliccio-scala

In vari casi e' richiesto di determinare la stabilita' del filtro in senso BIBO.

### Diretta II

E' sufficiente avere l'`1` come il coefficiente di `z^0` al denominatore.

### Diretta II trasposta

Come la diretta II, in cui bisogna:

- invertire versi dei triangolini
- sostituire `+` con `.` (e viceversa)
- altro?

### Cascata (in serie)

L'obiettivo e' ottenere il prodotto di piu' polinomi, principalmente attraverso la *fattorizzazione*.

### Parallelo

L'obiettivo e' ottenere la somma di piu' polinomi, principalmente attraverso la *scomposizione in fratte parziali*.

### Traliccio

### Traliccio-scala
