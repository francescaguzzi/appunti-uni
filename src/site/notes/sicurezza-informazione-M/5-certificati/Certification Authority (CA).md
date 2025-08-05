---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/certification-authority-ca/"}
---

#certificati 

È un **ente fidato** che rilascia ed autentica **certificati**, per avere la certezza che una chiave pubblica acquisita sia veramente quella associata al destinatario onde evitare manomissioni. 

---
## Certificati
L’insieme di informazioni minime da inserire all’interno del **certificato** e che devono essere fornite agli utilizzatori è costituito da:
$$ X \ || \ P_X \ || \ S_{S^T}(H(X\ || \ P_X))$$ dove:
- $X$ indica l'identità del proprietario della chiave
- $P_X$ indica la chiave pubblica dell'utente $X$
- $S_T$ chiave privata di $T$ 
- $S_{S^T}$ è la [[sicurezza-informazione-M/6-cifrariRSA/Firma digitale\|firma digitale]] per confermare che si conosce la chiave privata
- $H(X \ || \ P_X)$ firma digitale dell'hash dell'indentità e la chiave pubblica -> per garantire che il messaggio non sia stato modificato

Chi certifica la firma del certificatore? -> alla base firme autocertificate da ente fidato e poi ***chain-of-trust***.

Per la produzione di certificati si utilizzano **standard condivisi come** [[sicurezza-informazione-M/5-certificati/Standard X.509\|X.509]]. 

---
## Modelli di fiducia

#esercizi 

Gli utenti possono usare diverse CA -> bisogna instaurare rapporti di fiducia tra utenti di diversi domini -> <u>cammino di fiducia tra CA</u> -> due modelli:
- **Centralizzato**
	- Una <u>CA master</u> emette certificati per le altre -> troppe responsabilità
	- Tipicamente *struttura gerarchica* -> anche con cross-links
- **Distribuito**
	- Grafo generico in cui ogni CA può certificare le altre
	- Ogni CA segue le proprie politiche per la sicurezza e robustezza dei certificati 
		- *Policies* riportate nelle estensioni dei certificati emessi
		- Certificati emessi da una CA per un'altra <u>possono essere revocati</u> 
			- Uso di **Authority Revocation List (ARL)** -> praticamente CRL per le CA

