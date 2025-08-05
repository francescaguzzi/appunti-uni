---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/cifrario-di-playfair/"}
---

#definizione 

Matrice $5\times 5$ contenente la chiave e le restanti lettere dell'alfabeto (di solito lettera j sostituita con lettera i)

Si divide il messaggio in diagrammi, con eventuale padding X; -> se nel diagramma ci sono lettere doppie -> X (es: bb -> bx)

Una volta generata questa matrice quadrata la cifratura avviene nel seguente modo: 
1. Il testo in chiaro viene suddiviso in gruppi di due lettere.
2. Per ogni gruppo si cercano nella matrice le due lettere e si sostituiscono con altre due secondo le seguenti regole:
	- Se le due lettere sono in **righe e colonne diverse**, si prendono le due che fanno rettangolo con esse
	- Se le due lettere si trovano sulla **stessa riga**, si sostituiscono con le due lettere che le seguono a **destra**
	- Se le due lettere sono sulla **stessa colonna**, si prendono le due lettere **sottostanti**

La matrice, essendo segreta, conterrà la chiave che sarà scritta al suo interno, ogni lettera doppia non viene scritta e dopo la chiave si scrivono le rimanenti lettere in ordine alfabetico prestando attenzione alle ripetizioni che vanno tolte.

