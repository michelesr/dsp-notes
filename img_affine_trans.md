# Trasformazioni affini

Per **trasformazione affine** s'intende una manipolazione dell'immagine che ha lo
scopo di modificare la *posizione* dei pixel.

Consistono principalmente in due passi:

- *trasformazione spaziale* delle *coordinate*
- *interpolazione* delle *intensità* dei pixel

Alcuni tipi di *trasformazioni* più usate sono:

- rotazione
- traslazione
- ingrandimento
- scalatura
- inclinazione

## Trasformazione spaziale

### Matrice di trasformazione

L'operazione di trasformazione affine consiste nel [moltiplicare riga per colonna](http://www.youmath.it/lezioni/algebra-lineare/matrici-e-vettori/1567-prodotto-riga-per-colonna.html)
il *vettore delle coordinate* con la *matrice di trasformazione*.

Ad esempio per *ridimensionare* l'immagine:

![Scale-Matrix](http://latex.codecogs.com/gif.latex?%5Bx%2Cy%2C1%5D%20%5Cbegin%7Bbmatrix%7D%20c_x%20%26%200%20%26%200%20%5C%5C%200%20%26%20c_y%20%26%200%20%5C%5C%200%20%26%200%20%26%201%20%5Cend%7Bbmatrix%7D%20%3D%20%5BC_x%20x%2C%20C_yy%2C%201%5D)

Questa immagine offre una panoramica di alcune possibili *trasformazioni*:

![Affine-Matrix](https://upload.wikimedia.org/wikipedia/commons/2/2c/2D_affine_transformation_matrix.svg)

Esistono due approcci per l'applicazione delle trasformate:

- [forward mapping](img_affine_trans.md#forward-mapping)
- [inverse mapping](img_affine_trans.md#inverse-mapping)

### Forward mapping

Si visitano i pixel dell'immagine di input e si calcolano i pixel corrispondenti
nell'immmagine di output.

Il problema di questo approccio risiede nel fatto che se più pixel possono essere
assegnati alla stessa posizione nell'immagine di output, oppure non essere
assegnati affatto.

### Inverse mapping

Questo approccio risulta più efficace, in quanto visita le posizioni dei pixel
di output e ricava tramite operazione inversa la posizione del pixel
nell'immagine di input.

## Interpolazione 

I valori di intensità dei pixel vengono calcolati tramite interpolazione considerando i pixel più vicini.
