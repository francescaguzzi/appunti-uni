---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/ofb-output-feedback/"}
---

#modalitàcifratura #algoritmo 

La modalità OFB ricorda un [[sicurezza-informazione-M/4-cifrarisimmetrici/Cifrari a flusso#Cifrari a flusso sincroni\|cifrario a flusso sincrono]]. Essa è simile alla [[sicurezza-informazione-M/4-cifrarisimmetrici/CFB (Cipher Feedback)\|CFB (Cipher Feedback)]]: anche qui sono presenti **due shift register di dimensione `N`** e si vanno a cifrare un numero **`n << N`** bit alla volta, dove `n` rappresenta la dimensione del blocco. Anche qui deve essere precondivisa una chiave $k$ ed un vettore di inizializzazione IV. 

La differenza dal CFB è che **la retroazione non è del messaggio cifrato ma degli `n` bit più significativi del flusso di chiave** -> risulta quindi più resistente alla propagazione degli errori. 

| **PRO**                                                                                                                                                                               | **CONTRO**                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Stessi pro del CFB                                                                                                                                                                    | Stessi contro di CFB, senza il problema di propagazione dell'errore |
| **Resistente alla propagazione degli errori nel cifrato** -> sola retroazione del **flusso di chiave**                                                                                |                                                                     |
| La <u>modifica</u> di un bit del cifrato impatta solo la decodifica di quel bit, non tutto il flusso di dati -> per questo motivo **più indicata nei canali rumorosi** rispetto a CFB |                                                                     |
| La <u>cancellazione o l'iniezione</u> di un bit nel cifrato provocano invece **perdita di sincronismo definitiva**                                                                    |                                                                     |
Viene usato solitamente per la **trasmissione di caratteri mediante flusso di dati** attraverso **canali rumorosi**.

![OFB.png](/img/user/sicurezza-informazione-M/immagini/OFB.png)