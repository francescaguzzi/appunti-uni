---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/funzioni-di-hash/"}
---

#definizione 

>Le funzioni di hash sono funzioni che **accettano in ingresso una stringa x di lunghezza arbitraria** e generano un'uscita chiamata **impronta** (*fingerprint*) indicata con $H(x)$ e di lunghezza predefinita

Per definire una funzione di hash **crittograficamente sicura**, essa deve essere:
1. **Efficiente** -> calcolo di $H(x)$ facile per ogni $x$

2. ***Debolmente robusta alle collisioni*** (<u>resistenza debole</u>)
	*"Per ogni $x$ deve essere computazionalmente difficile trovare un $y\not=x$ tale che $H(y)=H(x)$"*
		Supponiamo di avere una funzione hash che, dati $n$ bit di input restituisce una delle sue possibili $2^n$ permutazioni in maniera equiprobabile
			Vogliamo trovare la dimensione $n$ dell'impronta che permette all'attaccante di trovare una collisione con una probabilità > 50%
				Si utilizza il **teorema binomiale** -> il numero di tentativi dipende da $n$ stesso -> num tentativi = $2^n$ stesso
					Bastano quindi **320 bit di impronta per garantire la resistenza debole** alle collisioni
{ #ecd5a4}

				
3. ***Fortemente robusta alle collisioni*** (<u>resistenza forte</u>)
	*"Data un'impronta $H(x)$ deve essere computazionalmente difficile per un intrusore risalire all'input $x$ che l'ha generata"*
		-> Deve essere computazionalmente difficile trovare una qualsiasi coppia $(x;y)$ tale che $H(x)=H(y)$ 
			In genere **è più facile trovare una collisione che viola la resistenza forte piuttosto che quella debole** -> si dimostra ciò tramite il [[sicurezza-informazione-M/2-hash-PRNG/Paradosso del compleanno\|Paradosso del compleanno]] 
			
4. **Unidirezionale** -> data un'impronta $H(x)$ deve essere computazionalmente difficile per un intrusore risalire all'input $x$ che l'ha generata

Quasi tutti gli algoritmi di hash si basano sul [[sicurezza-informazione-M/2-hash-PRNG/Principio di compressione iterata\|Principio di compressione iterata]].