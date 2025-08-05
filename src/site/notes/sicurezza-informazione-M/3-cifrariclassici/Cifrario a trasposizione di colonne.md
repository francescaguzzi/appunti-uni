---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/cifrario-a-trasposizione-di-colonne/"}
---

#definizione 

Questa tecnica consiste nello **scrivere il testo all’interno di una matrice** (un carattere per colonna). Viene poi concordata una **sequenza di valori** (possibilmente casuali) che permettono di **numerare univocamente le colonne**. Il testo viene poi riscritto in forma piana leggendo le colonne dalla prima all’ultima (secondo la numerazione data dal numero casuale)

- Frase in una tabella $P \times Q$ 
- Chiave -> codice numerico cifre $1 \to Q$
- $X$ di padding per celle rimanenti

Per ricostruire il testo di partenza si può cercare di capire *quali diagrammi non sono naturali ma derivano dalla scrittura in colonne del testo in chiaro*. 