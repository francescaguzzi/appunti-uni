---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/master-key/"}
---

#gestionechiavi

Questa soluzione permette di creare un **sistema scalabile per la distribuzione in maniera automatica delle chiavi segrete per ogni sessione**.

Infatti, ad ogni sessione, è necessario che A e B condividano una chiave segreta in modo da potersi inviare dati cifrati a vicenda. Però, se A e B comunicano molto frequentemente, non è verosimile che siano state scambiate in precedenza una moltitudine di chiavi già prefissate.

L'architettura Master Key prevede quindi che **le entità siano già in possesso di un segreto condiviso, chiamato Master Key**, che non viene utilizzato per cifrare messaggi. 

Per preservare questo segreto si faranno circolare il minor numero di testi cifrati possibili prodotti con l’uso della Master Key. I messaggi verranno infatti cifrati con delle chiavi, dette **Session Key**, che verranno distribuite all’altra entità in forma cifrata grazie all’uso della Master Key. 

**La Master Key, quindi, avrà vita più lunga possibile e verrà usata solo per cifrare chiavi di sessione**. **La chiave di sessione invece verrà cambiata spesso** per evitare che un intrusore possa intercettare un alto numero di testi cifrati con la stessa chiave e possa dedurre qualche informazione.

Il funzionamento del sistema:
1. All'inizio di ogni sessione -> A e B condividono **una sola chiave**, la **master-key**
2. A genera con un [[sicurezza-informazione-M/2-hash-PRNG/Random Number Generator (RNG)#Pseudo Random Number Generator Cryptographically Secure (PRNGCS)\|PRNG crittograficamente sicuro]] una **chiave di sessione `k`**
3. **A invia a B** la chiave di sessione `k` (*cifrata con la master-key*) insieme al messaggio cifrato con `k`
4. B **decifra la chiave di sessione `k` con la master-key** e una volta ottenuta `k` potrà decifrare il messaggio inviato da A

> SOSTANZIALMENTE Si usa master key per cifrare session key che cifrano messaggi e per decifrare le session key si usa la master key 

***Problemi***:
- Come scambiare in modo sicuro la master-key?
- Se si vuole comunicare con $N$ utenti, **ogni utente dovrà memorizzare $N-1$ master key diverse**
	Nel sistema si avrebbero un totale di $\frac{N(N-1)}{2}$ chiavi
		-> soluzione non scalabile, crescita esponenziale delle chiavi all'aumentare degli utenti 
		-> il [[sicurezza-informazione-M/4-cifrarisimmetrici/Key Distribution Center (KDC)\|Key Distribution Center (KDC)]] cerca di migliorare questo problema


