# Piano di rimedio e hardening — handout per il board

Il documento che si lascia al board **dopo** l'apertura dei dossier: il board deve
uscire dalla stanza rassicurato e con un piano di controllo in mano (regola 40/60).

> Riferimento: Parte V del manuale integrato.

---

## A. Azioni immediate a costo zero (entro 7 giorni)

### 1. Procedura di verifica fuori banda (out-of-band)

**Regola vincolante:** nessuna variazione di coordinate bancarie (IBAN) né
richiesta di bonifico urgente può essere autorizzata senza una **chiamata di
conferma** al numero storico del fornitore/dirigente già memorizzato
nell'anagrafica — mai al numero indicato nella mail o nella fattura stessa.

→ È la singola contromisura che spezza lo scenario "Venerdì alle 18:30".

### 2. Sanitizzazione dei metadati

Policy interna per la rimozione dei metadati (autore, percorsi di rete, software)
prima della pubblicazione di qualsiasi documento o PDF sul sito aziendale o sui
portali fornitori.

### 3. Security briefing personalizzato (30 minuti per dirigente)

Revisione guidata delle impostazioni di privacy sui profili social delle quattro
figure: disattivazione della geolocalizzazione automatica dei post e limitazione
della visibilità dei contatti.

---

## B. Interventi strutturali a medio termine (entro 30–60 giorni)

### 1. Autenticazione forte resistente al phishing (FIDO2 / passkey)

Chiavi di sicurezza fisiche (es. security key) per l'accesso alle caselle email di
CEO, CFO, HR e Ufficio Acquisti: neutralizza il furto di sessione e il phishing
tradizionale.

### 2. Segmentazione e sandbox per la ricezione CV (Ufficio HR)

Isolare la casella di reclutamento in un ambiente sicuro, o adottare una
piattaforma che converta automaticamente in PDF sanitizzato i file inviati dai
candidati prima che raggiungano le postazioni.

### 3. Monitoraggio continuo dei domini civetta (typosquatting)

Monitoraggio proattivo che segnali la registrazione da parte di terzi di domini
simili a quello aziendale o a quelli dei partner strategici.

---

## C. Delibera richiesta al board

Al minuto 40–45 della riunione, richiesta di delibera formale:

> Adozione immediata e vincolante della **procedura di verifica out-of-band** per
> ogni variazione di coordinate bancarie e ogni richiesta di pagamento urgente,
> con firma della direzione.

| Azione | Responsabile | Scadenza | Costo |
|---|---|---|---|
| Procedura verifica out-of-band | {{CFO / Amministrazione}} | 7 giorni | € 0 |
| Policy sanitizzazione metadati | {{IT / Marketing}} | 7 giorni | € 0 |
| Briefing privacy 4 dirigenti | {{IT / SecOps}} | 7 giorni | € 0 |
| Rollout FIDO2 / passkey | {{IT}} | 30–60 giorni | {{stima}} |
| Sandbox ricezione CV | {{IT / HR}} | 30–60 giorni | {{stima}} |
| Monitoraggio domini civetta | {{IT / SecOps}} | 30–60 giorni | {{stima}} |
