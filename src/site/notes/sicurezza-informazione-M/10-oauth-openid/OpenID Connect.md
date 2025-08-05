---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/10-oauth-openid/open-id-connect/"}
---

#identificazione #argomentotutor 

OIDC è un’estensione di OAuth 2.0 che aggiunge funzionalità di autenticazione. Fornisce anche informazioni sull’utente (es. nome, email) oltre all’autorizzazione.

Permette ai client di verificare l’identità dell’utente e ottenere informazioni sul profilo dell’utente tramite un ID Token.

#### Caratteristiche principali
- Richiede lo scope `openid`.
- Fornisce sia access token che ID token.
- Il client riceve informazioni sull’identità dell’utente.
- Supporta il **Single Sign-On (SSO)** -> un solo login per più applicazioni

#### ID Token
- È un JSON Web Token (JWT).
- Include informazioni come: ID dell’utente, timestamp del login, durata, firma crittografica.
- Verificabile tramite chiavi pubbliche del provider.
- Maggiore interoperabilità tra servizi.
- Supporto completo per login federato e identità utente.