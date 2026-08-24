# Device Control USB — SentinelOne

Documentazione operativa per l'attivazione del blocco dei dispositivi USB tramite
SentinelOne Device Control su infrastruttura multisede.

## Architettura console di riferimento

```
Account (unico)
├── Site "<SEDE-1>"
│   ├── Group <SEDE-1>-Uffici
│   ├── Group <SEDE-1>-Produzione
│   ├── Group <SEDE-1>-IT
│   └── Group <SEDE-1>-Pilota
├── Site "<SEDE-2>"
│   └── ...
└── Site "<SEDE-N>"
```

**Principio di disegno:** il divieto vive a livello **Account**, l'eccezione vive
sul **Group** più stretto possibile. Nessuna eccezione va creata a livello Account
o Site salvo casi documentati.

## Indice dei documenti

| Documento | Contenuto | Destinatario |
|---|---|---|
| [`docs/01-runbook.md`](docs/01-runbook.md) | Runbook operativo fase per fase, passi console | IT / SecOps |
| [`docs/02-matrice-regole.md`](docs/02-matrice-regole.md) | Matrice regole e scope da trascrivere in console | IT / SecOps |
| [`docs/03-registro-eccezioni.csv`](docs/03-registro-eccezioni.csv) | Template registro eccezioni | IT / Audit |
| [`docs/04-checklist-test.md`](docs/04-checklist-test.md) | Checklist di test pre-enforcement | IT / Referenti di sede |
| [`docs/05-policy-supporti-rimovibili.md`](docs/05-policy-supporti-rimovibili.md) | Policy aziendale d'uso dei supporti rimovibili | Direzione / HR / tutti |
| [`docs/06-comunicazione-utenti.md`](docs/06-comunicazione-utenti.md) | Comunicazione agli utenti prima dell'attivazione | Tutti i dipendenti |
| [`docs/07-prerequisiti-e-adempimenti.md`](docs/07-prerequisiti-e-adempimenti.md) | Prerequisiti tecnici e adempimenti normativi | IT / Legale / HR |

## Postura adottata

Percorso a tre fasi:

1. **Fase 0 — Discovery** (2 settimane): inventario dei dispositivi realmente in uso.
2. **Fase 1 — Read-Only** su mass storage, tutte le sedi: chiude l'esfiltrazione con impatto utente minimo.
3. **Fase 2 — Block + allow-list** per Vendor+Product+Serial sui dispositivi aziendali censiti.

Se la direzione richiede il blocco immediato, la Fase 1 si può saltare: la Fase 0
resta obbligatoria, altrimenti l'allow-list nasce incompleta e il rollout genera
disservizi in produzione.

## Nota sulla nomenclatura console

Le voci di menu e i nomi delle categorie di dispositivo cambiano tra versioni di
console SentinelOne. Verificare la nomenclatura sull'istanza in uso prima di
seguire il runbook alla lettera.
