---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/identificazione-attiva-con-firma/"}
---

#identificazione #protocollo 

---
## Identificazione unilaterale 

 Questo protocollo permette a un'entità A (il prover) di dimostrare la propria identità a un'entità B (il verifier) utilizzando una firma digitale.

1. $B \to A : RB$
	- RB = *nonce* -> *number used once* -> garantisce **freshness**, cioè che la risposta di A sia generata al momento e non riutilizzata
	
2. $A \to B : c = S_{SA}(RB)$ 
	- A dimostra di essere in possesso della sua chiave privata SA e firma il nonce di B
	
3. $V_{PA}(c) = RB$ 
	- B verifica la firma usando la <u>chiave pubblica</u> di PA di A

Il protocollo è semplice, ma tuttavia suscettibile ad alcune tipologie di attacchi:
-   ***Attacchi con testo scelto*** -> chiunque può inviare ad A un messaggio sensato e farselo firmare 
	- Contromisura -> modificare il messaggio del punto (2) così che diventi casuale e non riutilizzabile $$ A \to B \ : \ R_A \ || \ S_{SA}(R_A \ || \ R_B)$$
- ***Attacchi man-in-the-middle*** -> sufficiente allegare alla risposta (2) il <u>certificato associato alla propria chiave pubblica</u> $$ A \to B : \text{cert}(P_A,T) \ ||\ R_A \  || \ S_{SA}(R_A \ || \ R_B)$$ 
- ***Attacchi "gran maestro degli scacchi"*** -> è tipo un attacco man-in-the-middle in cui l'intruso si inserisce in un protocollo di autenticazione facendo credere sia ad A che a B di comunicare direttamente tra di loro, mentre in realtà lui controlla il flusso dei messaggi 
{ #cda3e1}

	- Contromisura -> allegare una [[sicurezza-informazione-M/8-sicurezzadistribuita/TSS (Time Stamping Service)\|marca temporale]] T e l'identificatore del richiedente autenticazione nel punto (2) $$ A \to B : \text{cert}(P_A,T) \ ||\ R_A \ ||\ B \ || \ S_{SA}(R_A \ || \ R_B \ || B)$$

---
## Mutua identificazione

Per quanto riguarda l’identificazione mutua è possibile apportare alcune modifiche al protocollo precedente facendolo divenire:

1. $B \to A : \tau B1$
2. $A \to B : \text{cert}(PA,T) \ || \ \tau A \ || \ B \ || \ S_{SA}(\tau A \ || \ \tau B_1 \ || \ B )$ 
3. $B \to A : \text{cert}(PB, T') \ || \ \tau B2 \ || \ S_{SB}(\tau B2 \ || \ \tau A \  || \ A)$ 

---

