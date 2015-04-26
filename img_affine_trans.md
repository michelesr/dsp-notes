# Trasformazioni affini

Per `trasformazione affine` si intende una manipolazione dell'immagine che ha lo
scopo di modificare la posizione dei pixel.

Consistono principalmente in due passi:

- trasformazione spaziale delle coordinate
- interpolazione delle intensità dei pixel

Alcuni tipi di trasformazioni più usate solo:

- rotazione
- traslazione
- ingrandimento
- scalatura
- inclinazione

## Trasformazione spaziale

### Matrice di trasformazione

L'operazione di trasformazione affine consiste nel moltiplicare riga per colonna
la matrice di trasformazione con la funzione che definisce l'immagine:

![Affine-Matrix](https://en.wikipedia.org/wiki/File:2D_affine_transformation_matrix.svg)

Esistono due approcci per l'applicazione delle trasformate:

- forward mapping
- inverse mapping

### Forward mapping

Si visitano i pixel dell'immagine di input e si calcolano i pixel corrispondenti
nell'immmagine di output.

Il problema di questo approccio sta nel fatto che se più pixel possono essere
assegnati alla stessa posizione nell'immagine di output, oppure non essere
assegnati affatto.

### Inverse mapping

Questo approccio risulta più efficace, in quanto visita le posizioni dei pixel
di output e ricava tramite operazione inversa la posizione del pixel
nell'immagine di input.

## Interpolazione 

I valori di intensità dei pixel vengono calcolati tramite interpolazione considerando i pixel più vicini.
