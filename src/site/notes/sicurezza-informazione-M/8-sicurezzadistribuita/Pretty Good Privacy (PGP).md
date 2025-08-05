---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/8-sicurezzadistribuita/pretty-good-privacy-pgp/"}
---

#protocollo #identificazione #gestionechiavi #highpriority 

PGP è un servizio a livello applicativo che offre la **riservatezza** e l’**autenticazione** (oltre a *compressione* e *compatibilità*), impiegato in applicazioni di posta elettronica e di archiviazione di file.

Questo modello è nato per rinunciare ai costi dovuti all’intera [[sicurezza-informazione-M/5-certificati/Public Key Infrastructure (PKI)\|infrastruttura PKI]] necessaria all’utilizzo delle chiavi pubbliche ed introduce una ***rete di fiducia reciproca*** in sua sostituzione. Il modello di fiducia su cui si basa PGP prende il nome di ***Web of Trust*** ed è totalmente <u>decentralizzato</u> in quanto **non c'è l’ausilio di un’autorità di certificazione che si assume responsabilità sulle chiavi pubbliche che certifica**.

Sebbene PGP sia leggero in termini infrastrutturali, questo modello **non ha validità in termini legali** e risulta inutilizzabile nel caso di reti già di medie dimensioni in quanto **implica che tutti gli utenti si conoscano e che si fidino l’un l’altro**.

Questo protocollo è realizzato mediante l’utilizzo di servizi di:
- Autenticazione con firma digitale
- Confidenzialità
- Compressione
- Compatibilità

---
# Autenticazione 

Per l’autenticazione viene utilizzato uno **schema con appendice** in modo da ottenere i vantaggi già descritti precedentemente. Solitamente si utilizza questo schema per l’invio di mail firmate.

![pgpauth.png](/img/user/sicurezza-informazione-M/immagini/pgpauth.png)

Si noti l’introduzione di una ***funzione di compressione*** ($Z$) <u>dopo</u> l’operazione di firma, questo è dovuto ad un motivo legato alla verifica a posteriori della firma stessa; infatti:
- se la funzione $Z$ fosse <u>prima</u> della firma -> verrebbe firmato il documento compresso 
	- se il destinatario volesse verificare la firma dovrebbe comprimere di nuovo il documento -> overhead
- ponendo $Z$ <u>dopo</u> la decompressione va effettuata soltanto una volta alla ricezione del documento

---
# Riservatezza

![pgpriservatezza.png](/img/user/sicurezza-informazione-M/immagini/pgpriservatezza.png) 

Per garantire la riservatezza dei dati viene usato un [[sicurezza-informazione-M/6-cifrariRSA/Cifrario Ibrido\|Cifrario Ibrido]]. 

La chiave `k` utilizzata per cifrare i dati viene **generata di volta in volta per mezzo di un generatore di numeri casuali** in modo da ottenere una cifratura robusta.

Per quanto riguarda la funzione $E_p$ -> tecniche di padding sicuro o randomizzazione dei dati in ingresso per garantire la robustezza dell'operazione.

Si noti inoltre l’**uso della funzione di compressione <u>prima</u> della cifratura dei dati** -> **riduce la quantità di ridondanza naturalmente presente nei dati** -> aumenta l'<u>entropia</u>.

## Autenticazione e riservatezza

Si noti che le due tecniche possono essere combinate in modo da inviare dati autentici e riservati allo stesso tempo. Per ottenere questo è necessario **prima firmare il messaggio e poi cifrarlo** secondo gli schemi sopra descritti. Questa scelta <u>non risulta ottimale in realtà</u>, infatti essa **costringe un utente a decifrare obbligatoriamente il messaggio per poterlo autenticare**; dunque, nel caso in cui un messaggio non risulti autentico l’utente avrà effettuato un’operazione inutile.

| AUTENTICAZIONE   | <u>Compressione a valle</u> per **efficienza in memorizzazione** e per non dover comprimere ogni volta il messaggio per verificare la firma |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **RISERVATEZZA** | **Compressione <u>a monte</u> per eliminare ulteriore ridondanza                                                                            |


---
# Compatibilità

Alcuni sistemi di posta permettono di elaborare solamente i **caratteri ASCII** stampabili; pertanto, occorre trasformare la rappresentazione dei dati in una composta solo da caratteri ASCII, per ottenere ciò si utilizza il sistema Radix-64 (conosciuto anche come ***Base-64***) -> **quest'operazione introduce un'espansione dei dati del 33% circa**

---
# Chiavi e portachiavi

**Ogni utente possiede un *portachiavi* per contenere le proprie chiavi private ed uno per conservare le chiavi pubbliche ottenute -> sostituisce il CA**
### Portachiavi privato (per ogni utente)
Questa struttura contiene le chiavi private dell’utente. Esse sono salvate e cifrate (con un cifrario simmetrico che usa come chiave i 128 bit dell’hash della passphrase).
### Portachiavi pubblico (per ogni utente)
Questa struttura contiene le <u>chiavi pubbliche degli utenti con cui ogni utente interagisce</u>. 
È strutturato nel seguente modo:
- **Owner trust** -> grado di fiducia che il proprietario ripone in una certa chiave pubblica -> si possono impostare a seconda di quando è stata ottenuta la chiave o quanto si conosce il proprietario
- **Signature** -> contiene il certificato della chiave, se esiste -> firmato da un qualsiasi intermediario
- **Signature trust** -> <u>calcolata da PGP</u> -> livello di fiducia associato al firmatario intermediario (valore in Owner Trust)
- **Key Legitimacy** -> <u>calcolata da PGP</u> -> owner trust + signature trust -> viene ricalcolato ad intervalli regolari

Questo modello non si basa quindi esclusivamente su CA, ma anche sul “*passaparola*” tra gli utenti per la distribuzione delle chiavi pubbliche, pertanto <u>non può avere valore legale</u>. 

Allo stesso tempo, **la revoca di una chiave non può essere propagata automaticamente**, pertanto il diffondersi di questa informazione risulta **molto più lento**. 

---
# Formato dei messaggi

![pgpformato.png](/img/user/sicurezza-informazione-M/immagini/pgpformato.png)

Per risparmiare spazio, dato che le chiavi possono essere molto lunghe, **si usano come ID i 64 bit meno significativi**
- Nessun problema di sicurezza
- Possibilità rara di non univocità -> piccolo overhead