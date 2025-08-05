---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/cifrari-asimmetrici/"}
---

#concetto 

La crittografia a chiave pubblica si basa sull’uso di **problemi difficili della matematica**, ovvero problemi per i quali **non si troveranno mai algoritmi con tempo polinomiale se si usano le funzioni nel “verso sbagliato”** e su insiemi numerici dotati di regole precise, al fine di garantire la robustezza del cifrario.

Tra i **problemi difficili principali** ritroviamo:

- **Logaritmo discreto** -> dato un numero primo $p$, un generatore $g$, un intero $x$ e un $y = g^x (\mod p)$ trovare l'intero $x$ è un problema difficile
	-> utilizzato nel [[sicurezza-informazione-M/4-cifrarisimmetrici/Protocollo Diffie-Hellman\|Protocollo Diffie-Hellman]] 

- **Radice e-esima** -> dato un $n$ prodotto di due primi, un $e$ coprimo con $\Phi(n)$ e un elemento $c$, trovare un intero $m \equiv
{ #e}
\sqrt{c}$  è un problema difficile 
	-> utilizzato nel [[sicurezza-informazione-M/6-cifrariRSA/Cifrario RSA\|Cifrario RSA]] 
	-> il problema risulta **facile** se si conoscono i fattori di $n$ o se $n$ è primo

- **Problema della fattorizzazione** -> dato un intero positivo $n$, trovare i numeri primi $p_i$ e i coefficienti interi $$ e_i \ge 1 : n =p_1e_1 \cdot ... \cdot p_ke_k$$ è un problema difficile (crittografia asimmetrica = $p_1 \cdot p_2$)
	-> utilizzato nel [[sicurezza-informazione-M/6-cifrariRSA/Cifrario RSA\|Cifrario RSA]]

> ***I cifrari simmetrici sono più veloci rispetto a quelli asimmetrici*** -> i primi utilizzano sostituzioni e permutazioni, i secondi l'esponenziale modulare -> risultano mille volte più lenti -> si utilizzano per messaggi corti (chiave di un cif. simmetrico)

Per questo motivo, si può scegliere di utilizzare piuttosto un [[sicurezza-informazione-M/6-cifrariRSA/Cifrario Ibrido\|Cifrario Ibrido]].
