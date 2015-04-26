# Compressione delle immagini

L'obiettivo della `compressione` è quello di ridurre la quantità di dati necessari alla rappresentazione dell'informazione contenuta nell'immagine. 

I `dati` rappresentano l'`informazione`, e diverse quantità di dati possono essere utilizzate per rappresentare la stessa `informazione`.

## Ridondanza della codifica

Un `codice` è un insieme di `simboli` (`bit`, `cifre`, `lettere`) usati rappresentare un insieme di `eventi` o una certa quantità di informazione.

Ad ogni `evento` o `informazione` viene associato una particolare parola del codice (`codeword`). 

Il `numero di simboli` di una `codeword` viene detto `lunghezza`.

Per ridurre la quantità di dati necessari alla rappresentazione possiamo definire `codici` a lunghezza inferiore.

### Codice naturale

In un codice `naturale` tutti i possibili eventi o valori vengono presi in considerazione e codificati con una `codeword`.

Con `n` `eventi` avremo un numero di bit necessari pari a `log2(n)`.

La scelta di un codice `naturale` non risulta ottimale in quanto non tiene conto delle `probabilità` che hanno i vari `valori` di presentarsi (e quindi della [ddp](https://it.wikipedia.org/wiki/Distribuzione_di_probabilit%C3%A0))

### Codice a lunghezza variabile

Un bel trucco per ridurre la `lunghezza del codice` consiste nel definire un `codice a lunghezza variabile` dove le parole hanno una lunghezza proporzionale alla probabilità di presentarsi dell'evento o valore a cui si riferiscono.

## Ridondanza spaziale e temporale

Dato che spesso molti `pixel` hanno valori `correlati` tra di loro, abbiamo un inutile `replicazione` del valore e quindi una `ridondanza` di valori tra i pixel correlati `spazialmente`.

### Codifica RLE (Run-Lenght)

In questa codifica si definiscono coppie di valore e lunghezza, ovvero si codifica il valore del primo pixel e il numero di volte che questo valore si ripete consecutivamente.

Questo tipo di codifica è molto efficace quando abbiamo ad esempio zone di intensità costante (come ad esempio il cielo in un punto dove non ci sono variazioni di intensità, o l'erba del prato, ecc...). 

Si parla di processo `reversibile` quando è possibile risalire all'informazione originale (compressione `lossless`), mentre si parla di processo `irreversibile` quando la codifica introduce una perdita di informazione (compressione `lossy`).

## Informazione irrilevante

La maggior parte delle `matrici di intensità 2D` contengono `informazioni` ignorate dal `sistema visivo umano` (oppure addirittura `estranee` all'utilizzo dell'immagine). L'`informazione` risulta non necessaria in quanto non `fruibile`.

Per esempio se abbiamo una zona con un livello di grigio con piccole variazioni, il sistema visivo umano le percepisce uguali e quindi possiamo codificarle con il valore medio (sfruttando magari la codifica RLE).

Il processo di ridurre un range di valore in un range minore viene detto `quantizzazione` ed è `irreversibile`.

### Teoria dell'informazione

La teoria dell'informazione stabilisce che l'informazione contenutà in un evento è determinata da:

![Information-Theory](http://latex.codecogs.com/gif.latex?I%28E%29%20%3D%20%5Clog%28P%28E%29%5E%7B-1%7D%29%20%3D%20-%5Clog%28P%28E%29%29)

La base del logaritmo determina l'unità di informazione.

#### Esempio

Un evento di probabilità `1/2`, come il lancio di una moneta, porta un'informazione binaria.

    -log2(1/2) = log2(2) = 1

## Modelli di compressione di un'immagine

Un `sistema` per la `compressione` delle `immagini` è formato da due distinte `componenti`:

- `encoder`
- `decoder`

L'`encoder` esegue la `compressione` e il `decoder` la `decompressione`.

Entrambe le operazioni possono essere eseguite da `software` o da un misto di `hardware` e `firmware` (come nel caso dei lettori `DVD`).

Per `codec` si intende un oggetto `hardware` o `software` in grado di eseguire entrambe le operazioni di `codifica` e `decodifica`.

### Tipi di compressione

Suddividiamo le compressioni in:

- `lossless`, o `error free`, o `information preserving`
- `lossy`

a seconda della possibilità che la compressione offre di ricostruire il segnale originale senza perdita di informazioni.

## Processo di codifica

Il `codificatore` procede alla `codifica` rimuovendo le `ridondanze` attraverso `3` operazioni `indipendenti`:

- mapping
- quantizzazione
- codifica

### Mapper

Riduce la ridondanza spaziale e temporale. Questa operazione è `reversibile`.

Un esempio è la codifica `RLE`.

### Quantizzazione

Viene ridotta l'accuratezza della rappresentazione secondo criteri di fedeltà prestabiliti con l'obiettivo di eliminare informazione irrilevante.

### Codifica dei simboli

Viene infine scelto un `codice`, spesso a [lunghezza variabile](https://en.wikipedia.org/wiki/Variable-length_code) per rappresentare i valori.

## Processo di decodifica

Il processo di codifica consiste nella `decodifica` e `inverse mapping`, dato che il processo di quantizzazione è `irreversibile`.

