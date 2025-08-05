---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/meccanismi-asimmetrici/"}
---

#definizione 

La crittografia asimmetrica può essere usata nelle comunicazioni per garantire: 
- Riservatezza 
- Autenticazione 
- [[sicurezza-informazione-M/1-concettibase/Non ripudiabilità\|Non ripudiabilità]] -> importante 

Ogni entità che comunica mediante un cifrario asimmetrico possiede una coppia di chiavi:
- **Chiave privata** -> *segreta*
- **Chiave pubblica** -> *pubblicamente accessibile* -> bisogna garantirne *autenticità* ed *integrità* -> deve essere **disponibile** e facilmente reperibile da chiunque

Per la generazione delle chiavi viene utilizzata una **funzione pseudo unidirezionale** in modo che sia possibile **derivare facilmente la chiave pubblica dalla chiave privata, ma che non sia possibile effettuare l’operazione inversa**.
-> le chiavi vengono generate da [[sicurezza-informazione-M/6-cifrariRSA/Cifrari asimmetrici\|Cifrari asimmetrici]] 

Deve sempre essere possibile, inoltre, reperire la chiave pubblica di un utente e deve esistere un meccanismo che garantisca che quella chiave appartenga effettivamente ad un certo utente (non-ripudio) -> per evitare *man-in-the-middle*. 
Bisogna a tal fine disporre di un'**architettura software in grado di garantire l'autenticità delle chiavi**.

Questo esempio mette in luce la necessità di un diverso meccanismo per la distribuzione delle chiavi pubbliche, più sicuro rispetto ad un repository pubblico. A questo proposito vi sono due modelli:
- **Centralizzato** -> ente di terze parti -> [[sicurezza-informazione-M/5-certificati/Public Key Infrastructure (PKI)\|Public Key Infrastructure (PKI)]] + [[sicurezza-informazione-M/5-certificati/Certification Authority (CA)\|Certification Authority (CA)]]
- **Distribuito** -> ogni utente fornisce certificati -> [[sicurezza-informazione-M/8-sicurezzadistribuita/Pretty Good Privacy (PGP)\|Pretty Good Privacy (PGP)]]




