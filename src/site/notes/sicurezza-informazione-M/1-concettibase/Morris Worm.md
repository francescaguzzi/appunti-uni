---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/1-concettibase/morris-worm/"}
---

#funfact 

Nella notte del 2 novembre 1988 uno studente della Cornell University, Robert T. Morris Jr., diffuse il primo worm che infettò il 10% dei nodi della rete internet dell’epoca (evoluzione di Arpanet). Il _worm è un particolare tipo di malware capace di auto-replicarsi_. 

Il worm sfruttava le seguenti vulnerabilità: 
- Una falla nella modalità di debug del programma Unix sendmail per propagarsi nella rete
- Un buffer overflow o overrun del servizio di rete “finger”
- Sfruttava `rsh/rexec` indovinando password deboli 

Morris non intendeva creare un programma altamente distruttivo, voleva semplicemente evidenziare le debolezze presenti in molte reti dell'epoca. Purtroppo, però, una errata codifica del worm portò a una conseguenza non voluta da Morris; infatti, quest’ultimo divenne più dannoso e diffondibile di quanto originariamente previsto -> programmò il worm per copiare se stesso il 14% delle volte -> un computer poteva essere infettato più volte -> crash continui. 

Dopo questo attacco venne istituita la CERT (Computer Emergency Response Team), un’associazione che si facesse responsabile di raccogliere le informazioni degli attacchi e cercare quindi strategie per evitarle e prevenirle.