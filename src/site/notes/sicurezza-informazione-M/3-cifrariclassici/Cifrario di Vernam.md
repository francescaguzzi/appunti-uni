---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/cifrario-di-vernam/"}
---

#definizione 

Si parte come base dal [[sicurezza-informazione-M/3-cifrariclassici/Cifrario di Vigenere\|Cifrario di Vigenere]] e da una codifica binaria di 5 bit -> ogni carattere viene cifrato con un carattere ottenuto da un nastro molto lungo che ad ogni sostituzione avanza.

Stesso funzionamento del *cifrario di Vigenere* MA la chiave è memorizzata in un nastro a scorrimento molto lungo ed è ottenuta a partire dallo **XOR di una codifica binaria a 5 bit**.

Risulta **ancora vulnerabile** perchè la chiave comunque si ripeterà quando il nastro ricomincerà da capo.