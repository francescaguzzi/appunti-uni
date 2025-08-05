---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/9-blockchain/bitcoin/"}
---

## Cos’è Bitcoin

**Bitcoin** è la prima criptovaluta basata su [[sicurezza-informazione-M/9-blockchain/Blockchain\|Blockchain]]. È una rete peer-to-peer in cui ogni nodo può inviare e ricevere moneta da altri nodi in modo anonimo. In Bitcoin non esiste una banca centrale: tutti partecipano alla gestione della rete condividendo copie del registro (ledger).

- **Rete peer-to-peer:** tutti i nodi sono uguali (peer) e tengono una copia aggiornata della blockchain. Per ricevere bitcoin, ogni utente genera uno o più indirizzi (stringhe alfanumeriche) basati su una coppia di chiavi crittografiche. Il wallet (portafoglio) è l’applicazione che tiene al sicuro queste chiavi; non contiene fisicamente monete, ma consente di firmare le transazioni.
    
- **Mining:** i miner sono i nodi che raccolgono le transazioni valide e tentano di aggiungere nuovi blocchi alla catena. Per ogni blocco minato con successo ricevono una _block reward_ (una certa quantità di bitcoin) oltre alle commissioni di transazione. Il numero di bitcoin creati è limitato a 21 milioni: ogni ~4 anni la ricompensa per blocco viene dimezzata. Questo processo è reso complicato dal puzzle di consenso (PoW) che controlla la velocità di creazione dei blocchi (circa uno ogni 10 minuti).
    
- **Wallet:** è il software in cui l’utente crea e gestisce le proprie chiavi crittografiche. Il wallet serve a firmare le transazioni (dimostrando che si possiede realmente la quantità inviata). Alcuni nodi sono solo wallet (custodiscono chiavi e identità) e non memorizzano l’intera blockchain.
    

### Funzionamento della rete Bitcoin

1. **Creazione della transazione:** Alice (nodo A) decide di inviare bitcoin a Bob (nodo B). Crea una transazione che include l’importo, il suo indirizzo e quello di Bob, e la firma con la sua chiave privata.
    
2. **Diffusione della transazione:** La transazione firmata viene trasmessa a tutti i nodi della rete (broadcast). Ogni nodo che la riceve la verifica: controlla la firma digitale e che Alice abbia abbastanza bitcoin non spesi.
    
3. **Validazione e inserimento in blocco:** Se la transazione è valida (firma corretta, nessuna doppia spesa), viene conservata in un pool di transazioni in attesa. I miner le raccolgono a gruppi per inserirle in un nuovo blocco. Tutti i nodi devono essere d’accordo sulla validità delle transazioni prima che queste vengano registrate.
    
4. **Consenso e mining:** I miner competono per risolvere il problema di PoW sul blocco candidato. Il primo miner a risolvere il puzzle invia il blocco alla rete. Gli altri nodi verificano la correttezza della soluzione e delle transazioni contenute; se tutto è valido, il blocco viene aggiunto alla blockchain. A quel punto Bob riceve i bitcoin, confermati dall’inserimento nel blocco.
    
5. **Incentivi alla correttezza:** Nessuno controlla i miner in anticipo, ma esistono ricompense economiche per chi agisce legittimamente. Ogni blocco minato contiene una transazione speciale (coinbase) che paga il miner vincitore. Se un miner provasse ad imbrogliare (inserendo una transazione falsa o provando a fare doppia spesa), rischierebbe di non far convalidare il blocco dalla maggioranza della rete e perdere così la ricompensa.
    
