---
{"dg-publish":true,"permalink":"/sicurezza-informazione-m/10-oauth-openid/o-auth/"}
---

#identificazione #argomentotutor 

OAuth è un protocollo di autorizzazione che consente a un'applicazione di ottenere accesso limitato ai dati di un utente presenti su un altro servizio, senza bisogno di conoscere la password dell'utente.

#### Flusso base (Authorization Code Flow)
1. L’utente clicca su “Accedi con...” (resource owner).
2. Viene reindirizzato all’authorization server per il login.
3. L’utente concede l’accesso all’app.
4. Il client riceve un authorization code.
5. Il client scambia il code per un access token.
6. Il client usa l’access token per accedere ai dati dell’utente.

#### Concetti chiave
- **Resource Owner**: l’utente.
- **Client**: l’applicazione che chiede l’accesso.
- **Authorization Server**: il server che autentica l’utente e fornisce il token.
- **Resource Server**: il server che ospita i dati protetti.
- **Access Token**: token di accesso temporaneo.
- **Scope e Consent**: definiscono e limitano i permessi richiesti dal client.
- **Client ID/Secret**: credenziali dell’applicazione client.


 **Vantaggi di OAuth**:
- Maggiore sicurezza: non condivide la password.
- Accesso granulare: l'app vede solo ciò che è autorizzata a vedere.

OAuth 2.0 è un protocollo di autorizzazione delegata che consente a un’applicazione (client) di accedere a dati o funzionalità in un altro servizio (resource server) per conto dell’utente, senza condividere la password dell’utente.


