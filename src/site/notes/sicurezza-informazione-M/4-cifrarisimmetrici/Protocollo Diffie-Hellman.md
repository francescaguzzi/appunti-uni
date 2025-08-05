---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/protocollo-diffie-hellman/"}
---

#highpriority #gestionechiavi #algoritmo 

Si tratta di un ulteriore approccio per lo scambio di chiavi che non prevede nessun *Key Agreement* (KA).

**Esso consente di scambiare una chiave in maniera sicura su un canale insicuro per mezzo di funzioni pseudo unidirezionali. Si basa sulla difficoltà computazionale del calcolo dei logaritmi discreti.**

L'algoritmo funziona come segue:

1. Alice e Bob scelgono inizialmente
	- Un numero primo molto grande (almeno 350 cifre decimali) detto $p$
	- Un generatore $g$ di quel numero $p$ -> un numero le cui potenze modulo $p$ generano interi compresi tra $1$ e $p-1$ e quindi $$g^1 \mod p, g^2 \mod p, ..., g^{p-1}\mod p$$
2. Alice sceglie un valore casuale $a<p$ e calcola il valore $V_A=g^a (\mod p)$ e lo invia a Bob

3. Bob sceglie a sua volta un valore casuale $b<p$ e calcola $V_B = g^b(\mod p)$ e lo invia ad Alice

4. Alice calcola $K_A= (V_B)^a(\mod p)$ 

5. Bob calcola $K_B=(V_A)^b(\mod p)$

6. Grazie alle proprietà dell’aritmetica modulare si dimostra che tali valori sono uguali $$ K_B= (g^a\mod p)^b \equiv (g^b\mod p)^a = K_A$$
Di conseguenza, **Alice e Bob sono in possesso della medesima chiave sebbene non l’abbiano mai condivisa esplicitamente**.

Questo scambio è **anonimo** e **non permette in alcun modo di identificare le parti in causa**; esistono tuttavia varianti che prevedono anche di fare questo. 

La sua robustezza è legata alla difficoltà di calcolare il logaritmo discreto di un numero; in particolare, tale operazione risulta **molto complessa quando la base del logaritmo è un numero primo molto grande**.

![diffiehellman.png](/img/user/sicurezza-informazione-M/immagini/diffiehellman.png)

---
## Diffie-Hellman variante El Gamal

Questa variante di Diffie-Hellman prevede che almeno uno dei due comunicanti (A o B) deve aver fornito all’altra parte il suo $V_A$ o $V_B$ (in modo sicuro) **tramite un canale fuori banda anch'esso sicuro**. 

Purtroppo, in questa variante **si perde il più grande vantaggio di Diffie-Hellman,** ovvero la **possibilità di comunicare senza accordi fuori banda**. 

---
# Scambio Diffie-Hellman e certificati
#highpriority #certificati 

## Anonymous Diffie-Hellman

**Diffie-Hellman Anonymous** è la versione del protocollo Diffie-Hellman descritta in precedenza. È detto anonimo perché non abbiamo nessuna garanzia su chi ha generato $V^A$ A e $V^B$ ovvero sul fatto che A e B siano realmente chi dicono di essere; infatti, non assicura nessuna garanzia sull’autenticità delle parti. Quindi a meno che non ci troviamo in uno scenario in cui gli utenti possono fidarsi tra di loro, questo algoritmo non può essere usato per la condivisione sicura di segreti.

Molti protocolli di rete come [[sicurezza-informazione-M/8-sicurezzadistribuita/SSL-TLS\|SSL-TLS]] e [[sicurezza-informazione-M/8-sicurezzadistribuita/IPSec\|IPSec]] utilizzano una versione di questo modello che prevede che <u>non vengano utilizzati VA e VB per cifrare</u>, in quanto se tra un client e un server venisse utilizzata sempre la stessa chiave aumenterebbe la probabilità di successo di eventuali attacchi. 

È prevista dunque una **randomizzazione dei V** (che vengono chiamati *pre-master secret*) **ogni volta che si inizia una nuova sessione di comunicazione**.

> La chiave { $K_A=(V^B)^A \mod p = K_B = (V^A)^B \mod p$ }(detta *master secret*) 
> sarà data alla funzione hash calcolata su { $R_A \ || \ R_B \ || \ V$ }
> con $R_A$ e $R_B$ numeri random

![anonymousDH.png](/img/user/sicurezza-informazione-M/immagini/anonymousDH.png)

Per superare i problemi relativi all’identificazione delle parti in gioco, (ovvero dell’autenticazione di V che manca nella versione Anonymous) si ricorre ai certificati e si adottano due schemi.

---
## Fixed Diffie-Hellman

La variante Fixed prevede che **il parametro $V$ di un utente, $p$, $g$ e l'identità dell'utente vengano incapsulati in un [[sicurezza-informazione-M/5-certificati/Certification Authority (CA)#Certificati\|certificato X.509]]**. 

Quindi, esattamente come avviene per le chiavi pubbliche, ci sarà un CA che firmerà digitalmente il certificato -> in questo modo però **il pre-master secret $V$ non potrà mai cambiare ma sarà sempre valido fino a quando non sarà valido il certificato**. 

La variante Fixed **garantisce l’autenticazione di $V$ ma ancora non garantisce l’identificazione delle parti** (so di chi è V, non so chi me lo sta mandando) -> l'unica garanzia che assicura è che **un malintenzionato non può fingersi A o B, perchè non conosce gli esponenti ($a$ o $b$)** con il quale è stato generato il parametro $V$ nel certificato.
 
**Chiunque potrebbe però inviare il certificato di qualcun altro e sfruttare questo stratagemma per indurre l’altra parte a generare messaggi cifrati che non sarebbero previsti** -> <u>il protocollo non garantisce l'identificazione delle parti</u>
-> (si può prevedere un protocollo di sfida-risposta al termine dello scambio per verificare che le due chiavi sono uguali)

![fixedDH.png](/img/user/sicurezza-informazione-M/immagini/fixedDH.png)

---
## Ephemereal Diffie-Hellman

**La variante Ephemeral, evita che $V$ rimanga fisso per un determinato utente e mette in piedi uno scambio degli $V$ (che quindi diventano variabili) tra client e server garantendone l’autenticità.**

Client e server genereranno per ogni sessione degli $a$ o $b$ diversi quindi, di conseguenza, **degli $V$ diversi che verranno inviati all'altra parte firmati digitalmente e con allegato il certificato inerente alla chiave pubblica ($P_A$ e $P_B$) con cui l'altra parte può verificare l'autenticità della firma.**

**La [[sicurezza-informazione-M/6-cifrariRSA/Firma digitale\|Firma digitale]] garantisce autenticità e integrità del parametro $V$ inviato**; tuttavia, <u>non garantisce ancora l’identificazione delle parti</u> in quanto **chiunque potrebbe aver inviato un parametro $V$ firmato digitalmente intercettato in una precedente comunicazione**, insieme al certificato di chiave pubblica dello stesso utente intercettato, che è disponibile pubblicamente.

Quindi l’autenticità di V mi garantisce che, se una delle due parti non è chi dice di essere, esse non potranno arrivare a concordare lo stesso segreto, **ma ancora una volta non dà nessuna garanzia che l’utente che invia un parametro firmato è realmente chi dice di essere.** 

![ephemerealDH.png](/img/user/sicurezza-informazione-M/immagini/ephemerealDH.png)