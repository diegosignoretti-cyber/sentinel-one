# Prerequisiti tecnici e adempimenti normativi

Da chiudere **prima** di toccare qualsiasi policy. I punti 1-4 possono invalidare
l'intero piano; i punti 5-6 possono rendere inutilizzabili i log raccolti.

## 1. Licenza

Device Control è incluso a partire da **Singularity Control**. Su Singularity Core
la funzionalità non è disponibile e serve un upgrade commerciale.

- [ ] Verificato tier di licenza dell'Account
- [ ] Verificato che la scheda **Device Control** sia visibile nella toolbar

## 2. Versione agent

Il supporto Device Control richiede agent recenti (indicativamente 21.6+; verificare
il requisito minimo per la versione di console in uso). Agent più vecchi accettano
la policy senza applicarla: è la causa numero uno di "policy attiva ma non blocca".

- [ ] Estratto elenco agent per Site (Sentinels → colonna Agent Version)
- [ ] Identificati agent sotto la versione minima
- [ ] Pianificato aggiornamento **prima** dell'enforcement, non dopo

## 3. Sistemi operativi

| OS | Device Control USB | Azione |
|---|---|---|
| Windows | Supportato | Copertura piena |
| macOS | Supportato | Copertura piena, verificare differenze di comportamento in fase pilota |
| Linux | **Non supportato** | Serve controllo compensativo |

Controllo compensativo per i Linux (da valutare con chi gestisce quelle macchine):
blacklist del modulo `usb-storage`, regole `udev` di deny, disabilitazione porte USB
da BIOS/UEFI con password, o esclusione fisica dal perimetro.

- [ ] Censiti gli endpoint Linux per Site
- [ ] Definito e approvato il controllo compensativo

## 4. Anti-Tamper

Senza Anti-Tamper attivo, un utente con privilegi di amministratore locale può
fermare o disinstallare l'agent e aggirare il blocco. **Il blocco USB senza
Anti-Tamper non è un controllo di sicurezza, è un suggerimento.**

- [ ] Anti-Tamper verificato attivo su tutti i Site
- [ ] Censiti gli utenti con admin locale (idealmente da ridurre in parallelo)

## 5. Art. 4 Statuto dei Lavoratori (L. 300/1970)

I log di Device Control associano dispositivo, macchina, utente e orario: sono
potenzialmente strumenti dai quali deriva un controllo a distanza dell'attività
lavorativa. Prima dell'attivazione serve, secondo l'inquadramento del caso concreto:

- informativa adeguata ai lavoratori sulle modalità d'uso degli strumenti e di
  effettuazione dei controlli;
- valutazione se ricorra la necessità di accordo sindacale o di autorizzazione
  dell'Ispettorato del Lavoro.

**Da chiarire con il consulente del lavoro prima dell'attivazione.** Log raccolti
senza i presupposti non sono utilizzabili a fini disciplinari.

- [ ] Parere del consulente del lavoro acquisito
- [ ] Informativa ex art. 4 c.3 consegnata ai lavoratori
- [ ] Se necessario: accordo sindacale / autorizzazione ITL

## 6. GDPR

I log di Device Control contengono dati personali (identificativo utente, macchina,
seriale del dispositivo, timestamp).

- [ ] Trattamento inserito nel registro dei trattamenti
- [ ] Informativa dipendenti aggiornata
- [ ] Periodo di conservazione dei log definito e documentato
- [ ] Definito chi accede ai log e con quale ruolo console

## 7. Riferimento ISO 27001 (se applicabile)

Questa configurazione copre il controllo **A.7.10 Supporti di memorizzazione** e
concorre ad **A.8.7**. Runbook, matrice regole e registro eccezioni costituiscono
l'evidenza documentale per l'audit.

- [ ] Statement of Applicability aggiornato
- [ ] Documentazione collegata al controllo in SoA

## 8. Ruoli console

Serve un ruolo con permessi di **Policy Management** sullo scope di intervento.

- [ ] Identificati gli operatori abilitati per Account e per Site
- [ ] Definito chi può creare eccezioni (vedi `03-registro-eccezioni.csv`)
