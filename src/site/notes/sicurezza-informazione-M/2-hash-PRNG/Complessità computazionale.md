---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/complessita-computazionale/"}
---

#definizione 

Nel caso della sicurezza, ci si concentra principalmente sul tempo per valutare se un algoritmo è facile o difficile; tuttavia, sussiste il problema per cui ogni macchina ha una potenza diversa; quindi, l’unità di misura non potrà essere il tempo stesso, ma occorrerà un’unità indipendente dalla piattaforma.

Si considera per questo scopo il **numero N di operazioni necessarie per completare l’algoritmo dati n bit in ingresso**. Si può esprimere il numero di operazioni come:$$ N = f(n)$$Per garantire le proprietà di sicurezza occorre che gli **algoritmi atti alla difesa** delle informazioni abbiano un **tempo di esecuzione polinomiale** $$T = O(t^n)$$ altrimenti i legittimi proprietari non riuscirebbero ad accedere ai dati; viceversa, gli **algoritmi per violare le proprietà** dovranno avere un **tempo di esecuzione esponenziale** o sub-esponenziale 
$$T= O(n^t) \ \text{oppure} \ T=O(\exp n)$$
### MIPS 
Un MIPS è la velocità di un computer di riferimento in grado di fare un milione di operazioni al secondo; un anno MIPS è il numero di operazioni eseguibili in un anno lavorando a 1 MIPS.

>La soglia di sicurezza si alza con l’avanzamento della tecnologia passando da 80 bit delle chiavi simmetriche degli anni ’90 ai 128 bit necessari ad oggi.

### Livello di sicurezza
#definizione 
Seconda unità di misura nata per svincolarsi dal progresso tecnologico. 

> Si definisce livello di sicurezza **il numero n di bit minimo per cui l'algoritmo di brute force risulti computazionalmente complesso
