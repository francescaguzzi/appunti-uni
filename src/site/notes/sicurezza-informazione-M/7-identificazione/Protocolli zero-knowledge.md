---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/7-identificazione/protocolli-zero-knowledge/"}
---

#progetto #lowpriority #identificazione #protocollo 

-> [[libroscreenzeroknowledge.png]]

Questa tipologia di protocolli mira ad eliminare un difetto intrinseco dei protocolli sfida/risposta, ovvero che qualunque sia la trasformazione impiegata il **dato segreto deve** comunque, in una forma o nell’altra, **partecipare alla comunicazione** e quindi <u>non è mai completamente sicuro</u>. 

Questi protocolli permettono all’identificando di essere riconosciuto dando soltanto **una prova della conoscenza del segreto**, **senza effettivamente utilizzarlo nello scambio dei messaggi**. 

Per fare ciò l’identificando **dichiara di saper risolvere un problema difficile** (per il quale però esiste un algoritmo di verifica con tempo polinomiale) e **lo dimostra al verificatore facendogli vedere di essere in grado di risolvere un diverso ed isomorfo problema difficile** che ha in precedenza concordato con una terza parte fidata. 

L’interazione tra i due corrispondenti prevede tipicamente tre passi:
1. L’identificando fornisce una testimonianza di quello che asserisce di saper fare
2. Il verificatore gli lancia una sfida che consente di giudicare la veridicità della testimonianza
3. L’identificando invia la risposta alla sfida ed il verificatore controlla se è corretta

Al termine dei tre passi può esserci il dubbio che l’identificando abbia dato la risposta corretta “tirando ad indovinare”: per rendere piccola la probabilità di questo evento, <u>i tre passi devono essere ripetuti più volte</u>.

