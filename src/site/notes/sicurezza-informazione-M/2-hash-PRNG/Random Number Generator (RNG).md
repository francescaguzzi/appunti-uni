---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/random-number-generator-rng/"}
---

#definizione #highpriority #algoritmo 

> ***Si definisce Random Number Generator (RNG) un sistema che permette di produrre 0 o 1 con la stessa probabilità e senza correlazione tra bit diversi.***

-> **Indipendenza statistica**
-> **Valori equiprobabili**

Per verificare queste proprietà, sono stati progettati diversi algoritmi ormai diventati standard che determinano se una sequenza di bit è casuale: 
- **Monobit** -> va a verificare che il numero di 1 sia circa uguale a quello degli 0
- **Poker** ->  la stringa viene suddivisa in sequenze di M bit e si valuta se ognuna di queste configurazioni sia equiprobabile -> check se le $2^M$ configurazioni compaiono lo stesso numero di volte 
- **Run** -> verifica la presenza di lunghe sequenze di bit consecutivi identici (ovvero che sono tutti 0 oppure tutti 1) nei numeri generati -> presenza di *pattern* 
	- Tutti 1 = *block*
	- Tutti 0 = *gap* 
- **Long run** -> valutazione del block con più 1 
Ci sono poi altri test come autocorrelazione, trasformazione discreta di Fourier o imprevedibilità verificata tramite *next-bit test*
# True Random Number Generator (TRNG)
#definizione 
Questa implementazione di RNG genera il valore casuale tramite la **digitalizzazione di un fenomeno fisico casuale** (tempo medio di emissione di particelle durante il decadimento radioattivo, via software tramite estrazione di rumori di funzionamento del computer, turbolenza di fluidi, ecc...) garantendo quindi una reale casualità dei valori. 
Nella crittografia moderna i TRNG vengono utilizzati in tutti i componenti crittografici che richiedono un **seed iniziale casuale**, imprevedibile e indeducibile oppure una chiave segreta che necessariamente deve essere generata in modo da essere casuale, imprevedibile e indeducibile -> funzioni di Encryption

***Svantaggi***:
- **Bassa frequenza di generazione dei valori** -> dipendono da fenomeni fisici che vanno elaborati
- **Non è in grado di riprodurre un certo valore**, ad esempio dall'altro lato della comunicazione
# Pseudo Random Number Generator (PRNG)
#definizione 
**Questa implementazione di RNG utilizza algoritmi deterministici per generare il valore casuale, di conseguenza non garantisce la reale casualità dei valori. I valori generati si ripetono ciclicamente con un periodo di lunghezza variabile a seconda delle implementazioni, maggiore è la lunghezza del periodo maggiore è l’apparente casualità dei valori.** 

Per molti PRNG la generazione dei valori parte da un valore iniziale detto seme (*seed*). Se il seed risulta noto è possibile riprodurre la medesima sequenza di valori ogni volta, pertanto è importante che esso sia scelto in maniera realmente casuale, ad esempio mediante un TRNG. 

-> **La sequenza in uscita prima o poi si ripete** -> periodicità, meno sequenze possibili e valore in uscita **prevedibile** -> _la riproducibilità lo rende inadatto a produrre chiavi_
### Pseudo Random Number Generator Cryptographically Secure (PRNGCS)
#definizione 
I PRNG crittograficamente sicuri sono modellati sulla base di un **automa a stati finiti** avente un registro di stato e due funzioni (delle quali almeno una deve essere [[sicurezza-informazione-M/2-hash-PRNG/Trasformazioni#Unidirezionali (one-way functions)\|unidirezionale]]):
- Funzione di uscita $F$
- Funzione di calcolo di stato futuro $G$
Questo tipo di generatore **deve garantire 3 proprietà** per essere chiamato tale:
1. **Casualità dei bit di uscita** -> si sottopone l'uscita ad una serie di test statistici
2. **Imprevedibilità dei bit di uscita** -> deve superare il ***next-bit test*** 
		Esso valuta, dati $L$ bit della stringa di uscita, se esiste o meno un [[sicurezza-informazione-M/2-hash-PRNG/Complessità computazionale#^bb115d\|algoritmo polinomiale]] in grado di predire il bit successivo $(L+1)$ della stessa con probabilità maggiore del 50%
3. **Indeducibilità del seed** -> deve essere computazionalmente infattibile per un intruso riuscire a risalire ai bit precedenti fino al seed iniziale
		Garantita dall'uso della <u>funzione unidirezionale</u> al posto delle funzioni $F$ o $G$ dell'automa a stati finiti