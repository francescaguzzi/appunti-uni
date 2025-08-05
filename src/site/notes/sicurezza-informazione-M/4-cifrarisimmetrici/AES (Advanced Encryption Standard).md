---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/4-cifrarisimmetrici/aes-advanced-encryption-standard/"}
---

#algoritmo

AES è un algoritmo di **crittografia simmetrica** (a chiave condivisa) usato per proteggere dati sensibili. È veloce, sicuro e ampiamente utilizzato (es. HTTPS, VPN, file encryption). 

Comunemente conosciuto anche come **algoritmo di Rijandael**, a differenza del DES, è una [rete a sostituzione e permutazione](https://it.wikipedia.org/wiki/Rete_a_sostituzione_e_permutazione "Rete a sostituzione e permutazione"), non una [[sicurezza-informazione-M/4-cifrarisimmetrici/Rete di Feistel\|Rete di Feistel]], che implementa comunque il [[sicurezza-informazione-M/3-cifrariclassici/Robustezza dei cifrari#Principio di Shannon\|principio crittografico di Shannon]] di "confusione e diffusione". 

AES è veloce sia se sviluppato in **software** sia se sviluppato in **hardware** è relativamente semplice da implementare, richiede **poca memoria** e offre un buon livello di protezione, motivi che complessivamente l'hanno reso il preferito rispetto agli altri algoritmi proposti.

Presenta alte prestazioni su tutte le piattaforme, un key setup veloce e presenta **3 lunghezze di chiavi** nel suo standard:
- **AES-128** (chiave a 128 bit)
- **AES-192** (chiave a 192 bit)    
- **AES-256** (chiave a 256 bit) → Più sicuro, ma leggermente più lento.

Dopodichè esegue **più round** di trasformazioni (10 round per 128 bit, poi 12 e 14). 