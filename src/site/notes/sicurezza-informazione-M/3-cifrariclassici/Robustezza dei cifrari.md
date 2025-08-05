---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/robustezza-dei-cifrari/"}
---

#proprietà 

Per creare un cifrario robusto, dobbiamo tenere conto di due proprietà:
## Confusione

>  ***Nasconde la relazione esistente tra testo in chiaro e testo cifrato e rende poco efficace lo studio del secondo basato su statistiche e ridondanze del primo***

Rende quindi difficile prevedere che cosa accadrà al testo cifrato anche modificando un solo simbolo del testo in chiaro. **<u>La sostituzione è il mezzo più semplice ed efficace per creare confusione</u>**.

## Diffusione

> ***Nasconde la ridondanza del testo in chiaro spargendola all’interno del testo cifrato***

Si impone ad ogni simbolo del testo in chiaro di influire su molti se non tutti i simboli del testo cifrato. Rende difficile prevedere quali e quanti bit si modificano se si modifica anche un solo simbolo del testo in chiaro. <u>La trasposizione è il mezzo più semplice ed efficace per ottenere diffusione</u>.

### Principio di Shannon
#### Cifrario composto

> Stadi di sostituzione **alternati** a stadi di trasposizione