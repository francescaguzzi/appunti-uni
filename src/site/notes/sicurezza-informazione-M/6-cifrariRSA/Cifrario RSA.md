---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/cifrario-rsa/"}
---

#modalitàcifratura #highpriority 

È stato il primo cifrario asimmetrico ad essere individuato. È **deterministico**, **opera a blocchi** ed è universalmente considerato sicuro.

Ha le seguenti caratteristiche:

1. **Frammentazione del testo in chiaro** -> per garantire che vi sia una corrispondenza biunivoca tra il testo in chiaro e il cifrato <u>non devono esserci collisioni</u> -> *uno stesso messaggio cifrato non deve essere riconducibile a più messaggi in chiaro*
	Dal momento in cui si opera tramite *algebra modulare*, occorre garantire le **proprietà**:
	- **Il testo in chiaro deve essere frammentato in blocchi di valore strettamente minore del modulo. Se così non fosse, potrebbe accadere che messaggi in chiaro diversi producano lo stesso testo cifrato.**
	- Bisogna porre attenzione per quanto riguarda i **messaggi più corti del modulo**; infatti, questi possono essere particolarmente **vulnerabili ad attacchi a forza bruta**; pertanto, bisogna inserire un **padding**.
	Ad esempio, con un messaggio di 60 bit e RSA con 1024 bit di chiave -> molto più corto -> va inserito padding perchè ha una dimensione minore di 128bit

2. ***Aleatorietà del testo cifrato*** -> l'<u>algoritmo RSA è deterministico</u> per cui è necessario rendere aleatorio il testo in chiaro per evitare che si possa dedurre qualcosa dal cifrato
	- Si può **concatenare un numero casuale** al messaggio in chiaro prima di cifrarlo
	- Sfruttando il [[sicurezza-informazione-M/6-cifrariRSA/Padding OAEP\|Padding OAEP]]

3. **Si basa su una trasformazione che è variabile nel tempo**

4. **Si basa su problemi difficili della teoria dei numeri** -> in questo caso sul *problema della fattorizzazione* e di *estrazione della radice e-sima di un numero*

5. **Proprietà di reversibilità** -> indica che il cifrario RSA può essere usato per:
	- garantire **riservatezza dei dati** -> cifrare e decifrare
	- **garantire autenticazione**
	- **firmare digitalmente** -> [[sicurezza-informazione-M/6-cifrariRSA/Firma digitale con RSA\|Firma digitale con RSA]]

6. **Caratterizzato da due algoritmi:**
	- Un algoritmo $G$ per la generazione delle chiavi
	- Un algoritmo $E$ di *encryption*, che corrisponde anche all'algoritmo di *decryption*

---
# Cifratura

Si suddivide il messaggio in blocchi $m$ di $k$ bit, con $$2^k < n \le 2^{(k+1)}$$ quindi si cifra ogni blocco come $$c = m^e(\mod n)$$ L'operazione inversa a quest'ultima è la radice e-esima, che risulta essere computazionalmente complessa.

---
# Decifrazione

Si può eseguire l'esponenziazione $$m=c^d(\mod n)$$ che permette di ottenere il testo in chiaro -> $d$ **inverso moltiplicativo** di $e$. 
Ciò è vero perchè si dimostra, se $m<n$, che -> $c^d\mod n \equiv m^e \mod n \equiv m$

---
# Generazione della coppia di chiavi in RSA
#highpriority 

Si procede come segue:
1. Si generano due numeri primi (che devono rimanere segreti) molto grandi $p$ e $q$ 
2. Si calcola $n = p \cdot q$
3. Si calcola $\Phi (n) = (p-1)(q-1)$ -> *funzione toziente di Eulero*
4. Si cerca un intero $e$ **coprimo con $\Phi(n)$** e compreso tra $1$ e $\Phi(n)$ 
5. Si calcola $d$ -> **inverso moltiplicativo di $e$** -> $d=e^{-1}(\mod \Phi(n))$ 
6. Si ottengono le due chiavi:
	- **Pubblica** -> **`k[pub] = (n,e)`**  -> numero $n$ ed $e$ coprimo di $\Phi(n)$ 
	- **Privata** -> **`k[priv] = (n,d)`** -> numero $n$ e l'inverso moltiplicativo $d$ di $\Phi(n)$ 

(*numeri coprimi* -> unico divisore in comune è 1)

***Calcolo di e*** -> si utilizza l'**algoritmo esteso di Euclide**
***Calcolo di n*** -> siccome $n$ è il prodotto di due numeri primi grandi, si utilizza il [[sicurezza-informazione-M/6-cifrariRSA/Appendice matematica#Test di primalità di Miller-Rabin\|test di primalità di Miller-Rabin]]. 

Per la cifratura si utilizza la tecnica [[sicurezza-informazione-M/6-cifrariRSA/Appendice matematica#Algoritmo Repeated Square and Multiply\|Repeated Square and Multiply]] -> si utilizza come valore di $e=65537$ perchè la sua **rappresentazione binaria ha pochi 1** -> maggior efficienza nel calcolo di $m^e$ -> per il RSAM meno 1 ci sono più le moltiplicazioni sono veloci.

---
# Sicurezza di RSA

Il proprietario della chiave privata deve tenere segreti $d$ e i fattori $p$ e $q$ di $n$ (tipicamente questi ultimi due <u>vengono distrutti dopo la generazione delle chiavi</u>). 

Se l’attaccante non conosce p e q (e, p, q sono numeri primi molto grandi) deve risolvere un problema di fattorizzazione del quale non si conoscono ancora algoritmi polinomiali in grado di risolverlo. 

In ogni caso, sono sempre possibili attacchi di:
- ***Forza bruta*** -> tranne se chiave pubblica > 128bit -> si usano chiavi di almeno 2048 bit
- ***Attacchi matematici*** -> attacco di fattorizzazione per calcolare $p$ e $q$ o per trovare $\Phi(n)$ 
- ***Attacco a tempo*** -> si analizza tempo di decifrazione per avere informazioni sulla chiave
	- soluzione: **Blinding*** -> trasformazione del testo cifrato per offuscarlo
- ***Attacchi con testo cifrato scelto*** -> *l'intruso sceglie del testo cifrato e induce l'entità a decifrarlo* -> va risolto il determinismo (vedi sopra - concatenazione di numero casuale e padding OAEP)

---


