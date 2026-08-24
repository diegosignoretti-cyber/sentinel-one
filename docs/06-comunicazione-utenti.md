# Comunicazione agli utenti

> **BOZZA.** Da inviare **almeno 10 giorni prima** dell'attivazione della Fase 1 e
> di nuovo 3 giorni prima di ogni onda del rollout. Compilare i campi tra
> parentesi angolari.

Il blocco tecnico senza comunicazione preventiva produce ticket "il PC non
funziona", aggiramenti e resistenza. La comunicazione costa mezz'ora e dimezza i
ticket.

---

## Email 1 — Annuncio (10 giorni prima)

**Oggetto:** Nuove regole sull'uso delle chiavette USB — attivazione dal \<data\>

Ciao a tutti,

dal **\<data\>** introduciamo una nuova misura di sicurezza sui PC aziendali che
riguarda l'uso delle chiavette USB e dei dischi esterni.

**Cosa cambia**

Dal \<data\> non sarà più possibile **copiare file su chiavette USB e dischi
esterni personali** dai PC aziendali. La lettura dei file presenti su una chiavetta
resterà possibile.

\<In Fase 2 sostituire con: Dal \<data\> le chiavette USB e i dischi esterni non
approvati non saranno più utilizzabili sui PC aziendali, né in lettura né in
scrittura.\>

**Perché**

Le chiavette sono oggi la causa più frequente di perdita di dati aziendali —
si smarriscono, si prestano, finiscono su PC di casa — e uno dei canali con cui i
virus entrano in azienda. La misura protegge i dati dell'azienda e il lavoro di
tutti.

**Cosa NON cambia**

Continueranno a funzionare normalmente:

- tastiere, mouse, monitor, docking station
- stampanti, webcam, cuffie
- token di firma digitale, lettori smart card, chiavi di sicurezza
- lettori barcode e strumentazione di reparto
- \<altro specifico dell'azienda\>

**Come trasferire i file da qui in avanti**

Usa i canali aziendali: \<file server / OneDrive / SharePoint / posta aziendale /
piattaforma approvata\>. Sono più veloci di una chiavetta e i file restano
recuperabili se sbagli qualcosa.

**Se ti serve davvero una chiavetta per lavorare**

Alcune attività richiedono un supporto fisico. Se è il tuo caso, scrivici a
\<contatto\> entro il \<data\> spiegando cosa devi fare: valutiamo insieme la
soluzione, che può essere una chiavetta aziendale assegnata a te. **Non aspettare
il giorno del blocco:** segnalacelo prima e non ti fermi.

Per domande: \<contatto\>.

\<Firma\>

---

## Email 2 — Promemoria (3 giorni prima)

**Oggetto:** Promemoria — dal \<data\> nuove regole sulle chiavette USB

Ciao a tutti,

un promemoria breve: **dal \<data\>** entra in vigore la misura annunciata il
\<data email 1\> sull'uso delle chiavette USB e dei dischi esterni sui PC
aziendali.

Se hai un'attività che richiede l'uso di una chiavetta e non ce l'hai ancora
segnalata, scrivici **oggi** a \<contatto\>: facciamo in tempo a sistemarla prima
dell'attivazione.

Se colleghi una chiavetta e non riesci a usarla, non è un guasto: apri un ticket a
\<contatto\> indicando cosa stavi facendo e ti rispondiamo entro \<SLA\>.

\<Firma\>

---

## Nota per l'helpdesk (interna, non inviare agli utenti)

Risposta standard al ticket "non riesco a usare la chiavetta":

> È una misura di sicurezza attiva dal \<data\>, non un guasto. Per capire come
> aiutarti mi serve sapere: quale file devi trasferire, da dove a dove, e con che
> frequenza. Nella maggior parte dei casi si risolve con \<canale aziendale\>;
> se l'attività richiede davvero un supporto fisico, ti assegniamo una chiavetta
> aziendale previa approvazione del tuo responsabile.

**Non** risolvere il ticket creando un'eccezione al volo. Ogni eccezione passa dal
processo di approvazione e va registrata in `03-registro-eccezioni.csv` con
approvatore e scadenza.

Da tracciare durante il rollout, per sede: numero di ticket, quanti risolti con
canale alternativo, quanti hanno richiesto un'eccezione reale. Se le eccezioni
reali superano il \<10%\> delle postazioni di una sede, la Fase 0 su quella sede è
stata incompleta: fermare l'onda e rifare l'inventario.
