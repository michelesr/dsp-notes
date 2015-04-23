# Fase

## Ritardo di fase e di gruppo

Tutte le componenti di frequenza di un segnale sono ritardate durante il
passaggio attraverso un sistema quale filtro, amplificatore o altoparlante.

Il ritardo del segnale sarà differente per ogni frequenza a meno che il
sistema sia a fase lineare (e quindi il ritardo di gruppo sia costante).

Il ritardo di fase che subiscono le singole componenti è: 

![Phase_Delay](http://latex.codecogs.com/gif.latex?tp%28%5Comega%29%20%3D%20-%20%5Cfrac%7B%5CTheta%28%5Comega%29%7D%7B%5Comega%7D)

Il ritardo di gruppo ha la seguente forma: 

![Group_Delay](http://latex.codecogs.com/gif.latex?tg%28%5Comega%29%20%3D%20-%20%5Cfrac%7Bd%5CTheta%28%5Comega%29%7D%7Bd%5Comega%7D)

### Fase lineare

La fase lineare è una proprietà del filtro, che si verifica quando la risposta
di fase è una funzione lineare della frequenza. Il risultato è che tutte le
componenti in frequenza del segnale sono spostate nel tempo (ritardate di
solito) di valore costante, che viene chiamato ritardo di fase.

In un sistema a fase lineare non ci sono distorsioni di fase dovute al ritardo
relativo tra le varie frequenze (dato che son ritardate tutte allo stesso modo).

Per sistemi a tempo discreto, la fase lineare perfetta si ottiene tramite
l'utilizzo di filtri a risposta impulsiva finita (`FIR`).

### Fase minima

Un sistema lineare e tempo invariante (`LTI`) viene detto a `fase minima` se il
sistema e il suo inverso sono `casuali` e `stabili`.

Per esempio, un sistema con funzione di trasferimento `H(z)` soddisfa causalità
e stabilità sse tutti i `poli` stanno all'interno del circolo di raggio
unitario.
