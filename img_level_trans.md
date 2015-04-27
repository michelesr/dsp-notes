# Trasformazioni di intensità

Sono caratterizzate da una legge che mappa il valore di intensità dei pixel `r`
nel corrispondente valore `s`:

    s = T(r)

Lavorando con quantità digitali, i valori di una trasormazione di intensità
vengono memorizzati in un array monodimensionale e le mappature vengono
realizzate mediante tabelle (lookup table).

Fra le varie trasformazioni approfondiremo le sequenti:

- lineare
- logaritmica
- potenza

## Negativi

Il negativo di un immagine con livelli di intensità compresi tra `[0,L-1]` si
ottiene con la sequente legge:

    s(r) = L - 1 - r

L'elaborazione permette di migliorare i dettagli bianchi o grigi inseriti in
regioni scure di un'immagine.

## Trasformazioni logaritmiche

Hanno la seguente forma:

    s(r) = c log(1+r)

Dove `c` è una costante e `r >= 0`.

Questa trasformazione assegna a una gamma ristretta di valori a bassa intensità
un range più alto, mentre riduce la gamma di valori per i valori a intensità più
alta.

Il risultato è che i dettagli più scuri verranno resi più visibili a discapito
di quelli più chiari.

La trasformazione `esponenziale` realizza l'esatto contrario.

### Amplificazione dello spettro

La funzione `logaritmica` ha l'importante proprietà di comprimere la gamma
dinamica delle immagini che presentano ampie variazioni di valore dei pixel,
come ad esempio lo `spettro di Fourier` delle immagini.

## Trasformazioni di potenza (gamma)

Le trasformazioni di potenza hanno la forma base:

    # g è gamma
    s = cr^g

con `c` e `g` costanti positive.

Le curve di potenza con valori `frazionali` di `g` espandono i livelli scuri
comprimendo quelli chiari.

Con `g > 1` i valori chiari vengono amplificati a discapito di quelli scuri.

Molti strumenti usati per catturare le immagini producono un segnale che
risponde in base a una legge di potenza.

Il procedimento in uso per correggere questi fenomeni di riposta  vengono detti
`gamma correction`.

## Funzioni lineari a tratti

Le funzioni lineari a tratti si utilizzano per quello che viene definito
`strecthing del contrasto` (ovvero `espansione del contrasto`).

La forma di queste funzioni può essere arbitrariamente complessa.

Lo strecthing del contrasto ampia la gamma dei livelli di intensità di un
immagine in modo da visualizzare l'intera gamma di valori dello strumento di
registrazione o visualizzazione.
