---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/cifrario-di-vigenere/"}
---

#definizione 

Sfrutta una griglia $26\times 26$ in cui in ogni riga si ripete l'alfabeto così:
- Nella prima riga partendo da A
- Nella seconda da B con A alla fine
- Nella terza da C con AB alla fine e così via fino ad avere l'alfabeto completo nella prima colonna e nella prima riga

Viene poi definita una chiave di caratteri alfabetici, che viene ripetuta più volte per far corrispondere a ogni carattere del messaggio uno della chiave. 

L’algoritmo di cifratura è così definito: 
1. Si considera la prima lettera del testo in chiaro e della chiave
2. Si usano queste lettere come coordinate cartesiane nella tavola
3. L’intersezione delle righe e colonne identificate fornisce il carattere da sostituire nel testo cifrato
4. Infine, si itera per tutta la lunghezza del testo

Questa tecnica permette quindi di avere una **sostituzione diversa per lo stesso carattere in punti diversi** (*polialfabetica*), usa una chiave di simboli del linguaggio naturale e di lunghezza finita, permettendo di avere sequenze di più caratteri cifrati con gli stessi caratteri della chiave.

Se la chiave è lunga $L$ caratteri, ogni $L$ simboli si userà la stessa sostituzione alfabetica -> il [metodo Kasiski](https://it.wikipedia.org/wiki/Metodo_Kasiski) *individua le sequenze ripetute considerando che il MCD tra le distanze di sequenze ripetute molto probabilmente è la lunghezza della chiave*. 

Possibili accorgimenti:
- Chiave lunga e casuale 
- Ogni simbolo del testo in chiaro influisce sul valore di tutti i blocchi del testo cifrato

Queste estensioni sono applicate nel [[sicurezza-informazione-M/3-cifrariclassici/Cifrario di Vernam\|Cifrario di Vernam]]