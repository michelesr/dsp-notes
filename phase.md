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

## Il filtro ideale

Il filtro ideale è a fase lineare nella banda passante e a fase zero nella banda
interdetta, ha risposta di frequenza 1 nella banda passante e 0 nella banda
interdetta, ma non è ne stabile ne assolutamente sommabile, di conseguenza per
la realizzazione di filtri stabili si introduce una `banda di transizione` tra
la banda passante e quella interdetta in modo da consentire alla risposta in
frequenza di decadere graduatamente dal valore massimo a 0. 

## Il filtro a fase zero

Se non si opera in real time, le sequenze sono reali e finite, allora possiamo
realizzare un filtro a fase zero, ovvero un filtro con risposta in frequenza
rale e positiva. 

Tale filtro si ottiene elaborando x(n) con un sistema a coeficcienti reali H(z).
L'uscita di questo filtro viene invertita (time-reverse) e rifiltrata con lo
stesso filtro H(z), e infine si ribalta nuovamente il tempo.

Il sistema cosi' realizzato (filtro, time-reverse, filtro, time-reverse) è a
fase nulla.

Per applicare dunque un filtro con risposta di ampiezza A ci basta applicare il
metodo citato sopra con un filtro sqrt(A).
