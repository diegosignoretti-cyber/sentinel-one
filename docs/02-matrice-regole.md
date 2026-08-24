# Matrice regole Device Control

Da trascrivere in console. Sostituire `<SEDE-n>` con i nomi reali dei Site.

## Convenzione di naming delle regole

```
<AZIONE>-<SITE>-<GROUP>-<DEVICE>-<TICKET>
```

Esempi:

- `ALW-MILANO-Produzione-BarcodeZebra-INC12345`
- `ALW-ROMA-IT-KingstonIKVP-CHG00987`
- `RO-BARI-Kiosk-MassStorage-STD`

Prefissi azione: `ALW` = Full Access, `RO` = Read Only, `BLK` = Block.

Il ticket nel nome non è burocrazia: è l'unico modo per sapere, tra sei mesi,
perché una regola esiste e se è ancora necessaria.

---

## Livello Account — policy di default

Impostata **una sola volta**, ereditata da tutti i Site presenti e futuri.

| Interfaccia | Categoria | Fase 1 | Fase 2 | Note |
|---|---|---|---|---|
| USB | Mass Storage | `Read Only` | `Block` | Il cuore del controllo |
| USB | Smartphone / MTP / PTP | `Block` | `Block` | Verificare come è classificata nella console in uso |
| USB | Adattatori di rete | da valutare | da valutare | Attenzione alle docking station: testare in pilota prima |
| USB | HID (tastiere/mouse) | **non toccare** | **non toccare** | Bloccare = macchine inutilizzabili |
| USB | Smart card / CCID | `Full Access` | `Full Access` | Token firma digitale, CNS |
| USB | Stampanti | `Full Access` | `Full Access` | |
| USB | Audio / Video | `Full Access` | `Full Access` | Webcam, cuffie |
| Bluetooth | — | da valutare | da valutare | Interfaccia separata, fuori dallo scope di questo progetto |

> Le categorie disponibili e i loro nomi variano tra versioni di console.
> Allineare questa tabella alla nomenclatura effettiva prima di procedere.

---

## Livello Site — nessuna regola

Per disegno, **nessuna eccezione va creata a livello Site**. Un'eccezione Site
vale per tutte le funzioni di quella sede, comprese quelle che non ne hanno
bisogno.

Unica deroga ammessa: un dispositivo effettivamente presente su tutti i Group di
una sede (es. un unico modello di lettore badge in tutta la sede). Va motivato nel
registro eccezioni con approvazione IT.

---

## Livello Group — eccezioni

Una riga per regola. Compilare in Fase 0, applicare in Fase 1/2.

### Template

| Nome regola | Site | Group | Interfaccia | Criterio | Vendor ID | Product ID | Serial | Azione | Scadenza | Ticket |
|---|---|---|---|---|---|---|---|---|---|---|
| `ALW-<SEDE>-<GRUPPO>-<DEVICE>-<TKT>` | | | USB | Vendor+Product+Serial | | | | Full Access | | |

### Eccezioni tecniche ricorrenti (da verificare in Fase 0)

Righe tipiche in un'azienda con produzione. **Non copiarle alla cieca**: i VID/PID
vanno letti dai log reali della propria Fase 0.

| Dispositivo | Group tipico | Criterio consigliato | Azione | Note |
|---|---|---|---|---|
| Token firma digitale / CNS | tutti | Class (smart card/CCID) | Full Access | Regola di categoria a livello Account, non eccezione |
| YubiKey / FIDO2 | tutti | Class (HID) | Full Access | Coperta dal non bloccare HID |
| Dongle licenza HASP / Sentinel HL | `<SEDE>-Produzione`, `<SEDE>-Uffici` | Vendor+Product | Full Access | Non-storage: serial non necessario |
| Lettore barcode | `<SEDE>-Produzione` | Vendor+Product | Full Access | Spesso si presenta come HID |
| Programmatore PLC / cavo seriale-USB | `<SEDE>-Produzione` | Vendor+Product | Full Access | Verificare col responsabile di reparto |
| Chiavetta aziendale cifrata | `<SEDE>-<funzione>` | Vendor+Product+**Serial** | Full Access | **Serial obbligatorio** |
| Disco esterno backup | `<SEDE>-IT` | Vendor+Product+**Serial** | Full Access | Con scadenza se temporaneo |
| Chiavetta manutentore esterno | Group dedicato o temporaneo | Vendor+Product+**Serial** | Read Only | **Sempre con scadenza** |

---

## Anti-pattern da rifiutare in fase di approvazione

| Richiesta | Perché va rifiutata | Alternativa |
|---|---|---|
| "Sblocca il vendor SanDisk" | Autorizza qualunque chiavetta di quella marca al mondo | Vendor+Product+Serial del dispositivo specifico |
| "Sblocca tutto per la Direzione" | Deroga per ruolo, non per esigenza tecnica. I portatili di direzione sono il bersaglio a più alto valore | Nessuna deroga; se serve trasferire file, canale approvato |
| "Metti l'eccezione su Account così vale ovunque" | Sblocca tutte le sedi | Regola replicata sui Group che ne hanno bisogno |
| "Eccezione permanente per il fornitore X" | Nessun controllo sul dispositivo del fornitore | Read Only + scadenza + Group dedicato |
| "Creiamo un gruppo Esenti" | Diventa la discarica dei ticket e svuota la policy | Eccezioni puntuali, tracciate, a scadenza |
| "Blocchiamo anche gli HID per fermare i BadUSB" | Macchine senza tastiera e mouse | Intervento separato, valutato a parte |
