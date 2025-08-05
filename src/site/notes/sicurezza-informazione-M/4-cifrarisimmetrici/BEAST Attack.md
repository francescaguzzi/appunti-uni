---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/beast-attack/"}
---

#attacchi 

## Browser Exploit Against SSL TLS

Il BEAST attack è un **attacco attivo al protocollo SSL/TLS 1.0**. Esso può essere eseguito soltanto se il protocollo è stato configurato per usare [[sicurezza-informazione-M/4-cifrarisimmetrici/CBC (Cipher Block Chaining)\|CBC (Cipher Block Chaining)]] con un vettore di inizializzazione negoziato tra le parti **prima dello scambio dei dati e prevedibile**.

Sostanzialmente, consiste in un attacco di tipo **man-in-the-middle** -> l'intrusore effettua un attacco con *testo in chiaro scelto*, sfruttando la proprietà di [[sicurezza-informazione-M/4-cifrarisimmetrici/Attacco di malleabilità\|malleabilità dello XOR]]. 

-> Quando ci si connette a un sito web tramite HTTPS, il browser web e il server negoziano uno schema di crittografia e una chiave da utilizzare per la sessione. Il processo di negoziazione è protetto dalla crittografia asimmetrica, ma la comunicazione vera e propria è crittografata con algoritmi simmetrici molto più veloci, di solito cifrari a blocchi come AES

Il **primo blocco**, in modalità **CBC**, viene **combinato con un vettore di inizializzazione (IV)**, ovvero un blocco di dati casuale che rende unico ogni messaggio. La sicurezza di qualsiasi cifrario a blocchi in modalità CBC <u>dipende interamente dalla casualità degli IV</u>.

In **TLS 1.0, i vettori di inizializzazione non erano generati casualmente**. Invece di generare un nuovo IV per ogni messaggio, il protocollo *utilizza l'ultimo blocco di testo cifrato del messaggio precedente come nuovo IV*. Questo è una grave vulnerabilità, perché chiunque intercetti i dati cifrati ottiene anche gli IV. 

Infatti, i blocchi vengono combinati mediante XOR, che è un'**operazione reversibile**; quindi, conoscere gli IV potrebbe consentire a un aggressore di scoprire informazioni dai messaggi crittografati.

Se l'attaccante conosce il tipo di dati inviati e la loro posizione nel messaggio, **può iniettare un blocco di dati appositamente creato e verificare se il blocco crittografato risultante è lo stesso del blocco corrispondente nel flusso di messaggi effettivo tramite un attacco “chosen plaintext”** -> se l'attaccante indovina un probabile blocco di dati e fa lo XOR con il IV e il blocco di testo cifrato precedentemente, può iniettare ciò che vuole nella sessione. 







