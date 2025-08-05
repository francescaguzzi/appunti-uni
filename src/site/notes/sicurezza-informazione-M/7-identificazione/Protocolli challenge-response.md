---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/7-identificazione/protocolli-challenge-response/"}
---

#identificazione #protocollo 

L’identificatore sfida l’identificando, la cui risposta si basa sulla conoscenza di un segreto $s$ precedentemente concordato -> si assume che l'identificatore si comporti correttamente. 

Questi schemi possono essere basati su: 
- **Trasformazione E e D** -> il verifier genera un numero casuale, lo cifra e sfida il prover a mandare indietro il risultato corretto
- **Trasformazioni S e V** -> il verifier sfida il prover a *firmare un numero casuale* e mandare indietro il risultato, che verrà controllato con la funzione di verifica -> tipo [[sicurezza-informazione-M/6-cifrariRSA/Identificazione attiva con firma\|Identificazione attiva con firma]]

Nel caso del primo schema, il protocollo può essere del tipo:

1. $B \to A : R_B$
2. $A \to B : R_A \ || \ H(R_B \ || \ S)$
3. $B \to A: H(R_A \ || \ S)$

## Vulnerabilità

Dal momento che il messaggio di risposta ad ogni sfida è simmetrico, nel senso che presenta sempre la stessa struttura, con il <u>numero random della sfida concatenato con il segreto</u>, questo protocollo è vulnerabile ai seguenti attacchi:

- ***Interleaving ([[sicurezza-informazione-M/6-cifrariRSA/Identificazione attiva con firma#^cda3e1\|chessmaster]])*** 
- ***Replica*** -> l'attaccante può fingersi un'altra entità usando informazioni raccolte 
- ***Reflection*** -> un attaccante C può aprire <u>in contemporanea due sessioni di identificazione con A</u>, fingendosi B e riproponendo nella seconda sessione la stessa sfida che A ha lanciato nella prima -> si può identificare
	- Soluzione -> **rompere la simmetria nelle comunicazioni** -> essenzialmente concatenando roba a caso

## Generazione di R

[[sicurezza-informazione-M/2-hash-PRNG/Random Number Generator (RNG)\|Random Number Generator (RNG)]]

Affinchè $R_B$ sia valido per l'identificazione, bisogna considerare come viene generato:

- **TRNG** -> lo si esclude, considerando la bassa e incostante frequenza di generazione

- **PRNG casuale** -> lo si esclude perchè un **requisito fondamentale per la robustezza** del protocollo è l'***imprevedibilità del nonce***, non garantita se il PRNG non è crittograficamente sicuro

- **PRNG crittograficamente sicuro** -> soluzione corretta se usato con un periodo molto lungo per <u>evitare ripetibilità</u> 