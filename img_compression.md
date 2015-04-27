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

### Decodifica

Il processo di codifica consiste nella `decodifica` e `inverse mapping`, dato che il processo di quantizzazione è `irreversibile`.

## Algoritmi di compressione

### Codifica di Huffman

La codifica di Huffman costruisce il codice con la minor lunghezza possibile.

I passi per implementarlo sono:

- si visitano tutti i pixel
- si ordinano le intensità in base alla frequenza
- si uniscono i due valori con le frequenze minori
- si ripete il procedimento fino ad ottenere 2 simboli

Per un insieme di 6 valori avremo una situazione del tipo:

    1 è un simbolo, 0 è un insieme di simboli
    00 è un simbolo, 01 è un insieme di simboli
    011 è un simbolo, 010 un insieme di simboli
    0100 è un simbolo, 0101 un insieme di simboli
    01011 è un simbolo, 01010 è l'ultimo simbolo

Quindi avremo due serie di simboli:

    # simboli della codifica ordinati per frequenza
    [1, 00, 011, 0100, 01011, 01010]

    # simboli non usati nella codifica
    [0, 01, 010, 0101]

Notare come i `prefissi` son tutti diversi, in questo modo si determina in
maniera immediata la fine della parola e l'inizio della successiva.

Questo tipo di codifica si usa anche nei formati
`jpeg`,`mpeg`,`mp3`,`zip`,`rar`.

### Codifica RLE (Run-Lenght)

In questa codifica si definiscono coppie di valore e lunghezza, ovvero si codifica il valore del primo pixel e il numero di volte che questo valore si ripete consecutivamente.

Questo tipo di codifica è molto efficace quando abbiamo ad esempio zone di intensità costante (come ad esempio il cielo in un punto dove non ci sono variazioni di intensità, o l'erba del prato, ecc...). 

La codifica `RLE` viene utilizzata anche nei formati `JPEG` e `BMP`

#### RLE nel formato BMP

Nel formato `BMP` i dati possono essere rappresentati in due modi diversi:

- codificati
- assoluti

Entrambe le modalità possono essere presenti nella stessa immmagine.

#### BMP a dati codificati

Viene utilizzata una rappresentazione `RLE` a 2 `byte`. Il primo `byte`
individua il numero di pixel consecutivi che hanno lo stesso valore, che è
descritto nel secondo `byte`.

Quindi con il secondo byte è possibile descrivere fino a 256 valori (che di
solito rappresentano l'intensità o i colori).

#### BMP a dati assoluti

Il primo byte vale sempre `0`, mentre il secondo `byte` può assumere i seguenti
valori:

- `0`, `fine della linea`
- `1`, `EOF`
- `2`, i `byte` successivi contengono gli `indirizzi relativi` (orrizzontali e
  verticali), a una nuova posizione spaziale dell'immagine
- `3-255`, determina il numero di pixel successivi non compressi con RLE, e nei
  `byte` successivi troviamo l'indice del colore dei pixel.

### Codifica per piani di bit

TODO

### Codifica a blocchi mediante trasformata

Si tratta di una tecnica di compressione che divide l'immagine in piccoli
blocchi non sovrapposti ed elabora i blocchi utilizzando una `fft` `2d`.

Il decoder esegue quindi le seguenti operazioni:

- costruzione delle sottoimmagini
- trasformazione
- quantizzazione
- codifica

Il decoder esegue dunque le operazioni inverse (tranne per la quantizzazione che
non è `invertibile`).

Tra le possibili trasformate possiamo scegliere:

- `DFT`
- `DCT` (`Discrete Cosine Transorm`)
- `WFT` (`Walsh-Hadamard Fourier Transform`)

