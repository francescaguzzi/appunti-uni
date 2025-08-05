---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/chiavi/"}
---

#definizione

Gli algoritmi crittografici, che siano utilizzati per esigenze di riservatezza o per l'autenticazione, usano **una chiave $k_s$ alla sorgente ed una chiave $k_d$ alla destinazione**. Si distinguono in due famiglie:
## Algoritmi simmetrici
$k_s$ e $k_d$ **sono uguali** oppure (raramente) facilmente calcolabili una dall'altra -> i cifrari simmetrici sono solitamente utilizzati per garantire la [[sicurezza-informazione-M/1-concettibase/Riservatezza\|Riservatezza]]
## Algoritmi asimmetrici
$k_s$ e $k_d$ sono **diverse ma biunivocamente legate** ed è molto difficile dedurre una chiave a partire dall'altra -> spesso una chiave viene tenuta privata ed una pubblica. 
Ogni entità possiede una coppia di chiavi; i cifrari asimmetrici garantiscono [[sicurezza-informazione-M/1-concettibase/Riservatezza\|Riservatezza]] ed [[sicurezza-informazione-M/7-identificazione/Identificazione\|Identificazione]]

> Per garantire riservatezza gli algoritmi simmetrici risultano più efficienti (rispetto agli asimmetrici)

>Per garantire autenticazione occorre usare un algoritmo asimmetrico