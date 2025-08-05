---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/ocsp-online-certificate-status-protocol/"}
---

#certificati #protocollo 

**È un protocollo standard client-server che permette ad un utente di contattare una terza parte fidata, anche diversa dalla CA, per chiedere se un determinato certificato è ancora valido. Il server risponderà con un messaggio firmato che contiene lo stato del certificato.** 

Questo metodo viene solitamente usato se è necessario che l’utente abbia informazioni sempre aggiornate circa lo stato di revoca dei certificati (che è <u>pull e online</u>).

I cosiddetti ***OCSP Responder*** seguono principalmente due modelli:
- **Trusted responder** -> il server OCSP firma le risposte con una coppia chiave-certificato <u>indipendente</u> da quella della CA per cui opera
- **Delegated responder** -> il server OCSP firma le risposte con una coppia chiave-certificato diversa <u>in base alla CA</u> per cui sta operando

Il protocollo OCSP offre quindi due **vantaggi** principali:
- Freschezza delle informazioni
- Gli utenti non devono scaricare la struttura dati con le revoche dei certificati