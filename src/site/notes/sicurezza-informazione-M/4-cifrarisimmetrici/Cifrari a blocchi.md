---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/cifrari-a-blocchi/"}
---

#definizione 

Sono cifrari che ricordano il [[sicurezza-informazione-M/3-cifrariclassici/Cifrario di Playfair\|Cifrario di Playfair]] (con regole di sostituzione e permutazione sui blocchi del testo in chiaro al fine di ottenere confusione e diffusione). 

Trasformano i dati **in blocchi di grandezza variabile** applicando ad ognuno di essi la medesima trasformazione, a differenza dei cifrari a flusso che cifrano ad un solo bit alla volta. La grandezza è variabile da cifrario a cifrario, ma rimane la stessa per lo stesso testo in chiaro.

Risultano particolarmente adatti per:
- proteggere **strutture dati**
- operare in **applicazioni asincrone** -> per esempio per cifrare molti dati che non necessitano di essere decifrati subito

Esempi di cifrari a blocchi: DES, 3-DES, [[sicurezza-informazione-M/4-cifrarisimmetrici/AES (Advanced Encryption Standard)\|AES (Advanced Encryption Standard)]] (standard attuale con chiave di 128 bit).

DES e TDES si basano sul modello della [[sicurezza-informazione-M/4-cifrarisimmetrici/Rete di Feistel\|Rete di Feistel]].

> ***DES, 3-DES e AES sono metodi di cifratura
> CBC e simili sono protocolli di implementazione delle funzioni di cifratura***

### Cifratura
Il messaggio originale viene suddiviso **in blocchi di grandezza variabile**, il cui numero varia a seconda dell’algoritmo. Ad ogni blocco viene quindi applicata la **stessa trasformazione**, secondo una **chiave di lunghezza finita abbastanza lunga** da rendere impossibile un attacco di forza bruta (ad oggi **almeno di 128 bit**). L’**ultimo blocco** può essere completato da dei **bit di informazione** ed eventualmente con **bit di padding**, è possibile usare diversi tipi di padding, questi non sono tutti uguali, solitamente si scelgono quelli standard per una sicurezza migliore.

Un cifrario a blocchi fornirebbe *sempre lo stesso testo cifrato per gli stessi dati e la stessa chiave*; sarebbe quindi vulnerabile agli attacchi di tipo “testo in chiaro scelto” (*chosen plaintext*).

Per questo motivo, i cifrari a blocchi vengono utilizzati solo in ***modalità operative specifiche*** che eseguono un’**elaborazione aggiuntiva** per aumentare la sicurezza:
- [[sicurezza-informazione-M/4-cifrarisimmetrici/ECB (Electronic Code Book)\|ECB (Electronic Code Book)]] -> padding
- [[sicurezza-informazione-M/4-cifrarisimmetrici/CBC (Cipher Block Chaining)\|CBC (Cipher Block Chaining)]] -> padding 
- [[sicurezza-informazione-M/4-cifrarisimmetrici/CFB (Cipher Feedback)\|CFB (Cipher Feedback)]] -> no padding
- [[sicurezza-informazione-M/4-cifrarisimmetrici/OFB (Output Feedback)\|OFB (Output Feedback)]] -> no padding 
- [[sicurezza-informazione-M/4-cifrarisimmetrici/CTR (Counter)\|CTR (Counter)]] -> no padding 

### Decifrazione
Si suddivide nuovamente il testo cifrato in blocchi, **ognuno decifrato con una stessa trasformazione** (inversa di quella di cifratura), pilotata dalla stessa chiave usata per cifrare. Applicando la stessa chiave a diversi blocchi, ha un funzionamento simile ad un [[sicurezza-informazione-M/3-cifrariclassici/Cifrari poligrafici\|cifrario polialfabetico]].
