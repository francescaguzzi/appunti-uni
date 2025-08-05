---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/attacco-di-estensione-di-lunghezza/"}
---

#attacchi #highpriority 

Il ***lenght-extension attack*** può essere eseguito:
- Sulle funzioni di hash implementate secondo il [[sicurezza-informazione-M/2-hash-PRNG/Principio di compressione iterata\|Principio di compressione iterata]]
- Nel caso in cui l'attaccante intercetti un messaggio $m$ (in chiaro) e una firma $H(s | | m)$ utilizzata per autenticare l'origine del messaggio (dove $s$ è un segreto)

> L'obiettivo dell'attaccante è estendere il messaggio originale, aggiungendo in coda un messaggio $m'$ e modificando l'autenticatore in modo che il destinatario non se ne accorga
> $$ m \to (m||m') $$ $$ H(s||m) \to H(s||m||m')$$

Funzionamento:
1. L'attaccante intercetta il messaggio $m$ e l'autenticatore $H(s||m)$
2. L'attaccante usa l'autenticatore come vettore di inizializzazione per la compressione iterata di $m'$
3. **Concatenando l'autenticatore di $m$ con il primo blocco dell'estensione del messaggio $m'$** si può proseguire (con compressione iterata) al calcolo di un attestato di autenticità corretto per $m||m'$ -> $H(s||m||m')$

![lengh-extension attack.png](/img/user/sicurezza-informazione-M/immagini/lengh-extension%20attack.png)

Questo attacco può essere risolto tramite [[sicurezza-informazione-M/2-hash-PRNG/Principio di compressione iterata#^7c923c\|padding]] (inefficace) oppure, in maniera più efficace, calcolando **l'attestato di autenticità concatenando s <u> dopo</u> il messaggio m**, calcolando quindi l'impronta di $H(m||s)$ -> in questo caso verrebbe sgamato dal destinatario, che troverebbe $m|| s ||m'$ 

Un'altra contromisura è applicare un'**ulteriore funzione di hash**: $H(H(m||s))$, perchè il destinatario riceverebbe un autenticatore $H(H(m||s))||m'$


