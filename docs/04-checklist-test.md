# Checklist di test pre-enforcement

Da eseguire sul Group `<SEDE>-Pilota` **prima** di estendere al Site completo, e da
ripetere a ogni onda del rollout.

**Regola d'oro:** ogni dispositivo va **scollegato e ricollegato fisicamente** prima
del test. Un dispositivo già montato quando la policy è stata applicata può restare
accessibile fino al riaggancio e dare un falso negativo.

Compilare una copia per Site.

---

## Composizione del pilota

Il pilota deve contenere almeno un esemplare di ciascuno, altrimenti non prova nulla:

- [ ] 1 postazione ufficio standard
- [ ] 1 postazione di produzione / reparto
- [ ] 1 portatile di direzione
- [ ] 1 macchina macOS (se presenti in azienda)
- [ ] 1 postazione con token di firma digitale
- [ ] 1 postazione con docking station
- [ ] 1 postazione con dongle di licenza hardware (se presenti)

Site: ______________  Fase: ______  Data: __________  Operatore: ______________

---

## A. Test di blocco (deve fallire l'accesso)

| # | Test | Atteso Fase 1 | Atteso Fase 2 | Esito | Note |
|---|---|---|---|---|---|
| A1 | Chiavetta personale non censita — lettura | Consentita | Bloccata | ☐ | |
| A2 | Chiavetta personale non censita — **scrittura** | **Bloccata** | Bloccata | ☐ | Test più importante della Fase 1 |
| A3 | Disco esterno non censito — scrittura | Bloccata | Bloccata | ☐ | |
| A4 | Smartphone Android via MTP — trasferimento file | Bloccato | Bloccato | ☐ | Falla più comune: verificare davvero |
| A5 | iPhone via USB — trasferimento foto | Bloccato | Bloccato | ☐ | |
| A6 | Chiavetta aziendale con **serial diverso** da quello in allow-list | Bloccata scrittura | Bloccata | ☐ | Verifica che il match sia sul serial e non sul modello |

## B. Test di continuità operativa (deve funzionare)

| # | Test | Atteso | Esito | Note |
|---|---|---|---|---|
| B1 | Tastiera e mouse USB | Funzionanti | ☐ | Se falliscono: rollback immediato |
| B2 | Token firma digitale / CNS — firma di un documento | Funzionante | ☐ | Blocco qui = fermo amministrativo |
| B3 | Lettore smart card | Funzionante | ☐ | |
| B4 | YubiKey / chiave FIDO2 — login | Funzionante | ☐ | Blocco qui = utenti fuori dai sistemi |
| B5 | Dongle licenza hardware — avvio gestionale/CAD | Funzionante | ☐ | Blocco qui = fermo produzione |
| B6 | Docking station — rete, monitor, periferiche | Funzionanti | ☐ | Espone più device: verificare tutti |
| B7 | Stampante USB — stampa di prova | Funzionante | ☐ | |
| B8 | Webcam e cuffie — videochiamata | Funzionanti | ☐ | |
| B9 | Lettore barcode / terminale di magazzino | Funzionante | ☐ | Solo su postazioni di reparto |
| B10 | Programmatore PLC / cavo seriale-USB | Funzionante | ☐ | Coinvolgere il responsabile di reparto |
| B11 | Chiavetta aziendale **in allow-list** — lettura e scrittura | Funzionanti | ☐ | Solo Fase 2 |

## C. Test di tenuta del controllo

| # | Test | Atteso | Esito | Note |
|---|---|---|---|---|
| C1 | Utente con admin locale prova a fermare il servizio agent | Fallisce (Anti-Tamper) | ☐ | Se riesce, il controllo non esiste |
| C2 | Utente prova a disinstallare l'agent | Fallisce | ☐ | |
| C3 | Disabilitazione Device Control da GUI locale | Non disponibile all'utente | ☐ | |
| C4 | Riavvio della macchina → policy ancora applicata | Sì | ☐ | |
| C5 | Macchina offline (senza rete) → policy ancora applicata | Sì | ☐ | Test critico: portatili in trasferta |

## D. Test di osservabilità

| # | Test | Atteso | Esito | Note |
|---|---|---|---|---|
| D1 | Un blocco genera un evento in Activity / Device Control logs | Sì | ☐ | |
| D2 | L'evento riporta Vendor ID, Product ID, Serial | Sì | ☐ | Serve per creare l'eccezione |
| D3 | L'evento è attribuito al Site e Group corretti | Sì | ☐ | Verifica che lo scoping funzioni |
| D4 | L'utente riceve un messaggio comprensibile del blocco | Sì | ☐ | Se no: rischio ticket "il PC non funziona" |

---

## Criterio di passaggio all'onda successiva

Tutti e tre devono essere veri:

- [ ] **Zero fallimenti in sezione B** — un solo fallimento in B blocca il rollout
- [ ] **Zero fallimenti in sezione C** — un fallimento qui significa che il controllo è aggirabile
- [ ] **3-5 giorni lavorativi** sul pilota senza ticket bloccanti

Fallimenti in sezione A significano che la policy non sta bloccando: verificare
versione agent e scope selezionato prima di procedere.

Esito complessivo: ☐ PASS  ☐ FAIL

Firma operatore: ______________  Referente di sede: ______________
