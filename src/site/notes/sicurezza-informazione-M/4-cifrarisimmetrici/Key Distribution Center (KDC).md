---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/key-distribution-center-kdc/"}
---

#gestionechiavi 

Il KDC è un sistema il cui scopo è quello di andare a scambiare chiavi. **Non risolve completamente il problema della scalabilità ma lo migliora**, infatti, l’obiettivo è quello di avere N utenti e di avere solamente N chiavi (al contrario dell’architettura Master Key), ovvero una per ogni utente. 

Per realizzare questo modello c’è la necessità di introdurre **una terza parte chiamata “Key Distribution Center” (KDC)**.

Il sistema, a grandi linee, funziona come segue:
- Si assume che le entità A e B abbiano condiviso con T (entità fidata del KDC) le proprie Master Key $K_A$ e $K_B$ in modo che non possano essere indovinate, dedotte o intercettate
- Se A vuole comunicare con B in forma cifrata, dovrà inviare a T la richiesta per ricevere una chiave single-use di sessione $k$
- T genererà la chiave e la distriburà in maniera sicura ad A
- A quindi metterà anche B in condizione di conoscere quella chiave che entrambi useranno per cifrare e decifrare i messaggi che si scambiano

Più nel dettaglio:

1. ALICE -> T : $R_A \ ||\  A\  ||\  B$ 
		$R_a$ numero random per evitare *replay attack*
		
2. T -> ALICE : $E_{K_A}(R_A \ || \ B \ || \ E_{k_B}(A \ || \ k))$ 

3. ALICE -> BOB : $E_{K_B}(A \ || \ k)$
		A da a B la chiave per comunicare
		
	-> qui un INTRUSO potrebbe fare replay attack se conosce k almeno parzialmente, può sostituire A
		-> possibile soluzione: B salva la $k$ già usata in precedenza
		-> KDC comunque attribuisce un **tempo di vita limitato** alle chiavi di sessione
		
4. BOB -> ALICE : $E_K (R_B)$ 
		B sfida A per assicurarsi che sia fidato

5. ALICE -> BOB : $E_K(R_B -1)$ 
		A che conosce $k$ decifra il messaggio e ne dà conferma a B 

Lo schema di implementazione di questo centro di distribuzione delle chiavi, così com’è, <u>non è vulnerabile a livello di riservatezza</u>, ciò è vero se:
- il database in cui T custodisce le master key è assolutamente protetto 
- $K_A$, $K_B$, $R_A$, $R_B$ e la chiave di sessione $k$ devono essere assolutamente **casuali, imprevedibili e indeducibili**


A <u>livello di integrità, un intrusore è sempre in grado di modificare i messaggi</u> -> problema del punto 3

![KDC.png](/img/user/sicurezza-informazione-M/immagini/KDC.png)