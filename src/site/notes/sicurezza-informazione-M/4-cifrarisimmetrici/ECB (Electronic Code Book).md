---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/ecb-electronic-code-book/"}
---

#modalitàcifratura #algoritmo 

La modalità di cifratura ECB prevede che **ogni blocco di testo in chiaro sia cifrato in maniera indipendente e totalmente scollegata dagli altri**.

-> blocchi di dimensione fissa
-> ogni blocco cifrato separatamente con la stessa chiave
-> padding

Essa prevede i seguenti step:
1. Si prende il messaggio e lo si divide in blocchi
2. All'ultimo blocco vengono aggiunti dei bit di padding per farlo diventare uguale alla *dimensione fissata*
3. Ad ogni blocco viene applicata la funzione $E$ (che avrà sempre la stessa chiave)

![ecb.png](/img/user/sicurezza-informazione-M/immagini/ecb.png)

| **PRO**                                                                             | **CONTRO**                                                                                   |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Alto parallelismo** -> ogni blocco cifrato in maniera indipendente                | ***DETERMINISTICO*** -> a blocchi in chiaro identici corrisponderanno blocchi cifrati uguali |
| **No propagazione degli errori** -> confinata al blocco in cui avviene la cifratura | [[sicurezza-informazione-M/4-cifrarisimmetrici/Attacco di malleabilità\|Malleabile]] poichè fortemente deterministico                     |
|                                                                                     | Viene aggiunto del **padding al messaggio** -> spreco di banda -> overhead                   |
ECB può essere usato con relativa sicurezza <u>solo per cifrare testo breve ed assolutamente aleatorio tipo una chiave</u> generata tramite un [[sicurezza-informazione-M/2-hash-PRNG/Random Number Generator (RNG)#Pseudo Random Number Generator Cryptographically Secure (PRNGCS)\|PRNG crittograficamente sicuro]].