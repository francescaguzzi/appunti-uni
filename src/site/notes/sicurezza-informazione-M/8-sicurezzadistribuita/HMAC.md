---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/8-sicurezzadistribuita/hmac/"}
---

#lowpriority #algoritmo #modalitàcifratura 

L'**HMAC** (_Hash-based Message Authentication Code_) è un meccanismo crittografico utilizzato per garantire **l'integrità** e **l'autenticità** dei dati trasmessi.

### **Funzionamento dell'HMAC

L'HMAC viene calcolato sui dati frammentati prima della cifratura. Ecco come funziona:

1. **Input**:
    
    - **Messaggio in chiaro**: I dati applicativi (es. una porzione di HTTP).
        
    - **Chiave segreta condivisa**: Derivata durante l'handshake (es. dalla `master secret`).
        
    - **Algoritmo hash**: Solitamente SHA-256 o SHA-384 (a seconda della cipher suite negoziata).
        
2. **Calcolo dell'HMAC**:
    
    - Viene generato un codice (detto _tag_ o _autenticatore_) combinando il messaggio e la chiave segreta con una funzione hash.

### **Perché Usare l'HMAC?**

- **Integrità**: Assicura che i dati non siano stati modificati durante la trasmissione.
    
- **Autenticità**: Conferma che i dati provengono dal mittente legittimo (grazie alla chiave segreta condivisa).
    
- **Resistenza agli attacchi**: Anche se un attaccante modifica il messaggio, senza conoscere la chiave segreta non può generare un HMAC valido.

### **Differenze Tra HMAC e MAC Standard**

|Caratteristica|HMAC|MAC Standard|
|---|---|---|
|**Resistenza agli attacchi**|Più robusto (usa hash + chiave)|Dipende dall'algoritmo|
|**Algoritmi tipici**|SHA-256, SHA-384|CBC-MAC, CMAC|
|**Complessità**|Doppio hashing|Singola operazione|
