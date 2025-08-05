---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/crittoanalisi/"}
---

#definizione  #lowpriority 

La crittoanalisi, come già detto, è la controparte della crittografia. In questo ambito **si cerca di dedurre i segreti utilizzati durante la cifratura dei dati**. L’intruso per carpire un dato segreto in generale può:
1. **Indovinare il segreto**
	Soluzione: dati casuali, non concedere tempo di prova, modificare frequentemente il segreto
2. **Intercettare il segreto**
	La sicurezza dipende da come è protetta l'area di memoria in cui è memorizzata la [[sicurezza-informazione-M/2-hash-PRNG/Chiavi\|chiave]]
3. **Dedurre il segreto** 
	Il *legame tra il testo in chiaro e il testo cifrato deve apparire come una variabile aleatoria che assume con eguale probabilità tutti i suoi possibili valori*
	Vi sono diverse tipologie di #attacchi per la deduzione del segreto:
	- **Solo testo cifrato** -> l'attaccante ha accesso solo a testi cifrati
	- **Con testo in chiaro noto** -> insieme di testi cifrati non scelti con i corrispondenti testi in chiaro
	- **Con testo in chiaro scelto** -> può scegliere del testo in chiaro e ottenere il corrispondente cifrato
	- **Con testo cifrato scelto** -> testo cifrato scelto da lui e versioni decifrate dello stesso (senza conoscere la chiave)