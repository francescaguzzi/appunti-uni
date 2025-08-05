---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/5-certificati/crl-certificate-revocation-list/"}
---

#certificati #highpriority 

**Questo modello prevede che venga pubblicata periodicamente, da parte della CA su una directory (LDAP), una lista autenticata dei certificati revocati.**

Essendo un **modello pull** che permette una verifica offline della validità del certificato, ogni utente scarica periodicamente dalla directory la Certificate Revocation List (CRL) e controlla localmente lo stato del certificato per sapere se è ancora valido o meno.

La struttura dati contenente la CRL presenta vari campi, di cui i più significativi sono:
- **Signature Algorithm Identifier**
- **Issuer name**
- **This Update Date** e **Next Update Date**
- **Revoked Certificate** -> elenco dei certificati revocati con rispettivi numeri di serie, data di revoca ed estensioni (motivi revoca)
- **Firma della CRL da parte di CA**

# Problemi

1. **LISTE NON AGGIORNATE** -> siccome la CRL viene rilasciata periodicamente, non è garantita la freschezza delle informazioni

2. **CRESCITA CONTINUA DELLA STRUTTURA DATI CONTENENTE LA CRL** -> overhead per banda e problemi di memorizzazione -> ricerca di un certificato più lenta
# Ottimizzazioni

Per **ottimizzare il problema della crescita continua della struttura dati** (punto 2 sopra), si ricorre ad alcuni metodi di ottimizzazione:

1. **Eliminare la revoca nella prima CRL emessa dopo la data di scadenza del certificato** -> tanto il client controlla prima data di scadenza e poi se è stato revocato

2. **Pubblicare CRL complete (*Base CRL*) e poi le differenze (*Delta CRL*)** 
	L’utente finale, nel momento in cui andrà a cercare un certificato nelle liste di revoca, dovrà scaricare e/o verificare prima la Base CRL e, nel caso in cui non fosse lì presente, le successive Delta CRL seguendo l’ordine in cui sono state emesse
	- *caso fortunato* -> la trova scaricando poca roba
	- *caso sfortunato* -> deve scaricare fino all'ultima Delta CRL -> comunque uguale a scaricare tutta la storia delle liste di revoca
		
3. **Suddividere la CRL in partizioni** -> soluzione più utilizzata -> si suddivide la CRL in sottogruppi, in base a criteri scelti dalla CA:
	- *numero seriale del certificato*
	- *durata temporale della validità*
	Il client saprà dove andare a cercare perchè nell'estensione del certificato la CA ha la possibilità di inserire il "*Distribution Point*" per specificare in quale partizione della directory andare a controllare
