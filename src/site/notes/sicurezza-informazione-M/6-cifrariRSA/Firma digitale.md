---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/6-cifrari-rsa/firma-digitale/"}
---

#highpriority #modalitàcifratura 

**L’impiego più naturale di un cifrario asimmetrico come l’RSA è per il servizio di firma digitale**, ma prima di tutto ricordiamo (dalla firma digitale nei cifrari simmetrici) quali sono i requisiti che uno schema di firma digitale deve possedere:

1. **Deve consentire a chiunque di identificare univocamente il firmatario** -> o <u>crittografia asimmetrica</u>, o <u>terza entità</u> nella crittografia simmetrica
2. La firma **non deve poter essere imitata da un impostore**
3. La firma **non deve poter essere trasportata da un documento all'altro**
4. La firma **non deve poter essere ripudiata dall'autore**
5. La firma **deve rendere inalterabile il documento su cui viene applicata**

In uno schema di firma digitale con *chiavi simmetriche*:
- Firma -> chiave privata
- Verifica -> chiave pubblica

---

Esistono due possibili schemi di firma digitale con ***meccanismi asimmetrici***:

- ***==Modalità con recupero==*** -> [[sicurezza-informazione-M/6-cifrariRSA/Firma digitale con RSA\|Firma digitale con RSA]] -> il messaggio <u>diviso in blocchi</u> ed ogni blocco viene <u>firmato separatamente con chiave privata</u>
{ #dac876}

	- Non rispetta punti 3 e 4 sopra -> un **attaccante potrebbe scambiare i blocchi del messaggio e ottenere un messaggio correttamente firmato**
	- Va **aggiunta ridondanza al messaggio tramite una funzione $R$ per creare un collegamento sotteso tra i blocchi**
	
- ***==Modalità con appendice==*** -> es. El Gamal, DSA -> **non viene firmato l'intero messaggio, ma un suo hash** ->dato che la firma viene allegata ed è separata, rende **immediatamente disponibili i dati** e la firma si controlla solo su necessità. 

Tipicamente **si preferisce la modalità appendice a quella con recupero** perchè rispettà tutte le proprietà in maniera efficiente -> inoltre <u>qualsiasi algoritmo con recupero è anche utilizzabile in modalità con appendice</u> -> basta cifrare con chiave privata l'hash


> **Si può utilizzare un algoritmo di firma (con recupero o appendice) per l'[[sicurezza-informazione-M/6-cifrariRSA/Identificazione attiva con firma\|Identificazione attiva con firma]]**

---

Nel caso di un ***workflow con firma digitale*** di documenti si possono adottare due modalità:

- ***==Firme concatenate==*** 
	**L’applicazione di una firma approva solo il contenuto del messaggio, a prescindere dalle firme applicate in precedenza** $$m' = m \ || \ S_{S^A}(H(m)) \ || \ S_{S^B}(H(M))\ || \ ...$$ In questo caso nessun utente si prende alcuna responsabilità nei confronti di firme di altri utenti.
	
- ***==Firme a cipolla==*** 
	**L’applicazione di una firma approva il contenuto del messaggio e anche tutte le firme applicate in precedenza**
	In questo caso A firma $m$ con appendice: $$ m_1=m \ || \ S_{S^A}(H(m))$$ e B firma il messaggio $m_1$ ottenendo $$m_2 = m_1 \ || \ S_{S^B}(H(m))$$ Quindi <u>B firma anche la firma di A</u>, assumendosi la responsabilità.

---
