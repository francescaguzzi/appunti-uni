---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/8-sicurezzadistribuita/kerberos/"}
---

#highpriority #identificazione #protocollo 

**Kerberos è un sistema di autenticazione di utenti in ambiente client/server**. *Il nome “Kerberos” si rifà alla figura mitologica del cane a tre teste per rappresentare i tre obiettivi originari dell’intero sistema, cioè l’<u>autenticazione</u>, l’auditing e l’accounting. Il progetto si è fermato alla gestione della sola autenticazione.*

Il protocollo Kerberos è quindi basato su un **ente centralizzato di autenticazione che permette di identificare gli utenti presso i server e viceversa, utilizzando solamente [[sicurezza-informazione-M/4-cifrarisimmetrici/Cifrari simmetrici\|crittografia simmetrica]]**. 

Gli utenti hanno a disposizione un certo numero di workstation che comunicano con un insieme di server. Ogni user ha un ID ed una password -> il sistema *memorizza un impronta della password di 64 bit come termine di paragone*. 

Obiettivi:
- Rendere impossibile ad un intruso l’impersonare un utente
- Eliminare la comunicazione della password in chiaro
- Rendere impossibile che un utente possa modificare l’IP di una workstation spacciandola per un’altra presso il server
- Rendere impossibili *attacchi con replica*
- L'utente deve identificarsi al primo accesso a ogni servizio

> Il pro di Kerberos è che **è tutto condiviso**, ma per ogni utente che va via o viene aggiunto bisogna garantire l’*aggiornamento delle workstation*, inoltre se ci sono cambi di server bisogna anche ristabilire i rapporti di fiducia. Dunque, è evidente che il contro sia la **gestione molto onerosa**

---
# AS e TGS

Efficienza, affidabilità e scalabilità del servizio di autenticazione sono ottenute tramite due server particolari: **AS** e **TGS**.
## Authentication Server (AS)

- **Memorizza password e diritti di tutti gli utenti**
- **Lancia una sfida a chi inizia una sessione** presso una qualsiasi workstation
- Restituisce un <u>documento cifrato</u> che l'**utente dovrà presentare a TGS**

AS <u>precondivide con tutti i client chiavi simmetriche</u> ($K_V'$, $K_V''$)
### Ticket-Granting Server (TGS)

- Condivide una **chiave segreta con AS** ed una con **ogni altro server**
- **Decodifica** e **verifica** il <u>documento</u> di AS che l'utente gli invia
- Esamina la correttezza della risposta alla sfida lanciata da AS 
- Se tutto è conforme **restituisce all'utente un diritto d'accesso (*ticket*) al server V di suo interesse** 
	- Il ticket è **valido per tutta la sessione di lavoro**

TGS <u>precondivide con tutti i server chiavi simmetriche</u>.

> $AD_C$ è l’**address del client**, o meglio della workstation dalla quale il client fa accesso. È **inserito nel ticket** <u>per evitare il riutilizzo del ticket stesso</u>. Ovviamente è possibile falsificare l’IP, dunque, non elimino il problema, ma ne riduco la probabilità.

---
# Protocollo di autenticazione

<mark style="background: #FFB86CA6;">Step 1</mark> 
$$\tag{1} C \to AS: ID \ || \ AD_C \ || \ ID_{TGS} \ || \ T_1$$ -> $C$ è l'user (con il suo relativo $ID$) e $T_1$ è un timestamp di log-on

<mark style="background: #FFF3A3A6;">Step 2</mark> 

$$AS \rightarrow C:E_{PSW}(K_{CT} \ || \ ID_{TGS}\ ||\ T_2 \ || \ \Delta T_2 \ || \ E_{K_{TGS}}(K_{CT} \ || \ ID \ || \ AD_C \ || \ T_2 \ || \ \Delta T_2)) \tag{2}$$
-> AS *controlla il timestamp*, preleva l'*hash della password salvato in corrispondenza di ID* e sfida C
-> se C riesce a decifrare il messaggio otterrà il documento per comunicare con il TGS
	-> $K_{CT}$ è la chiave di sessione, $T_2$ e $\Delta T_2$ inizio e durata massima della sessione, ed $E_{K_{TGS}}$ la chiave segreta che AS condivide con TGS 
		-> servirà per decifrare dati su chi è l'utente etc

<mark style="background: #BBFABBA6;">Step 3</mark> 
$$C\rightarrow TGS: ID_V\ || \ E_{K_{TGS}}(TICKET) \ || \ \underbrace{E_{K_{CT}}(ID \ || \ AD_C \ || \ T3)}_{\text{prova che C ha superato la sfida}} \tag{3}$$ -> C richiede la password all'utente, ne calcola l'hash e decifra il messaggio di AS
 -> se la decifrazione va a buon fine, C chiede $ID_V$ all'utente (ID server)
	 -> tramite il timestamp $T_3$ TGS controlla se la sessione è ancora valida

<mark style="background: #ABF7F7A6;">Step 4</mark>  
$$ TGS \rightarrow C:E_{K_{CT}}(K_{CV}\ || \ ID_V \ || \ T_4 \ || \ E_{K_V}(K_{CV} \ || \ ID \ || \ AD_C \ || \ T4 \ || \ \Delta T_4)) \tag{4}$$-> ​TGS decifra usando $K_{TGS}$ ed estrae $K_{CT}$, con cui completa la sfida di AS
-> se TGS riesce a recuperare il ticket di AS genera $K_{CV}$, $K_V$ e fissa un tempo entro cui l'accesso a $V$ è autorizzato ($T4$)

<mark style="background: #ADCCFFA6;">Step 5</mark>
$$C \rightarrow V:E_{K_V}(K_{CV}\ ||\ ID\ ||\ AD_C\ ||\ T_4\ ||\ \Delta T_4)\ ||\ E_{K_{CV}}(ID\ ||\ AD_C\ ||\ T5) \tag{5}$$-> $T5$ è il momento in cui il **client contatta effettivamente il server**
-> il diritto di accesso scadrà dopo $T​5 + \Delta T_4$

​<mark style="background: #D2B3FFA6;">Step 6</mark>
$$ V \rightarrow C:E_{K_{CV}}(T5+1)​ \tag{6}$$-> se $V$ è chi dice di essere riuscirà a decifrare il ticket e ad estrarre la chiave per comunicare con il client
	-> per farsi identificare da C, gli invia un messaggio in cui dimostra di aver decifrato quello precedente 

Nel caso in cui il client abbia ancora bisogno dello stesso server il procedimento ricomincia dal punto 5, mentre se ha bisogno di accedere ad un altro server ricomincia dal punto 3.

---

***Perché nel protocollo Kerberos si inserisce $AD_C$ (indirizzo IP del client) e l’autenticatore?***
	L’indirizzo IP del client serve per verificare che la richiesta provenga effettivamente dal Client che dice di averla inviata. TGS controlla che gli indirizzi IP corrispondano e, in caso contrario, scarta la richiesta.
		L’autenticatore viene inserito affinché il Client possa dimostrare al TGS di aver superato il controllo presso l’AS. Inoltre, viene inserito un timestamp T3 all’interno dell’autenticatore per evitare attacchi di replay.

---
# Versioni e kerberos inter-realm

Questa descritta è la versione 4 del protocollo che, come si è visto, **evita di dover inviare la password**. Ogni messaggio è corredato da un **timestamp** ed è cifrato con una **chiave di sessione** per <u>evitare attacchi con replica</u>. A seconda dell’impostazione dei ∆T, la frequenza di reimmissione della password sarà variabile. Quanto appena illustrato risulta valido nel caso in cui si stia analizzando un singolo dominio.

Non è possibile comunicare con altri realm (più kerberos), a meno che non siano presenti ***relazioni di fiducia tra i diversi realm*** -> se un utente vuole accedere a un servizio di un altro realm ne deve indicare l'$ID$ al posto di $ID_V$ nello step (3) -> il protocollo prevede poi due ulteriori step che servono a effettuare la richiesta presso il TGS remoto
- step 4 -> si ottiene il ticket di accesso al TGS remoto
- step 5 -> richiesta ticket d'accesso al server desiderato
- step 6 -> ottenimento ticket
- step 7 -> C contatta V

> Kerberos **non è un servizio di distribuzione di chiavi** (l’AS autentica gli utenti, non distribuisce chiavi). È un **servizio centralizzato basato su crittografia simmetrica**.

Dal punto di vista della ***scalabilità*** 
- **Intra-realm** -> fattore $N$ -> $N$ chiavi per $N$ utenti e $N$ servizi
- **Inter-realm** -> fattore $N^2$ 

Kerberos v5 introduce la possibilità di avere ticket di durata più lunga e utilizza algoritmi di cifratura più robusti di DES (usato in v4).