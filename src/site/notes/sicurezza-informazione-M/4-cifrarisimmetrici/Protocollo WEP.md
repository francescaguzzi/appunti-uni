---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/protocollo-wep/"}
---

#protocollo 

Questo protocollo, ormai deprecato, veniva usato nelle **reti wireless** per fornire protezione dei dati cercando al contempo di ottenere un protocollo sufficientemente leggero che potesse essere implementato su una grande varietà di sistemi differenti nelle caratteristiche ed implementa un [[sicurezza-informazione-M/4-cifrarisimmetrici/Cifrari a flusso#Cifrari a flusso sincroni\|cifrario a flusso sincrono (RC4)]].

Step dell'algoritmo:
1. Il WEP si basa su **una chiave precedentemente condivisa concatenata ad un vettore di inizializzazione di 24 bit, i quali vengono usati come seed del [[sicurezza-informazione-M/2-hash-PRNG/Random Number Generator (RNG)#Pseudo Random Number Generator (PRNG)\|PRNG]] per la generazione del flusso di chiave**
2. Viene inviato l’IV in chiaro assieme al testo cifrato, il quale verrà usato a destinazione per reimpostare il PRNG.

![wep2.png](/img/user/sicurezza-informazione-M/immagini/wep2.png)

Il WEP ***non risulta per nulla robusto***, perchè:
- **non è possibile utilizzare una chiave diversa per ogni frame** -> la chiave si lascia inalterata e per i frame successivi il vettore di inizializzazione viene incrementato di 1
- L'IV è di 24 bit e permette di creare $2^{24}$ seed distinti -> [[sicurezza-informazione-M/4-cifrarisimmetrici/Attacco a 2-time keys\|Attacco a 2-time keys]]
- **semplicità della cifratura** -> essendo solo uno XOR, è facile per un attaccante dedurre informazioni sui messaggi in chiaro
- spesso i dispositivi **operavano un reset dell'IV ad ogni spegnimento** -> facile capirne il valore

 ![wep1.png](/img/user/sicurezza-informazione-M/immagini/wep1.png)