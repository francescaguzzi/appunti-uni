---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/public-key-infrastructure-pki/"}
---

#certificati #highpriority 

**È un’infrastruttura di gestione dei certificati; permette di distribuirli, aggiornarli, e revocarli**. Questo modello prevede quattro entità:
1. ***Registration Authority (RA)*** -> entità a cui gli utenti si rivolgono per chiedere la certificazione delle chiavi, identificandosi -> riceve le richieste di *Certificate Signing Request (CSR)* e *Revocation Request (RR)*
2. [[sicurezza-informazione-M/5-certificati/Certification Authority (CA)\|Certification Authority (CA)]] -> rilascia e verifica i certificati -> deve risiedere su una macchina sicura, con minime interazioni con l'esterno
3. ***Directory (DB)*** -> repository in cui sono conservati i certificati emessi -> standard x.500
4. ***Utenti (U)***

L'**unico canale di comunicazione sicuro è quello che collega la RA alla CA** e che l’utente pertanto potrà interagire con il sistema solamente tramite **canali insicuri**.

---
# Interazioni nel PKI

1. Utente -> chiede certificato -> RA
2. RA -> inoltra richiesta -> CA (*canale sicuro*)
3. CA -> verifica domanda e pubblica il certificato -> DB
4. Utente <-> DB (tramite *protocollo LDAP*)

L'utente potrà scaricare i certificati degli altri utenti e contattarli con testo cifrato mediante un modello asimmetrico.

---
# Richiesta di un certificato

Un utente X, per **farsi certificare una chiave di firma** deve:
1. Generare un autocertificato della sua $P_X$ $$ X \ || \ P_X \ || \ S_{S^X}(H(X \ ||\ P_X ))$$ che verrà usato come CSR (*Certificate Signing Request*)
2.  X -> RA il CSR appena creato, RA verifica la firma di X e -> CA i dati di X (richiesta approvata)
3. CA organizza i dati raccolti, aggiunge quelli di sua competenza, l'hash e lo firma con la sua chiave privata (**completa il certificato**)
4. Prima copia -> X e seconda copia -> DB 

![pki1.png](/img/user/sicurezza-informazione-M/immagini/pki1.png)

Il database è pubblico e non richiede alcuna forma di sicurezza.

**Qualunque sia il motivo, il possessore di un certificato può, in qualunque momento, chiederne la [[sicurezza-informazione-M/5-certificati/Revoca e ripudio di un certificato\|revoca]] alla CA. Quest’ultima, non appena riceve la richiesta, deve comunicare a tutto il dominio da lei amministrato che il certificato non è più valido.** 

--- 
# Componenti di un PKI
## Directory

La directory è un **database distribuito** utilizzato per salvare i certificati delle chiavi degli utenti. I **diversi server** che compongono questa architettura prendono il nome di **DSA (Directory System Agent)** -> geograficamente distribuiti e coordinati. 

Gli **utenti** che vogliono **accedere** alla directory utilizzano il **DUA (Directory User Agent)** -> l'accesso può essere autenticato o meno

Le informazioni sono memorizzate come entry in forma di **albero gerarchico**, ed **ogni entry è identificata da un Distinguished Name (DN)** -> path assoluto che lo identifica univocamente.

## Protocolli di gestione
### Centralizzato 

Modello di base, composto **soltanto da CA e utenti**. In questo modello le chiavi sono generate direttamente dalla CA, che memorizzerà quella pubblica e invierà all’utente finale il certificato e la sua chiave privata. 

*Vantaggi* -> l'utente deve solo richiedere il certificato e può sempre recuperare la sua chiave privata dalla CA
*Svantaggi* -> sia CA che utente conoscono la chiave privata -> <u>non c'è supporto al non ripudio</u> 

### Distribuito (a 3 parti)

Trè entità: Utenti, RA e CA. La maggior problematica in questo caso è l'implementazione organizzativa, per cui ci sono tre differenti soluzioni: 

1. **Alice si presenta di persona, genera le chiavi e presenta alla RA le sue credenziali fisiche o elettroniche. La RA analizza le credenziali e le inoltra alla CA che genera il certificato e lo invia alla RA. Quest’ultima lo inoltra all’utente, ad esempio, con una smart card.**
		-> *CA protetta dall'esterno, ma metodo molto costoso*
	Due sotto scenari:
	 1. Alice fornisce le sue credenziali e richiede un certificato
	 2. RA controlla e genera già le chiavi per tutte le smart card
	 
	 ![pki3.png](/img/user/sicurezza-informazione-M/immagini/pki3.png)
	 
2. **Prima ci si fa identificare presentandosi di persona e in un secondo momento si fa richiesta di certificato**
	-> l'utente genera le proprie chiavi e in un secondo momento richiede il certificato -> [[sicurezza-informazione-M/5-certificati/Proof of Possession (POP)\|Proof of Possession (POP)]]

	![pki2.png](/img/user/sicurezza-informazione-M/immagini/pki2.png)

3. **Modello con CA e RA invertite** -> prima si fa richiesta di certificato a CA e poi si chiede la validazione a RA
	![pki3 1.png](/img/user/sicurezza-informazione-M/immagini/pki3%201.png)

---
# Proprietà di una PKI

Il PKI deve saper gestire:
- RA deve essere sempre disponibile
- CA deve essere rapida nella gestione della CRL
- Collo di bottiglia (max utenti)
- Ente degno di fiducia
- Interrogazione della CRL
- Vita della chiave di firma

Una PKI deve inoltre garantire l'aggiornamento delle chiavi in maniera trasparente ed automatica. La chiave pubblica, se si vuole inviare dei file cifrati, è usata per cifrare le cosiddette chiavi di sessione.
