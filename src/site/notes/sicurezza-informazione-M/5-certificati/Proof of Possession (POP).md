---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/proof-of-possession-pop/"}
---

#certificati 

La **Proof of Possession (POP)** è un **metodo utilizzato dalla CA per avere garanzie circa il possesso della chiave privata da parte del soggetto che richiede il certificato**. Rilasciare un certificato senza prova di possesso può portare a vari attacchi.

> La POP è essenziale per le chiavi utilizzate per l’autenticazione, ma non strettamente necessaria per le chiavi utilizzate per cifrare dati

Per richiedere la POP possono essere usati vari metodi:
- **POP a tempo di firma** -> ogni volta che l’utente firma un documento firma anche un riferimento al certificato che contiene la chiave pubblica relativa alla sua chiave privata, ovvero la chiave contenuta nel certificato -> metodo migliore, ma non supportato dai protocolli di sicurezza
- **POP online** -> la CA verifica la POP prima di emettere il certificato -> oltre alla chiave pubblica, viene mandato un messaggio cifrato con la chiave privata -> se la CA riesce a decifrare e trova il messaggio di richiesta allora può essere certa del possesso
- **Metodi Out-of-Band (OOB)** -> si basano sul possesso effettivo di una smart card o di un token