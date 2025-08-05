---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/trasformazioni/"}
---

#lowpriority 

Per proteggere i dati in transito su un [[sicurezza-informazione-M/1-concettibase/Attacchi informatici#^288f9d\|canale insicuro]] occorre **utilizzare delle trasformazioni facenti uso di una codifica ridondante**, applicate sia **prima dell'invio dei dati** da parte del mittente sia nel momento in cui il **destinatario ha intenzione di leggere i dati**. 

I dati vengono quindi trasmessi con dei **bit in più** o con una modifica dei bit del messaggio, i quali dovranno essere rielaborati dalla destinazione -> **overhead**. 

Queste trasformazioni possono essere costituite da: **algoritmi** o **protocolli** che vanno a trasformare il dato -> la disciplina che studia questi algoritmi e protocolli è detta ***crittologia***: la crittologia ha come obiettivo quello di individuare **trasformazioni efficienti, efficaci e sicure** ed è formata da due discipline:
- [[sicurezza-informazione-M/3-cifrariclassici/Cifrari classici\|Cifrari classici]] -> scienza che si occupa di applicare trasformazioni ai dati per rendere la loro trasmissione sicura
- [[sicurezza-informazione-M/2-hash-PRNG/Crittoanalisi\|Crittoanalisi]] -> processo inverso alla crittografia, ne valuta robustezza esaminando come ed in quanto tempo è possibile rompere le difese
# Principi di difesa
Le trasformazioni devono seguire due principi:
- ***Trasformazioni segrete***
- ***Calcoli impossibili*** -> denotano una sicurezza perfetta, che rende impossibile acquisire un qualsiasi quantitativo di nuove informazioni dopo un'attenta analisi -> **impossibile nella pratica**
Per questo ci si accontenta della **sicurezza computazionale** -> elevata **difficoltà computazionale** -> spesso efficiente grazie anche alla scadenza del tempo di vita delle informazioni. 
# Tipi di trasformazioni
- Trasformazioni per garantire la [[sicurezza-informazione-M/1-concettibase/Riservatezza\|Riservatezza]]
	È sufficiente **trasformare la rappresentazione delle informazioni in modo da renderla incomprensibile a chiunque a parte i diretti interessati** 
	Dato un messaggio `m` si ottiene il messaggio cifrato `c` mediante la trasformazione `E`:
		$c = E(m), \ m = D(c)$
- Trasformazioni per garantire l'[[sicurezza-informazione-M/1-concettibase/Integrità\|Integrità]]
	Si creano delle contromisure per la rilevazione di **eventuali modifiche al contenuto del dato originale** -> al dato viene aggiunto un piccolo riassunto, chiamato *digest* che identifica l'informazione stessa 
		Il digest viene creato con una funzione hash crittograficamente sicura
- Trasformazioni per garantire l'[[sicurezza-informazione-M/1-concettibase/Autenticità\|Autenticità]]
	Il **destinatario deve riconoscere se il messaggio ricevuto proviene veramente dal mittente o meno** -> allegare al messaggio informazioni non imitabili
		Varie soluzioni, firme digitali oppure hash del messaggio e di un segreto
# Funzioni
## Unidirezionali (one-way functions)
>Una funzione è detta unidirezionale se è invertibile, facile da calcolare per ogni ingresso, ma difficile da invertire data l'immagine di un ingresso casuale. 

Deve risultare per un intruso **computazionalmente difficile** invertire funzioni hash, cifratura etc. 
## Pseudo unidirezionali (trapdoor one-way function)
> Una funzione f è detta pseudo-unidirezionale se appare come unidirezionale per chiunque non sia in possesso di una particolare informazione sulla sua costruzione.

Ciclo di vita delle [[sicurezza-informazione-M/2-hash-PRNG/Chiavi\|chiavi]] mantenuto e gestito in maniera sicura -> chiavi composte da n di bit molto grandi -> cardinalità elevata
# Trasformazioni segrete
Il metodo più sicuro consiste nell'utilizzo di una [[sicurezza-informazione-M/2-hash-PRNG/Chiavi\|chiave]] -> in questo modo l'unico modo per decifrare un testo senza conoscere ulteriori informazioni è un attacco di **forza bruta**, che però spesso necessita di un tempo di esecuzione superiore al tempo di vita dell'informazione.