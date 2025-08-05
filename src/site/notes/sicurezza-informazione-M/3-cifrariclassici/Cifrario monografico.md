---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/cifrario-monografico/"}
---

#definizione 

Consiste nella **sostituzione di ogni lettera del testo con una corrispondente in un alfabeto noto alle sole parti legittime**, che costituisce la *chiave di sostituzione*. 
Dato un alfabero di $n$ simboli, si ottengono (al massimo) $n!$ trasformazioni. 

Esempi -> *Cifrario di Cesare*: $s = s +k$ con $k$ chiave
		  *Cifrario astash*: scambio prima->ultima, seconda->penultima

La sostituzione monoalfabetica è vulnerabile però ad [[sicurezza-informazione-M/3-cifrariclassici/Cifrario monografico#Attacchi statistici\|attacchi statistici]].
Questa tecnica non è quindi sicura in quanto ***il risultato della sua applicazione non è per nulla aleatorio e mantiene la distribuzione dei caratteri del messaggio in chiaro***. 

Una parziale soluzione consiste nel cifrare coppie o triple di lettere (o gruppi di lettere, però di pochi elementi), ovvero [[sicurezza-informazione-M/3-cifrariclassici/Cifrari poligrafici\|Cifrari poligrafici]]. Anche queste tecniche, sebbene offrano una resistenza maggiore, possono essere sottoposte ad analisi statistiche riguardanti i digrammi ed i trigrammi.

## Attacchi statistici
#attacchi 

I caratteri hanno una **frequenza precisa** con cui appaiono, e se il testo è abbastanza lungo, <mark style="background: #D2B3FFA6;">è possibile calcolare la percentuale dei caratteri</mark>, confrontarla con la frequenza dei caratteri del linguaggio originale e ottenere la corrispondenza. 

