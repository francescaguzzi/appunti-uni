---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/3-cifrariclassici/cifrario-di-vernam-mourborgne/"}
---

#definizione 
### One-time pad

Estensione del [[sicurezza-informazione-M/3-cifrariclassici/Cifrario di Vernam\|Cifrario di Vernam]] in cui **la chiave viene scelta casualmente**, viene **utilizzata una sola volta** e sarà **lunga quanto il testo** -> non potrà mai essere ripetuta nel testo cifrato. 

È l’unico esempio di cifrario **completamente sicuro da [[sicurezza-informazione-M/1-concettibase/Attacchi informatici#Attacchi passivi\|attacchi passivi]]** (ma non da attacchi attivi).

Questo cifrario è sicuro, ma non viene utilizzato salvo casi eccezionali, in quanto *la chiave deve essere lunga quanto l’intero testo*. Infatti, se dovessi mandare il testo in chiaro e la chiave in un canale non sicuro, **tanto vale mandare solamente il testo in un canale sicuro**.

