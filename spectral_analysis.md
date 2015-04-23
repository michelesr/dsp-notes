# Analisi spettrale

## Introduzione da Wikipedia

Spesso risulta utile considerare lo spettro di una porzione finita del
segnale, risulta quindi comodo applicare una funzione finestra al segnale
stesso.

Un esempio di funzione finestra:

    RectangularWindow(n) : 1 if n in [a,b], 0 otherwise  

La finestra ci permette di considerare il segnale solo nel range che
desideriamo.

Prendiamo come esempio la funzione cos(ωt). Per definizione il suo spettro
dovrebbe essere 0 per frequenze diverse da ω. Se andiamo ad applicare una
finestra rettangolare lo spettro della sinusoide non appare più come un impulso
unitario in ω, ma comprende delle frequenze con ampiezza diversa da 0, e in
particolare, le ampiezze saranno più accentuate vicino a ω, e comunque spalmate
in tutto lo spettro. Questo effetto  viene detto leakage spettrale.

![Leakage](https://upload.wikimedia.org/wikipedia/commons/f/f6/Spectral_leakage_from_a_sinusoid_and_rectangular_window.png)

Se le forme d'onda sotto analisi comprendono due sinusoidi, il leakage prodotto
dall'applicazione delle finestre può interferire con l'abilità di distinguere le
2 sinusoidi accuratamente. Infatti se le loro frequenze e ampiezze son diverse,
la sinusoide con ampiezza mimore potrebbe essere indistinguibile a causa del
leakage prodotto da quella con ampieza maggiore. Inoltre, se le sinuosidi hanno
ampiezza simile ma frequenze molto simili, il loro effetto leakage le renderà
indistinguibili.

La finestra rettangolare ha una risoluzione spettrale eccellente per sinusoidi
di forza comparabile, ma è una scelta povera per sinusoidi a diverse ampiezze.

[Spectral Analysis on Wikipedia] (https://en.wikipedia.org/wiki/Window_function#Spectral_analysis)
