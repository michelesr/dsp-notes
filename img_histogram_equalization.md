# Equalizzazione di istogrammi

L'obiettivo dell'equalizzazione consiste nell'ottenere un'immagine in cui le componenti di colore siano ben bilanciate e spalmate lungo tutto lo spazio colore disponibile.  Questo serve a massimizzare complessivamente il contrasto.

Per far questo dobbiamo applicare una trasformazione `T` in cui andiamo a lavorare sui singoli pixel di un'immagine.  `T` dev'essere una funziona monotona non decrescente (per evitare artefatti dovuti ad inversioni di intensita') che trasforma un'intensita' di un pixel da un range `[0, L-1]` ad un altro pixel sempre con range `[0, L-1]`.
