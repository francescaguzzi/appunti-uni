---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/1-concettibase/attacchi-informatici/"}
---

#attacchi #lowpriority 
# Esempi di attacchi 
## Spoofing 
Consiste nell'**impersonare un'altra entità**. La tipologia più comune è l'*IP spoofing*, dove viene sfruttato il fatto che il protocollo TCP/IP non verifica se sia stato modificato l’indirizzo del mittente durante l’instradamento; quindi, un’entità potrebbe modificarlo spacciandosi per una macchina diversa da quella che è in realtà -> mina l'[[sicurezza-informazione-M/1-concettibase/Autenticità\|autenticità]]
## Denial of Service
Es. *Ping of Death*, *SYN Flooding* -> consiste nell'**impedire ad una macchina di erogare un servizio agli utenti autorizzati** minandone quindi la [[sicurezza-informazione-M/1-concettibase/Disponibilità\|disponibilità]]. L’attacco *SYN Flooding* consiste nell’inondare un server di richieste di handshake per stabilire una connessione, fino a riempire le code di attesa per i pacchetti SYN. Così facendo il server inizia a scartare i pacchetti SYN degli utenti legittimi impedendo di fatto la comunicazione.
### Distributed Denial of Service
Il funzionamento di base è identico a quello di un attacco DOS locale, ma in questo caso l’attacco è attuato da un Botnet, cioè un insieme di macchine connesse in rete precedentemente infettate e di cui l’attaccante ha il controllo.
## Hijacking
Consente di dirottare la comunicazione.
## Malware
Esecuzione di programmi malevoli -> virus, trojan horse, worm etc.
## Data-Sniffing
Tecnica che mina la [[sicurezza-informazione-M/1-concettibase/Riservatezza\|confidenzialità]] della comunicazione e consente di intercettare dati
## Scanning delle porte
Consiste nell’eseguire una scansione delle porte aperte su un nodo di rete per poi poter pianificare un attacco, anche in virtù delle vulnerabilità conosciute. Diventato di recente una pratica perseguibile se eseguita su nodi non autorizzati.
## Buffer Overflow
Permette l’esecuzione di codice arbitrario iniettato tramite input correttamente manipolato.

----
# Tipologie di attacchi
Il modello dato per assunto durante il corso è quello del ***canale insicuro***, esso consiste in una infrastruttura distribuita composta da sorgente e destinazione, entrambe con hardware e sistema operativo sicuri, che comunicano attraverso un canale insicuro. 
{ #288f9d}


Sul canale un intruso può attuare due tipologie base di attacchi:
## Attacchi passivi
L'intruso non agisce sul flusso di comunicazione, ma si limita ad analizzarlo alla ricerca di informazioni -> mina la [[sicurezza-informazione-M/1-concettibase/Riservatezza\|confidenzialità]] 
Possibili contromisure di tipo preventivo:
- ***Rendere il canale incomprensibile*** -> [[sicurezza-informazione-M/3-cifrariclassici/Cifrari classici\|Cifrari classici]]
- ***Controllare l'accesso al canale*** -> non scalabile e non attuabile in rete -> internet non è dotato di controllo degli accessi
## Attacchi attivi
L'intruso agisce direttamente sui dati che transitano nel canale modificandoli, eliminandoli o aggiungendoli con sorgente camuffata -> mina [[sicurezza-informazione-M/1-concettibase/Disponibilità\|disponibilità]], [[sicurezza-informazione-M/1-concettibase/Autenticità\|autenticità]] e [[sicurezza-informazione-M/1-concettibase/Integrità\|integrità]] dei dati- 
Principali contromisure: 
- ***Controllare l'accesso al canale*** (come sopra)
- ***Generare attestati di integrità e origine***
