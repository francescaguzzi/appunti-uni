---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/10-oauth-openid/identita-digitale/"}
---


#  Identità Digitale e Autenticazione Federata

##  Cos'è l'identità digitale?
L’identità digitale è l’insieme di informazioni, attributi e credenziali che rappresentano un individuo (o un’organizzazione) nel mondo online. Con la crescita esponenziale dei servizi digitali, ogni utente gestisce molteplici identità su piattaforme diverse.

---

#  Evoluzione dei modelli di identità

### 1. Identità centralizzata
- Ogni servizio gestisce in autonomia identità e credenziali.
- Problemi principali:
  - Punti singoli di fallimento (es. data breach).
  - Gestione separata di molteplici credenziali.
  - Bassa usabilità e scarsa sicurezza.

### 2. Identità federata
**Un gruppo di entità fidate condivide le responsabilità di autenticazione, permettendo l’uso di un’unica identità su più servizi**.

 **Vantaggi**:
- Login unico (es. "Accedi con Google").
- Minore numero di account da gestire.

 **Svantaggi**:
- Dipendenza da un provider (es. Google, Microsoft).
- Preoccupazioni sulla privacy: il provider sa dove e quando ti autentichi.

---

# Tecnologie principali per identità federata

Abbiamo [[sicurezza-informazione-M/10-oauth-openid/OAuth\|OAuth]] ed una sua estensione, [[sicurezza-informazione-M/10-oauth-openid/OpenID Connect\|OpenID Connect]]. 

### Differenza tra OAuth 2.0 e OIDC

| OAuth 2.0                  | OpenID Connect (OIDC)                  |
| -------------------------- | -------------------------------------- |
| Autorizzazione             | Autenticazione + Autorizzazione        |
| Accesso a risorse protette | Login e profilazione utente            |
| Access Token               | ID Token (JWT) + Access Token          |
| Uso generico per API       | Uso specifico per login federato e SSO |

### Esempio pratico
Un sito (es. “Terrible Pun of the Day”) chiede accesso ai contatti email per inviare SMS:
1. Reindirizza al provider per il login.
2. Ottiene autorizzazione dell’utente.
3. Riceve un authorization code → access token.
4. Usa il token per leggere i contatti ed eseguire azioni.
5. L’utente può revocare l’accesso in qualsiasi momento.

---

# Self-Sovereign Identity (SSI)

 Il prossimo passo dell’identità digitale: **controllo totale dell’identità in mano all’utente**.

 Principi:
- Nessun intermediario.
- Dati conservati sul dispositivo dell’utente.
- Ogni dato può essere selettivamente condiviso.

###  DID - Decentralized Identifier
- Identificatore univoco decentralizzato.
- Collegato a un documento (DID Document) con chiavi pubbliche e info.

##  Verifiable Credentials (VC)
Credenziali digitali firmate crittograficamente, controllate dall’utente.

## Selective Disclosure
Condivisione mirata solo dei dati necessari.


## Recap SSI

|Aspetto|Spiegazione breve|
|---|---|
|Cos'è|Identità digitale controllata direttamente dall'utente|
|Chiavi|L’utente ha chiavi crittografiche private/pubbliche|
|DID|Identificatori unici e decentralizzati|
|VC|Credenziali firmate, verificabili e portabili|
|Privacy|Rivelazione selettiva, unlinkability, ZKP|
|Vantaggi|Autonomia, sicurezza, privacy, portabilità|
|Sfide|Usabilità, revoca, interoperabilità, gestione chiavi|
|Normativa|eIDAS 2.0 dà una base legale e interoperabile|

---

##  Minacce e Sicurezza

1. Furto della chiave privata.
2. Uso improprio di credenziali rubate.
3. Contraffazione di credenziali.
4. Accesso eccessivo ai dati da parte dei servizi.
5. Replay attack.

---

##  EBSI & EUDIW
- Infrastruttura [[sicurezza-informazione-M/9-blockchain/Blockchain\|Blockchain]] europea.
- Supporta servizi pubblici e credenziali verificabili.


---
