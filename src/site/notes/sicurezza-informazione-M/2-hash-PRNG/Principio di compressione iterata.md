---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/principio-di-compressione-iterata/"}
---

#definizione  #algoritmo 
# Schema di Merkle-Damgard

> *Suddivide il risultato in blocchi di dimensioni fisse e li processa uno alla volta con la funzione di compressione, ogni volta combinando l'input con l'output del blocco precedente*

Questo schema prevede i seguenti step:
1. Il messaggio viene **suddiviso in blocchi** con **lunghezza prefissata di $n$ bit** 
	-> le funzioni di compressione non sono in grado di gestire input di dimensioni arbitrarie
2. Ogni blocco viene processato con la *funzione di compressione unidirezionale* $f$
	 -> si occupa di trasformare due input di lunghezza fissa in un output della stessa dimensione degli input di partenza
3. Per ogni blocco del messaggio, la funzione di compressione $f$ prende il risultato fin'ora ottenuto e lo combina con il blocco corrente producendo un risultato intermedio
4. Eventualmente ***padding***
5. L'**ultimo blocco dipende indirettamente quindi da tutte le impronte dei blocchi precedenti** 
L'algoritmo parte con un valore iniziale fisso, denominato **vettore di inizializzazione** (IV) 

![compressioneiterata.png](/img/user/sicurezza-informazione-M/immagini/compressioneiterata.png)

> La popolarità di questa costruzione è dovuta al fatto (provato da Merkle e Damgård) che se la funzione di compressione unidirezionale $f$ è [[sicurezza-informazione-M/2-hash-PRNG/Funzioni di Hash#^ecd5a4\|resistente alle collisioni]], allora lo sarà anche la funzione di hash costruita utilizzando tale modello.

Per garantire quanto sopra è anche necessario utilizzare un **appropriato schema di *<mark style="background: #D2B3FFA6;">padding</mark>***-> vengono aggiunti all'ultimo blocco dei bit di riempimento che rappresentano la lunghezza dell'intero messaggio -> ciò può portare alla nascita di nuove vulnerabilità, perchè per esempio se un messaggio è soltanto numerico può risultare difficile distinguere il contenuto dal padding

Questo schema è particolarmente vulnerabile ad [[sicurezza-informazione-M/2-hash-PRNG/Attacco di estensione di lunghezza\|Attacco di estensione di lunghezza]].