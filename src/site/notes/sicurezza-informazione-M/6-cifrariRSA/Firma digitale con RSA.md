---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/firma-digitale-con-rsa/"}
---

#highpriority #modalitàcifratura 

Nel caso in cui venga utilizzato l'algoritmo RSA, ci sono diverse **proprietà** da analizzare.

## Proprietà di reversibilità delle chiavi

> **La proprietà di reversibilità del cifrario RSA consiste nella possibilità di utilizzar lo stesso algoritmo, cioè l’esponenziazione modulare, scambiando l’utilizzo delle chiavi, pubblica e privata, per poter eseguire rispettivamente sia la cifratura del messaggio sia per fornire il servizio di firma digitale.**

Oltre alla cifratura con chiave pubblica, l'algoritmo RSA è reversibile, **RSA a chiavi invertite (cifratura con chiave privata) è dunque un algoritmo di [[sicurezza-informazione-M/6-cifrariRSA/Firma digitale#^dac876\|firma con recupero]]**.

-> tale metodo è sicuro ma *inefficiente* -> un messaggio lungo deve essere suddiviso in blocchi $m < n$, e poi cifrato -> si può risolvere il problema cifrando soltanto l'impronta di $m$ -> l'impronta però ha lunghezza molto inferiore a quella del modulo ($m << n$) e ciò porta a vulnerabilità -> padding
 
## Proprietà moltiplicativa

>  Questa proprietà afferma che **la cifratura del prodotto di due messaggi è congrua (mod n) al prodotto dei due testi cifrati**. Analogamente, si ha che **la decifrazione di un testo cifrato ottenuto moltiplicando due testi cifrati è congrua (mod n) al prodotto dei due corrispondenti testi in chiaro**.

$$ E(m_1\cdot m_2) \equiv c_1 \cdot c_2 $$$$ D(c_1 \cdot c_2) \equiv m_1\cdot m_2$$ Questo è però anche alla base dell'<u>attacco con testo cifrato scelto</u>.

Un messaggio $m=m_1\cdot m_2$ (entrambi $<n$) ha come firma *il prodotto delle firme* di $m_1$ ed $m_2$ 

## Firma cieca

> **La proprietà moltiplicativa consente di eseguire la cosiddetta “firma cieca”** (o firma ad occhi chiusi o con messaggio oscurato). Tale tecnica risulta particolarmente utile nella situazione in cui **un utente X può richiedere ad un’autorità T di autenticargli (nel senso che T firma con la sua chiave privata) un messaggio m, di cui, però, non vuole rivelare il contenuto**.

-> casi come voto elettronico o commercio elettronico

1. `X` si fa autenticare da `T` un messaggio formato dal prodotto di `m` con un secondo messaggio `r` <u>generato apposta per oscurare m</u> (`r` coprimo con il modulo)
2. `T` potrà autenticare il ***messaggio oscurato*** $m\cdot r$ e `X` otterrà `m` autenticato 
		-> per la *proprietà di congruenza* basterà *moltiplicare il messaggio per l'inverso moltiplicativo di `r`*

