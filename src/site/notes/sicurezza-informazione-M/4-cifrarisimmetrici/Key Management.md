---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/key-management/"}
---

#gestionechiavi 

Il Key Management è l’area della crittografia che si occupa di come **generare**, **distribuire** e **distruggere** le [[sicurezza-informazione-M/2-hash-PRNG/Chiavi\|chiavi]].

l sistema più sicuro per lo scambio delle chiavi (simmetriche) sarebbe un canale sicuro dedicato, ma ciò non è scalabile né automatizzabile. Esistono quindi due modelli:
- La **presenza di un accordo a priori che implichi la condivisione di un segreto iniziale** a partire dal quale **generare le chiavi**
	- [[sicurezza-informazione-M/4-cifrarisimmetrici/Master Key\|Master Key]]
	- [[sicurezza-informazione-M/4-cifrarisimmetrici/Key Distribution Center (KDC)\|Key Distribution Center (KDC)]]
- **Senza alcun accordo a priori** di un segreto iniziale 
	- [[sicurezza-informazione-M/4-cifrarisimmetrici/Protocollo Diffie-Hellman\|Protocollo Diffie-Hellman]]
	- [[sicurezza-informazione-M/5-certificati/Meccanismi asimmetrici\|Meccanismi asimmetrici]]
