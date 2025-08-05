---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/appendice-matematica/"}
---

#lowpriority 

---
#### Numero primo di Sophie Germain

Numero primo $q$ tale che $2q+1$ è anch'esso un numero primo -> il numero $2q+1$ invece è detto *numero primo sicuro*

--- 
#### Esponenziale modulare

Operazione molto costosa -> <u>ad ogni moltiplicazione il range di valori aumenta e l'efficienza degrada</u>
Per ridurre il numero di operazioni occorre sfruttare le <u>proprietà dei generatori di gruppi ciclici</u> $$g^{53}=g^{32}g^{16}g^4g^1$$

--- 
#### Algoritmo Repeated Squaring

Per calcolare $b^e n(\mod m)$ 
1. Si converte in binario $e$
2. Si calcolano i $b_i$ con $i$ i soli bit dell'esponente non a 0
3. Si moltiplicano tra loro e si calcola il modulo secondo $m$

**Se l’esponente ha tutti i bit impostati a 1 non si ha alcun miglioramento, ma se alcuni sono impostati a 0 si ha una riduzione del numero di moltiplicazioni** (riferimento all’esempio 53=110101).

---
#### Algoritmo Repeated Square and Multiply

Anch’esso si basa su quanto appena illustrato, ma **permette di ridurre ulteriormente il range di valori utilizzati**. Ciò è ottenuto eseguendo l’operazione di modulo ad ogni moltiplicazione, sia del risultato parziale, sia del valore corrente, invece che solo alla fine.


---
#### Test di primalità di Miller-Rabin

Questo algoritmo (che ha un tempo di esecuzione polinomiale) si basa sul brute-force. 
1. Viene generato un numero dispari molto grande
2. Se tale numero non è primo, **si comincia ad iterare nell’intorno del numero scelto** fino a trovare un numero primo
3. Nel caso in cui il numero non è primo, si ripete iterativamente il processo dopo averlo **incrementato di 2**

In base al numero iniziale dispari molto grande scelto, varierà il tempo e la difficoltà di esecuzione: più il numero sarà grande più l’esecuzione richiederà tempo.

---



