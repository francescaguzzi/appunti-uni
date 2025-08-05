---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/rete-di-feistel/"}
---

#algoritmo 

In una rete di Feistel, ogni blocco di testo in chiaro viene sottoposto ad un insieme di **round** che consistono in **diverse fasi di elaborazione che includono sostituzione e trasposizione del testo in chiaro in ingresso per trasformarlo nell’output**, ovvero il testo cifrato.

1. Si condivide una chiave tra sorgente e destinazione
2. Chiave -> algoritmo -> sottochiavi, ciascuna delle quali sarà data in pasto ai round
	   Si utilizza una sottochiave per ogni blocco
3. Si divide il blocco in parte destra meno significativa e parte sinistra più significativa
4. Parte più significativa -> XOR con funzione $F$ 
		$F$ ha come ingressi sottochiave e parte destra meno significativa
5. Il blocco di destra così diventa il più significativo, ed il risultato dello XOR di (4) verrà sottoposto alla funzione $F$
6. I blocchi di destra e sinistra si scambiano e viene utilizzata una nuova sottochiave

Alla fine ogni blocco passerà per ogni round.

La decifrazione avviene dando in pasto all’algoritmo le sottochiavi in maniera inversa, cioè a partire dall’ultima utilizzata in fase di cifratura. L’algoritmo che esegue la cifratura e la decifratura è lo stesso.

![retefeistel.png](/img/user/sicurezza-informazione-M/immagini/retefeistel.png)