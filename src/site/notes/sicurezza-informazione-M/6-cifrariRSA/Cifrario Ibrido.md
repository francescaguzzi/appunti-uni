---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/cifrario-ibrido/"}
---

#modalitàcifratura 

Nello schema ibrido **si adotta un cifrario simmetrico, ma la chiave condivisa tra mittente e destinatario viene concordata ad esempio tramite [[sicurezza-informazione-M/4-cifrarisimmetrici/Protocollo Diffie-Hellman\|Diffie-Hellman]] o scambiata tramite crittografia a chiave pubblica**. L'efficienza ottenuta è pari a quella di un cifrario simmetrico.

In generale:
1. Ogni volta che il mittente apre una nuova sessione **viene generata una chiave simmetrica di sessione** che **viene crittata con la chiave pubblica del destinatario e poi spedita assieme al messaggio**
2. Il destinatario **decritta la chiave di sessione attraverso la sua chiave privata (asimmetrica)**
3. Infine usa la chiave di sessione simmetrica per decodificare il messaggio 

> **Le chiavi di sessione sono simmetriche ma allo scambio iniziale vengono crittate e decrittate asimmetricamente**

![cifrarioibrido.png](/img/user/sicurezza-informazione-M/immagini/cifrarioibrido.png)

Il vantaggio di questo sistema è che unisce la comodità nella gestione delle chiavi del sistema asimmetrico alla velocità propria di quello simmetrico.

Tuttavia, l'invio di $E_{p_B}(k)$ è **rischioso nel caso di k troppo piccole** -> la chiave pubblica $P_B$ è nota e si potrebbe usare forza bruta sui valori di $k$

Se le dimensioni di $k$ sono ridotte (<128 bit) occorre inserire del [[sicurezza-informazione-M/6-cifrariRSA/Padding OAEP\|Padding OAEP]].