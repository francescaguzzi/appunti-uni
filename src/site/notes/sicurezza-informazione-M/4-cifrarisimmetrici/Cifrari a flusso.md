---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/cifrari-a-flusso/"}
---

#definizione 

Sono cifrari che si ispirano al [[sicurezza-informazione-M/3-cifrariclassici/Cifrario di Vernam-Mourborgne\|One-Time Pad]] e vanno a ***trasformare uno o pochi bit alla volta*** del testo in chiaro facendone la somma modulo due (**XOR**) con un flusso di chiave opportunamente generato che prende il nome di ***keystream***.

Risultano adatti per la **trasmissione di dati orientata al flusso** (come applicazioni web, telefonia, trasmissione di caratteri, audio, video) perché per come sono implementati non introducono rallentamenti; quindi, sono ***generalmente più veloci dei cifrari a blocchi***.

Nei cifrari a flusso:
- **Cifratura** -> viene svolto lo XOR, bit per bit, del testo <u>in chiaro</u> con il flusso di chiave generato
- **Decifrazione** -> viene svolto lo XOR, bit per bit, del testo <u>cifrato</u> con il flusso di chiave generato

**Il flusso di chiave (keystream) deve essere casuale, imprevedibile, indeducibile e usato una sola volta. Esso è <u>lungo quanto il testo in chiaro</u> da cifrare e viene generato tramite un [[sicurezza-informazione-M/2-hash-PRNG/Random Number Generator (RNG)#Pseudo Random Number Generator Cryptographically Secure (PRNGCS)\|PRNG crittograficamente sicuro]] a partire da un seed imprevedibile concordato tra la sorgente e la destinazione.**

È computazionalmente sicuro ma non perfetto poiché dopo il periodo di generazione, il *PNRG ricomincia a generare la stessa sequenza di chiavi* e ciò provoca **vulnerabilità**.

## Perdita di sincronismo 
#proprietà 

La perdita di sincronismo può avvenire per l’**inserimento o la cancellazione di un bit** a seguito di un **attacco attivo di un intruso sul testo cifrato che transita nel canale insicuro**. 
Da quel momento in poi **tutto il cifrato verrà decifrato in maniera non corretta**. 

*La modifica di un bit, invece, non ha effetti in termini di sincronismo e l’errore di decifrazione è confinato ai singoli bit che sono stati modificati*, ovvero **non si ha propagazione dell’errore**. 

Nei due casi appena citati, la **conseguenza** dell’attacco sarà una **non-corrispondenza tra il bit i-esimo del testo in chiaro e il bit i-esimo del flusso di chiave**, condizione necessaria per una corretta decifrazione. 

## Tipologie di cifrari a flusso
### Cifrari a flusso sincroni

> ***I bit del testo cifrato dipendono solamente dai bit di testo in chiaro e dai bit del flusso di chiave***

In questa modalità, i bit del flusso di chiave sono *indipendenti* dal bit del testo in chiaro. 

La cifratura e la decifrazione sono esprimibili tramite un automa a stati la cui funzione $F$ si occupa di produrre la chiave a partire dallo stato interno, e la cui funzione $G$ si occupa di calcolare lo stato futuro. Il seed può interessare sia la funzione $F$ che la funzione $G$, ma in ogni caso tale funzione deve essere <u>unidirezionale</u>.

> **Condizione necessaria per una corretta decifrazione è dunque quella di avere perfetto sincronismo tra mittente e destinatario nella generazione del flusso di chiave (ovvero le due funzioni $G$).**

Infatti, in caso di inserimento o cancellazione di un bit da parte di un attaccante, la trasmissione perde di sincronismo e dunque è costretta a ricominciare utilizzando un seed differente. Diverso è il caso riguardante la modifica di un bit, infatti, a destinazione, solo il bit corrispondente verrà tradotto male e quindi la modifica non ha la possibilità di essere propagata.

Esempi: RC4, A5

![cifrarioflussosincrono.png](/img/user/sicurezza-informazione-M/immagini/cifrarioflussosincrono.png)

### Cifrari a flusso autosincronizzanti

> ***I bit del testo cifrato dipendono dai bit del testo in chiaro e dai bit del flusso di chiave aleatorio, ma vengono influenzati dai bit aleatori precedentemente generati e memorizzati in un registro a scorrimento*** (*shift register*)

Il flusso di chiave dipende dal flusso dei bit del testo cifrato (notare i due registri a scorrimento), in questo modo l’**eventuale perdita di sincronismo tra i due comunicanti non richiede intervento tra le due parti** ma, *dopo un breve transitorio*, la cui durata dipende dalle dimensioni del registro utilizzato, *i due generatori si risincronizzano in quanto il registro sarà nuovamente pieno solo di dati corretti*. 

In questo caso è di fondamentale importanza l’unidirezionalità della funzione $F$.

Esempi: DES-CFB.

![cifrarioflussoautosinc.png](/img/user/sicurezza-informazione-M/immagini/cifrarioflussoautosinc.png)

