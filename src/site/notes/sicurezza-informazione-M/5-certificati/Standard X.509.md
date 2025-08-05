---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/standard-x-509/"}
---

#certificati #lowpriority 

**È uno standard per comporre i certificati e per renderli validi a livello globale**. I certificati devono contenere tutti i dati necessari e, allo stesso tempo, minimizzare la dimensione.

Contiene una parte di dati e una di firma.

- Versione
- ID del certificato
- Algoritmo di firma
- Nome ente certificazione
- Periodo di validità -> in cui l'ente è responsabile -> due campi `not before` e `not after` 
- Nome soggetto
- Chiave pubblica
- Estensioni -> per aggiungere info su chiave, politiche di emissione, ente, utente) -> *key information*, *policy information*, *user and CA attributes* 