---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/ctr-counter/"}
---

#modalitàcifratura #algoritmo 

Questa modalità sfrutta un **contatore** avente le **stesse dimensioni del blocco da cifrare** e **inizializzato tramite un seed generato casualmente**.

Si seguono i seguenti step:
1. Il **contatore** viene inizializzato mediante un seed generato casualmente
2. I bit contenuti all'interno del contatore vengono cifrati mediante una chiave $k$ **precondivisa** per ottenere una **chiave casuale**
3. Tale chiave appena ottenuta verrà messa in XOR con il valore del blocco
4. Una volta cifrato un blocco **il valore del contatore viene incrementato**
		In questo caso il valore di ogni blocco non dipende dai precedenti, ma solamente dal **seed iniziale**

La segretezza della chiave $k$ garantisce che solo mittente e destinatario possano leggere il messaggio e tipicamente *il seed viene trasmesso in chiaro in testa al messaggio*. 

In termini di **propagazione dell’errore**, **non essendoci retroazione del cifrato**, anche qui la modifica di un bit del cifrato impatta solo la decodifica di quel bit, e **non tutto il flusso di dati**. 

Questo tipo di cifrari viene usato solitamente per **trasmissioni di caratteri orientate al blocco**, e permette di ottenere la cifratura e decifrazione selettiva dei blocchi di testo. Implementa il modello di [[sicurezza-informazione-M/4-cifrarisimmetrici/Cifrari a flusso#Cifrari a flusso sincroni\|cifrario a flusso sincrono]].

| **PRO**                                                          | **CONTRO**                                                                                |
| ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Resistente alla propagazione degli errori nel cifrato**        | Cifratura e decifrazione usano la stessa funzione $E$ (non necessariamente cosa negativa) |
| **Non richiede aggiunta di padding**                             |                                                                                           |
| **Possibilità di parallelizzare** sia cifratura che decifrazione |                                                                                           |

![CTR.png](/img/user/sicurezza-informazione-M/immagini/CTR.png)