---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/9-blockchain/blockchain/"}
---

#definizione #concetto #argomentotutor

## Cos’è la Blockchain

La blockchain è un registro digitale distribuito e condiviso tra molti computer (nodi) senza bisogno di un’autorità centrale. Ogni blocco contiene un insieme di transazioni confermate e riferimenti crittografici al blocco precedente. Grazie a questo collegamento, le informazioni aggiunte diventano praticamente **immutabili**: per modificare un vecchio blocco si dovrebbe rifare tutti quelli successivi, cosa che la rete respinge automaticamente. In pratica, la blockchain funziona come una **catena di blocchi** in cui ogni blocco è “salato” da un’impronta (hash) del blocco precedente. Così la catena diventa una lunga storia di transazioni ordinate cronologicamente e sicura tramite crittografia.

### Struttura dei blocchi

- **Intestazione (header):** ogni blocco ha informazioni di base come il numero di blocco, il timestamp (quando è stato creato) e un _nonce_ (un numero usato nei calcoli di consenso).
    
- **Hash del blocco precedente:** nell’intestazione c’è l’hash crittografico (SHA-256) dell’intestazione del blocco precedente. Questo “puntatore hash” collega i blocchi come in una catena.
    
- **Merkle Root:** nell’intestazione è memorizzato anche l’hash delle transazioni del blocco (la _Merkle Root_), ottenuto da un albero speciale (Merkle Tree).
    
- **Corpo del blocco:** oltre all’intestazione, il blocco contiene i dati delle transazioni vere e proprie. L’hash di ciascuna transazione viene combinato a coppie in un albero fino a formare la Merkle Root.
    

Questa struttura a catena e ad albero garantisce che ogni nuova informazione sia ben ancorata alle precedenti: una volta registrata, non può essere cambiata senza invalidare tutta la catena.

### Merkle Tree

Le transazioni all’interno di un blocco sono organizzate in un **albero di Merkle**. In questo albero, le foglie sono gli hash delle singole transazioni e ogni nodo padre è l’hash combinato dei due figli. Alla radice dell’albero si trova la **Merkle Root**, un unico hash che riassume tutte le transazioni del blocco. Grazie a questa struttura, per verificare se una certa transazione è inclusa nel blocco basta controllare una breve “prova” basata sulla Merkle Root, senza dover elaborare tutte le transazioni. In altre parole, la Merkle Root rende la verifica rapida ed efficiente, perché concentra tutte le informazioni di molte transazioni in un solo punto.

## Algoritmi di consenso

Per aggiungere nuovi blocchi alla blockchain tutti i nodi devono raggiungere un **consenso**, cioè concordare su quali transazioni siano valide. I protocolli di consenso risolvono il problema di farci accordare anche se ci sono nodi che sbagliano o tentano di barare. I due algoritmi più diffusi sono:

- **Proof of Work (PoW):** i miner (nodi partecipanti) competono a risolvere un problema di difficoltà variabile, essenzialmente cercando un valore (_nonce_) che rende l’hash del blocco numericamente sufficientemente piccolo. Chi trova la soluzione (trova il nonce giusto) per primo propaga il blocco in rete. Se la maggioranza dei nodi (50%+1) verifica che la soluzione è corretta, il blocco viene accettato ed il miner riceve una ricompensa in criptovaluta. La difficoltà del problema viene regolata in modo che mediamente venga trovato un blocco ogni ~10 minuti.
    
- **Proof of Stake (PoS):** invece di competere con la potenza di calcolo, gli utenti “stake-ano” (congelano) una certa quantità di criptovaluta come garanzia. Il sistema sceglie casualmente chi potrà aggiungere il prossimo blocco, dando più probabilità a chi ha messo in stake più monete. L’utente scelto (detto **forger** o validatore) riceve un premio proporzionale alla sua puntata.
    

Ogni protocollo di consenso previene vari attacchi (come doppie spese o manomissioni) sfruttando la matematica e le ricompense economiche. Ad esempio, in PoW chi tenta di falsificare un blocco spenderebbe tempo e elettricità inutilmente, perché senza la maggioranza dei nodi non otterrebbe la ricompensa.

## Libro mastro e sicurezza crittografica

Il **libro mastro** della blockchain è l’insieme dei blocchi concatenati: tutti i partecipanti hanno una copia di questo registro. La sicurezza è garantita da due strumenti principali: gli hash crittografici e le firme digitali. Ogni transazione è firmata digitalmente con la chiave privata del mittente, in modo che solo il legittimo proprietario possa spenderla. Inoltre, ogni blocco contiene l’hash SHA-256 del blocco precedente, legando i blocchi a catena. Si usano algoritmi robusti (SHA-256 per l’hash e curve ellittiche per le firme), ritenuti quasi impossibili da violare con la tecnologia odierna.

Grazie a questi sistemi, manomettere una transazione o un blocco è estremamente difficile: occorrerebbe rifare i calcoli di hash di tutti i blocchi successivi e convincere la maggioranza dei nodi ad accettare la versione alterata, cosa praticamente irrealizzabile. In breve, la blockchain agisce come un registro pubblico ma sicuro, dove ogni voce è verificata da tutta la rete e protetta dalla crittografia.

## Attacchi alla Blockchain

Alcuni possibili attacchi sfruttano la struttura della blockchain, ma vengono mitigati dal design del sistema:

- **Attacco del 51%:** se un singolo attore (o un gruppo coordinato) controllasse oltre il 50% della potenza di calcolo della rete, potrebbe potenzialmente riscrivere la storia della blockchain, impedendo ad altri di aggiungere blocchi o facendosi restituire transazioni già effettuate. In pratica avrebbe la maggioranza dei “voti” necessari a certificare i blocchi e potrebbe usare questo potere a proprio vantaggio (ad es. per fare doppia spesa). Per questo motivo, blockchain grandi e diffuse come Bitcoin sono molto sicure, perché ottenere il 51% dell’hashrate è proibitivo in termini di costi e risorse.
    
- **Fork (biforcazioni):** a volte la blockchain si divide in due rami temporanei quando due miner trovano simultaneamente un blocco diverso. In rete accadrà che alcuni nodi vedono prima l’uno, altri l’altro, creando due versioni della catena. A quel punto la regola della **chain più lunga** decide il vincitore: è probabile che dopo pochi minuti venga trovato un nuovo blocco su uno dei rami, rendendolo più lungo. Tutti i nodi allora considereranno principale la catena più lunga, scartando l’altro ramo secondario. Questo riallineamento garantisce che la blockchain torni unica (univoca) nel tempo.
    
- **Doppia spesa:** è il tentativo di spendere gli stessi bitcoin due volte. Ad esempio, un utente B invia bitcoin a C e simultaneamente prova a nascondere questa transazione (o a crearne una contraria). In questo caso esisterebbero due versioni della storia: una in cui C ha ricevuto i soldi e una in cui no. Il protocollo di consenso previene questo attacco: solo la transazione inclusa nella catena “vincente” viene considerata valida, mentre l’altra viene abbandonata. Se B cerca di imbrogliare, dovrà farlo contro la potenza di calcolo del resto della rete; perciò un tentativo di doppia spesa di solito genera un fork che si risolve a favore del ramo che riesce a crescere per primo.
    

In sintesi, la combinazione di consenso distribuito, crittografia e ricompense economiche rende la blockchain molto resistente a frodi e manomissioni. Tuttavia, è importante sapere che se potessero verificarsi situazioni estreme (come l’ottenere il 51% dell’hashrate), i protocolli correnti avrebbero difficoltà a difendersi, per cui la sicurezza si basa anche sulla grandezza e decentralizzazione del network.


