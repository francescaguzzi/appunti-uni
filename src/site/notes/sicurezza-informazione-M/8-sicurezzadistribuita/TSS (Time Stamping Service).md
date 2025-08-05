---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/8-sicurezzadistribuita/tss-time-stamping-service/"}
---

#protocollo #highpriority 

Nel mondo legale si presenta spesso la necessità di sapere quando un documento sia stato creato, inviato o, più in generale, di **associare ad un documento una marca temporale**.

La marcatura temporale risulta estremamente importante in quanto permette di **determinare il momento esatto in cui una certa azione è stata effettuata**. In particolare, risulta **fondamentale conoscere la marca temporale della [[sicurezza-informazione-M/6-cifrariRSA/Firma digitale\|firma digitale]]**, poiché essa permette di decidere se la firma vada considerata valida o meno sulla base dei dati ottenuti da una CA.

---
## Proprietà

Devono essere garantite le seguenti proprietà: 

1. **La marca non deve contenere un tempo falso** -> il tempo deve essere garantito da un ente fidato sulla base degli standard internazionali forniti dagli orologi atomici -> <mark style="background: #FF5582A6;">ente fidato</mark>

2. **La marca deve essere applicata ad uno specifico documento e deve individuare univocamente il documento, l’istante in cui è stato marcato e l’autore** -> <mark style="background: #FFB8EBA6;">firma digitale</mark>

3. **La marca temporale deve risultare immodificabile** -> oppure equivalentemente deve essere possibile identificare le modifiche -> <mark style="background: #D2B3FFA6;">hash sicuro</mark>

4. **Il documento deve poter rimanere riservato all’ente fidato che costruisce la marca temporale** -> <mark style="background: #D2B3FFA6;">hash sicuro</mark>

5. **Chiunque deve poter far marcare i propri documenti e verificare quelli marcati** -> <mark style="background: #BBFABBA6;">chiave di verifica sicura</mark> -> <mark style="background: #ABF7F7A6;">servizio pubblico</mark>

Per realizzare questo servizio sono sufficienti i meccanismi di firma digitale e le funzioni di hash già viste. Quest’ultime risultano fondamentali perché permettono di garantire la marcatura senza rivelare il contenuto dei dati all’ente fidato.

---
## Protocollo

![TSS.png](/img/user/sicurezza-informazione-M/immagini/TSS.png)

1. L'autore del documento che desidera ottenere una marca temporale invia all'ente fidato **solo un hash del documento**, **concatenato al proprio identificatore**
	- $H(m \ || \ A)$
	- Garantisce la <u>riservatezza del documento</u> e limita il consumo di banda
2. L'ente fidato genera la marca temporale **concatenando a ciò che ha ottenuto varie informazioni** -> istante di tempo di marcatura, il suo identificativo e un id di operazione 
	- $H(H(m\ || \ A) \ || \ TSS \ || \ t \ || \ n)$ 
	- l'ente, per avere valore legale, deve **firmare il messaggio con la sua chiave privata** ed archiviare il risultato
3. L’utente che riceve la marca temporale **concatena al documento originale la marca ottenuta** -> **firma il tutto tramite uno schema di firma digitale con appendice con la propria chiave privata** -> invia il tutto ad un altro utente

L'altro utente sarà in grado di comunicare con il TSS e verificare la marcatura del documento appena ricevuto.

---
## Problemi

1. ***Ogni documento avrà come allegato sia la firma dell’autore, sia la marca temporale firmata dall’ente terzo*** -> gestire nel tempo due chiavi diverse -> complicazione -> TSS viene utilizzato in contesti ridotti

2. ***Quando le chiavi di firma delle marche temporali scadono occorre inoltre che i documenti già firmati risultino ancora validi*** -> aumenta la complessità di gestione -> ulteriori firme

3. ***Poco scalabile*** -> l'efficienza degrada col numero di richieste

4. ***Sicurezza della chiave privata $S_T$*** -> viene utilizzata per firmare un elevato numero di documenti -> deve essere cambiata molto spesso