# Schede contenuto per ruolo — struttura dei 4 dossier

Guida di compilazione del one-pager a 4 quadranti, una scheda per figura apicale.
I campi tra `{{ }}` vanno popolati con le evidenze raccolte dall'auditor interno
(solo fonti pubbliche e passive). Il livello di esposizione è una valutazione
dell'auditor, non un dato pubblico.

> Vincoli trasversali (§4.6): nessun dato intimo/familiare/sanitario; password
> sempre mascherate; identità verificata al 100%.

---

## SCHEDA 1 — Amministratore Delegato (CEO)

- **Intestazione:** `TARGET: AMMINISTRATORE DELEGATO — LIVELLO ESPOSIZIONE: {{CRITICO}}`
- **Q1 — Identità & breach:** foto ufficiale (fonte); email personale in breach
  storici {{quali}} con password mascherata `{{A***201*!}}`; cariche societarie da
  visura pubblica.
- **Q2 — Movimenti & assenze:** date e sedi degli ultimi viaggi comunicati sui
  social {{es. "presenza a fiera dal 14 al 17"}}; evidenza: la finestra di assenza
  e la reperibilità ridotta risultano pubbliche.
- **Q3 — Relazioni & deleghe:** nome dell'assistente esecutivo (da ringraziamenti
  pubblici); eventuale firma autografa scansionata presente in documenti pubblici.
- **Q4 — Vettore d'attacco:** *CEO Fraud su bonifico d'urgenza.* Scenario sintetico
  (difensivo) che collega assenza + potere di firma a una richiesta di pagamento
  spoofata verso il CFO. Perdita potenziale stimata: {{€}}.

---

## SCHEDA 2 — Responsabile Finanziario (CFO)

- **Intestazione:** `TARGET: RESPONSABILE FINANZIARIO — LIVELLO ESPOSIZIONE: {{ALTO}}`
- **Q1 — Identità & breach:** email aziendale istituzionale; account terzi
  registrati con la mail aziendale (portali fiscali, newsletter finanziarie).
- **Q2 — Stack applicativo esposto:** software ERP/gestionale di contabilità in uso
  (desunto da profilo o annunci di lavoro passati); istituti bancari storici citati
  in note integrative o contratti pubblici.
- **Q3 — Organigramma amministrativo:** nomi e ruoli dei collaboratori che
  rispondono al CFO; flusso standard di approvazione dei mandati di pagamento.
- **Q4 — Vettore d'attacco:** *Invoice redirection / urgenza con deepfake.* Scenario
  sintetico che collega lo stack noto e il flusso di approvazione a una variazione
  IBAN fraudolenta. Perdita potenziale stimata: {{€}}.

---

## SCHEDA 3 — Responsabile Ufficio Acquisti (Head of Procurement)

- **Intestazione:** `TARGET: RESPONSABILE ACQUISTI — LIVELLO ESPOSIZIONE: {{CRITICO}}`
- **Q1 — Identità & contatti esterni:** email diretta e recapiti su elenchi
  fornitori o portali di gara; presenza a convegni di supply chain.
- **Q2 — Mappatura fornitori strategici:** elenco di {{n}} fornitori reali
  identificati via case study pubblicati o post di ringraziamento/consegna.
- **Q3 — Flusso documentale in ingresso:** volume stimato di file ricevuti
  dall'esterno (preventivi, listini); percorso di rete trapelato dai metadati di un
  capitolato pubblico {{es. \\SRV-FILE\Acquisti\...}}.
- **Q4 — Vettore d'attacco:** *Vendor Email Compromise via dominio typosquattato.*
  Scenario sintetico che collega un fornitore noto a una fattura inoltrata con
  coordinate alterate. Perdita potenziale stimata: {{€}}.

---

## SCHEDA 4 — Responsabile Risorse Umane (HR)

- **Intestazione:** `TARGET: RESPONSABILE RISORSE UMANE — LIVELLO ESPOSIZIONE: {{ELEVATO}}`
- **Q1 — Identità & presenza reclutamento:** email diretta nelle sezioni "Lavora
  con noi" o negli annunci; rete di collegamenti con agenzie per il lavoro,
  università, consulenti.
- **Q2 — Canale allegati non filtrato:** casella di ricezione CV ordinaria senza
  ambiente di isolamento; formati comunemente aperti sui PC dell'ufficio.
- **Q3 — Dati di organizzazione interna:** struttura gerarchica e ruoli vacanti
  esposti negli annunci (indizi su reparti sottodimensionati).
- **Q4 — Vettore d'attacco:** *Accesso iniziale via CV infetto.* Scenario sintetico
  che collega il canale allegati non filtrato all'ingresso nella rete. Perdita
  potenziale stimata: {{€}}.
