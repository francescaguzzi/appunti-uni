---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/2-hash-prng/paradosso-del-compleanno/"}
---

#concetto

> **Il paradosso del compleanno permette di trovare la probabilità di avere un duplicato in un insieme di k valori in cui ogni valore è equiprobabile**; segue quindi che, **aumentando la cardinalità di questo insieme (cioè usando impronte con più bit), la probabilità di trovare duplicati diminuisce**.

Assumendo la data di compleanno come equiprobabile: 
- Se prendo 253 persone, la probabilità che uno degli individui **compia gli anni in un giorno scelto** è maggiore del 50% (<u>resistenza debole</u>). 
- Se invece prendo 23 persone, la **probabilità che due persone siano nate lo stesso giorno** è maggiore del 50% (<u>resistenza forte</u>). 

Per quando riguarda la resistenza forte alle collisioni, per avere una probabilità maggiore del 50% di ottenere che due persone compiano gli anni lo stesso giorno si ha bisogno di un numero di prove pari a $2^{n/2}$ . Usando impronte di 160+ bit la resistenza alle collisioni forti è rispettata. 

Per quanto riguarda invece la resistenza debole, essa avrà bisogno di un numero di prove doppio, quindi $2^n$ per essere considerata sicura ovvero impronte di 80+ bit. Si ha quindi come conclusione che ***nelle funzioni di hash attaccare la resistenza forte è doppiamente più facile che attaccare quella debole***.

-> Per garantire sia resistenza forte che debole servono almeno 160+bit 
-> per sicurezza e completezza se ne utilizzano fino a 512 (SHA-256 ne utilizza 256)

**Il paradosso del compleanno è utile quando dobbiamo cercare due hash uguali in un insieme**. È utile per craccare la password in un database o per pre-generare due file diversi con lo stesso hash per poi sostituirne uno con l’altro -> quest’ultima cosa può essere utile per **far “firmare” un contratto a qualcuno mediante hash e sostituirlo in seguito con una versione diversa**.
-> tecniche note come *<u>birthday attack</u>