---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/revoca-e-ripudio-di-un-certificato/"}
---

#certificati #highpriority 

Il **ripudio** è l'azione con cui un utente, prima della scadenta, spezza l'associazione sancita da un certificato: $$\text{chiave pubblica - proprietario}$$È indispensabile che questo evento sia **tempestivamente notificato** a tutti gli altri utenti, altrimenti nello stesso istante del ripudio altri utenti potrebbero ancora utilizzare il vecchio certificato. Il **ripudio va notificato alla RA** e **la CA emette la revoca del certificato** e se ne assume la responsabilità.

Lo stato di revoca deve essere poi **notificato** e **verificato**.
- ***Notifica***
	- **Pull** -> user preleva il certificato e controlla se è stato revocato o no
	- **Push** -> CA notifica il dominio
- ***Verifica*** 
	- **Schema offline** -> l’utente scarica (una volta soltanto) l’intero insieme dei certificati revocati -> [[sicurezza-informazione-M/5-certificati/CRL (Certificate Revocation List)\|CRL (Certificate Revocation List)]] 
	- **Schema online** -> l'utente si rivolge ogni volta alla CA per poter determinare la validità del certificato -> [[sicurezza-informazione-M/5-certificati/OCSP (Online Certificate Status Protocol)\|OCSP (Online Certificate Status Protocol)]]

Sia CRL che OCSP sono protocolli <u>pull</u> -> **i metodi pull addossano meno carico su RA e CA** -> con un metodo push bisonerebbe utilizzare un protocollo publisher/subscriber tipo notifiche in tempo reale

## Performance

In quanto a prestazioni, a **lato utente** occorre preoccuparsi delle <u>dimensioni del file da scaricare</u>, sia perché ciò richiede una buona connessione sia perché richiede spazio su un dispositivo di memorizzazione, del <u>carico computazionale richiesto</u> (perché l’utente potrebbe accedere da macchine poco potenti) della <u>banda disponibile e quella richiesta</u>.

**Lato amministratore** invece occorre valutare la <u>mole dei picchi di carico e di richieste</u> e valutare a quanto ammontano il <u>carico medio e la richiesta media considerandone la distribuzione tra i nodi disponibili</u>. È importante inoltre considerare la <u>tempestività</u> in relazione al grado di sicurezza che si vuole garantire.