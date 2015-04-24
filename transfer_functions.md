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

- diretta
- diretta II
- diretta II trasposta
- parallela di 2 filtri del secondo ordine, con diretta II
- parallela di 2 filtri del secondo ordine, con diretta II trasposta
- traliccio
- traliccio-scala

In vari casi e' richiesto di determinare la stabilita' del filtro in senso BIBO.

### Diretta

Si disegna direttamente, di seguito un filtro FIR.

![](http://latex.codecogs.com/gif.latex?H%28z%29%20%3D%201%20-%20%5Cfrac%7B13%7D%7B4%7Dz%5E%7B-1%7D%20-%20%5Cfrac%7B3%7D%7B2%7Dz%5E%7B-2%7D%20&plus;%202z%5E%7B-3%7D%20-%20%5Cfrac%7B1%7D%7B2%7Dz%5E%7B-4%7D)

![](images/direct.png)

### Diretta II

E' sufficiente avere l'`1` come il coefficiente di `z^0` al denominatore.

![](http://latex.codecogs.com/gif.latex?%5Cfrac%7B%20%5Cfrac%7B1%7D%7B3%7D%20-%5Cfrac%7B1%7D%7B8%7Dz%5E%7B-1%7D%20-%5Cfrac%7B3%7D%7B4%7Dz%5E%7B-2%7D%20&plus;%5Cfrac%7B7%7D%7B24%7Dz%5E%7B-3%7D%20&plus;%20z%5E%7B-4%7D%20%7D%7B%201%20&plus;%20%5Cfrac%7B7%7D%7B24%7Dz%5E%7B-1%7D%20-%5Cfrac%7B3%7D%7B4%7Dz%5E%7B-2%7D%20-%5Cfrac%7B1%7D%7B8%7Dz%5E%7B-3%7D%20&plus;%20%5Cfrac%7B1%7D%7B3%7Dz%5E%7B-4%7D%20%7D)

![](images/direct2.png)

### Diretta II trasposta

Come la diretta II, in cui bisogna:

- invertire versi dei triangolini
- sostituire `+` con `.` (e viceversa)
- altro?

![](images/direct2_transposed.png)

### Cascata (in serie)

L'obiettivo e' ottenere il prodotto di piu' polinomi, principalmente attraverso la *fattorizzazione*.

### Parallelo

L'obiettivo e' ottenere la somma di piu' polinomi, principalmente attraverso la *scomposizione in fratte parziali*.

### Traliccio

0. Prendiamo la seguente funzione di trasferimento

    ![](http://latex.codecogs.com/gif.latex?H%28z%29%20%3D%201%20-%20%5Cfrac%7B13%7D%7B4%7Dz%5E%7B-1%7D%20-%20%5Cfrac%7B3%7D%7B2%7Dz%5E%7B-2%7D%20&plus;%202z%5E%7B-3%7D%20-%20%5Cfrac%7B1%7D%7B2%7Dz%5E%7B-4%7D)

1. Vediamo che il primo coefficiente e' gia' `1`, quindi ok

2. Prendiamo il primo `k` (ultimo coefficiente)

    ![](http://latex.codecogs.com/gif.latex?k_4%20%3D%20-%20%5Cfrac%7B1%7D%7B2%7D)

3. sottraiamo `k * H(z) a coefficienti invertiti`

    ![](http://latex.codecogs.com/gif.latex?H%28z%29%20%3D%201%20-%20%5Cfrac%7B13%7D%7B4%7Dz%5E%7B-1%7D%20-%20%5Cfrac%7B3%7D%7B2%7Dz%5E%7B-2%7D%20&plus;%202z%5E%7B-3%7D%20-%20%5Cfrac%7B1%7D%7B2%7Dz%5E%7B-4%7D%20&plus;%20%5Cfrac%7B1%7D%7B2%7D%20%28-%20%5Cfrac%7B1%7D%7B2%7D%20&plus;%202z%5E%7B-1%7D%20-%20%5Cfrac%7B3%7D%7B2%7Dz%5E%7B-2%7D%20-%20%5Cfrac%7B13%7D%7B4%7Dz%5E%7B-3%7D%20&plus;%20z%5E%7B-4%7D%29)

    ![](http://latex.codecogs.com/gif.latex?%5Cfrac%7B3%7D%7B4%7D%20-%20%5Cfrac%7B9%7D%7B4%7Dz%5E%7B-1%7D%20-%20%5Cfrac%7B9%7D%7B4%7Dz%5E%7B-2%7D%20&plus;%20%5Cfrac%7B3%7D%7B8%7Dz%5E%7B-3%7D)

4. dato che il primo coefficiente e' `!= 1`, moltiplichiamo di conseguenza

    ![](http://latex.codecogs.com/gif.latex?%5Cfrac%7B4%7D%7B3%7D%20%28%20%5Cfrac%7B3%7D%7B4%7D%20-%20%5Cfrac%7B9%7D%7B4%7Dz%5E%7B-1%7D%20-%20%5Cfrac%7B9%7D%7B4%7Dz%5E%7B-2%7D%20&plus;%20%5Cfrac%7B3%7D%7B8%7Dz%5E%7B-3%7D%20%29%20%3D%201%20-3z%5E%7B-1%7D%20-3z%5E%7B-2%7D%20&plus;%20z%5E%7B-3%7D)

5. a questo punto ripetiamo fino ad ottenere 4 `k`

    ![](http://latex.codecogs.com/gif.latex?k_4%20%3D%20-%5Cfrac%7B1%7D%7B2%7D%2C%20k_3%20%3D%20%5Cfrac%7B1%7D%7B2%7D%2C%20k_2%20%3D%20-2%2C%20k_1%20%3D%202)

6. infine disegniamo il diagramma a traliccio

    ![](images/lattice.png)

### Traliccio-scala
