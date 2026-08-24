# Runbook operativo — Device Control USB

Architettura: **un Account → un Site per sede → Group dentro ogni Site**.

Prerequisiti da chiudere prima di iniziare: vedi [`07-prerequisiti-e-adempimenti.md`](07-prerequisiti-e-adempimenti.md).

---

## Regole di disegno (valgono per tutte le fasi)

1. **Il divieto sta sull'Account, l'eccezione sul Group.**
   La policy di default si imposta una sola volta a livello Account: così un Site
   creato in futuro per una nuova sede nasce già protetto invece di essere
   dimenticato. Le eccezioni si scopano sul Group più stretto possibile.

2. **Mai eccezioni a livello Account o Site** (salvo casi documentati e approvati).
   Un'eccezione creata a livello Account per un utente di una sede sblocca tutte le
   altre sedi, e nessuno se ne accorge.

3. **Mai eccezioni per solo Vendor ID.**
   `Vendor = SanDisk` autorizza qualunque chiavetta di quella marca comprata al
   supermercato. Le eccezioni su storage si fanno su **Vendor + Product + Serial**.
   Vendor+Product senza serial è ammesso solo per periferiche non-storage
   (es. un modello di lettore barcode) e va motivato nel registro.

4. **Ereditarietà:** ciò che imposti su un Site è ereditato dai Group sottostanti;
   una modifica su un Group non risale al Site. Verificare sempre lo scope
   selezionato nel pannello **Scopes** prima di salvare: selezionare lo scope
   sbagliato è l'errore più frequente.

---

## Struttura dei Group da predisporre in ogni Site

Group per **funzione**, non per persona: le eccezioni si agganciano al ruolo e
restano valide quando cambia il personale o apre una nuova sede.

| Group | Contenuto | Postura tipica |
|---|---|---|
| `<SEDE>-Pilota` | 10-20 macchine miste, popolato solo durante il rollout | Fase in test |
| `<SEDE>-Uffici` | Postazioni amministrative e commerciali | Postura standard, nessuna eccezione |
| `<SEDE>-Produzione` | Postazioni di reparto, HMI, terminali | Eccezioni tecniche (PLC, barcode, dongle) |
| `<SEDE>-IT` | Postazioni del personale IT | Eccezioni operative, a scadenza |
| `<SEDE>-Direzione` | Portatili direzione | Postura standard: nessuna deroga per ruolo |
| `<SEDE>-Kiosk` | Postazioni condivise / non presidiate | Postura più restrittiva della standard |

> Non creare un Group "Deroghe" o "Esenti". Diventa la discarica dove finisce
> chiunque apra un ticket, e in un anno svuota la policy.

---

## Fase 0 — Discovery (2 settimane)

**Obiettivo:** costruire l'inventario reale dei dispositivi in uso, per sede e per
funzione, prima di bloccare qualsiasi cosa.

### Passi

1. Predisporre la struttura dei Group in ogni Site (tabella sopra).
2. Abilitare Device Control lasciando i permessi larghi (nessun blocco).
3. Attendere almeno **10 giorni lavorativi**, includendo un ciclo di chiusura
   mensile se in azienda esiste (è quando emergono gli usi USB straordinari:
   backup, invii a commercialista, scarico dati da macchinari).
4. Console → **Activity / Device Control logs**: esportare gli eventi con
   Vendor ID, Product ID, Serial, macchina, utente, Site.
5. Classificare ogni dispositivo trovato in una di quattro categorie:
   - **Aziendale approvato** → andrà in allow-list (Fase 2)
   - **Personale** → sarà bloccato
   - **Tecnico non-storage** (token, dongle, barcode, PLC) → eccezione dedicata
   - **Da chiarire** → contattare il referente di sede

6. Compilare `03-registro-eccezioni.csv` con le categorie 1 e 3.

> Verificare se la console in uso offre una modalità monitor/audit esplicita per
> Device Control: se presente, usarla. Altrimenti la discovery si fa come sopra.

### Lista dei falsi positivi da censire attivamente

Non aspettare che emergano dal log — vai a cercarli, chiedendo ai referenti di sede:

- token di firma digitale e lettori smart card (CNS, Aruba, InfoCert) — classe smart card/CCID
- chiavi di sicurezza FIDO2 / YubiKey — si presentano come HID
- dongle di licenza hardware (HASP / Sentinel HL) su gestionali, CAD, CAM
- lettori barcode, bilance, stampanti etichette, terminali di magazzino
- programmatori PLC, cavi seriali-USB, chiavette di manutenzione macchinari
- docking station (espongono ethernet + hub: si presentano come più device)
- tastiere, mouse, webcam, cuffie, stampanti

### Criterio di uscita dalla Fase 0

- [ ] Log esportati da tutti i Site
- [ ] Ogni dispositivo classificato, zero voci "da chiarire"
- [ ] Registro eccezioni compilato e approvato dai referenti di sede

---

## Fase 1 — Read-Only su mass storage

**Obiettivo:** chiudere il canale di esfiltrazione con impatto utente minimo.
La lettura resta possibile, la scrittura no.

### Passi

1. Console → pannello **Scopes** → selezionare **Account**.
2. Scheda **Device Control**.
3. Interfaccia **USB**, categoria **Mass Storage** → default **`Read Only`**.
4. Creare le regole di eccezione tecniche (categoria 3 della Fase 0) sui Group
   competenti, secondo [`02-matrice-regole.md`](02-matrice-regole.md).
5. **Applicare prima al solo Group `<SEDE>-Pilota`** di una sede, non a tutte.
6. Eseguire la [checklist di test](04-checklist-test.md) sul pilota.
7. Dopo **3-5 giorni lavorativi senza ticket bloccanti**, estendere al Site completo.
8. Ripetere sede per sede, non tutte in parallelo (vedi piano d'onda sotto).

### Attenzione operativa

Un dispositivo già montato prima dell'applicazione della policy può restare
accessibile fino al riaggancio. **In fase di test far scollegare e ricollegare
fisicamente il dispositivo**, altrimenti il test dà un falso negativo.

### Criterio di uscita dalla Fase 1

- [ ] Tutti i Site in Read-Only su mass storage
- [ ] Nessun ticket bloccante aperto da più di 5 giorni
- [ ] Allow-list Fase 2 completata e validata

---

## Fase 2 — Block + allow-list

**Obiettivo:** deny di default, accesso completo solo ai dispositivi aziendali
censiti e identificati per seriale.

### Passi

1. Scope **Account** → Device Control → USB → Mass Storage → default **`Block`**.
2. Per ogni dispositivo aziendale approvato, creare una regola
   **`Full Access`** su criterio **Vendor + Product + Serial**, scopata sul Group
   competente.
3. Rollout identico alla Fase 1: pilota → Site → sede successiva.

### Prerequisito organizzativo

La Fase 2 non parte finché non è operativo il **processo di eccezioni**:

- chi approva (responsabile di sede + IT)
- SLA di risposta dichiarato agli utenti (es. 1 giorno lavorativo)
- **data di scadenza obbligatoria** sulle eccezioni temporanee
- revisione dell'allow-list ogni 6 mesi

Senza scadenze e revisione, in due anni l'allow-list diventa più permissiva della
policy che ha sostituito.

---

## Piano d'onda multisede

Non attivare tutte le sedi insieme: se emerge un falso positivo sistemico, lo
scopri su una sede invece che su tutta l'azienda.

| Onda | Scope | Durata minima | Gate di passaggio |
|---|---|---|---|
| 1 | `<SEDE-1>-Pilota` | 5 gg | Checklist test superata |
| 2 | Site `<SEDE-1>` completo | 5 gg | Nessun ticket bloccante aperto |
| 3 | `<SEDE-2>-Pilota` + `<SEDE-3>-Pilota` | 5 gg | Checklist test superata |
| 4 | Site `<SEDE-2>` e `<SEDE-3>` completi | 5 gg | Nessun ticket bloccante |
| 5 | Sedi rimanenti | — | — |

Scegliere come sede pilota quella con **la maggiore varietà di casi d'uso**
(tipicamente quella con produzione), non la più piccola: la sede piccola non fa
emergere i problemi, li rimanda.

---

## Rollback

Se emerge un blocco che ferma un processo aziendale:

1. Riportare il default della categoria interessata al valore precedente **sullo
   scope minimo che risolve** (Group, non Account).
2. Registrare l'evento e la causa nel registro eccezioni.
3. Non estendere l'onda successiva finché la causa non è chiarita.

Il rollback su Account va usato solo per incidenti che coinvolgono più sedi.

---

## Cosa questo controllo NON copre

Da comunicare alla direzione in fase di approvazione, non dopo il primo incidente:

- **Non è DLP.** Non tocca esfiltrazione via webmail, cloud personale, servizi di
  trasferimento file, stampa.
- **Non ferma BadUSB.** Un dispositivo di attacco si presenta come tastiera (HID),
  non come storage. Bloccare la classe HID lascia le macchine senza tastiera e
  mouse: è un intervento separato e delicato, non va fatto in questo progetto.
- **Smartphone via MTP/PTP**: canale di uscita completo, non sempre classificato
  come mass storage. Verificare esplicitamente questa categoria in console — è la
  falla più comune di questo tipo di configurazione.
- **Tethering e chiavette LTE/Wi-Fi**: bypassano la rete aziendale e i suoi
  controlli. Categoria adattatori di rete, da valutare a parte prestando
  attenzione alle docking station.
- **Bluetooth**: interfaccia separata con controlli propri, non coperta dalle
  regole USB.
