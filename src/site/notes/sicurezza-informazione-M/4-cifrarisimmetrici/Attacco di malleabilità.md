---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/attacco-di-malleabilita/"}
---

#attacchi 

L’attacco di malleabilità è un **attacco attivo attuabile soltanto sui [[sicurezza-informazione-M/4-cifrarisimmetrici/Cifrari a flusso\|cifrari a flusso]]**; quest’ultimi ne sono infatti vulnerabili in quanto dedicati alla riservatezza, senza occuparsi di garantire [[sicurezza-informazione-M/1-concettibase/Integrità\|integrità]]. 

L’attacco si basa nello **sfruttare la seguente proprietà dello XOR** che afferma che **i termini uguali si elidono**:
$$a \oplus b \oplus a = b$$
Per cui un attaccante potrebbe **modificare il testo cifrato** per far in modo che arrivi a destinazione un messaggio voluto dall'attaccante.
Perchè questo tipo di attacco posa essere eseguito:
- l'intruso deve poter eseguire **attacchi attivi**
- l'intruso deve avere **informazioni pregresse sul contenuto del messaggio**
- il messaggio cifrato scambiato deve essere **fortemente strutturato** e l'intruso deve **conoscere questa struttura**

> ***Se una parte del testo è predicibile un cifrario a flusso è malleabile***

-> nei cifrari a flusso <u>non è previsto nessun meccanismo di rilevamento delle modifiche</u>
