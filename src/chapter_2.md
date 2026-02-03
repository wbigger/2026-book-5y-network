# Linee guida

Quando dobbiamo definire l'architettura di rete di un servizio, dobbiamo prima di tutto avere ben chiari in mente una serie di elementi che ci aiuteranno nella progettazione. In pratica dobbiamo _visualizzare_ chiaramente come il nostro servizio verrà usato, immaginando il come, perché, dove, etc. di ogni azione che gli utenti compiono.

> Dobbiamo sempre ricordarci di porre l'*utente* che dovrà fruire del nostro servizio al centro delle nostre riflessioni, ed a questo fine possiamo usare diverse strategie. Questo tipo di progettazione si chiama "User Centered Design" (UCD).

I passi che dovremo svolgere sono i seguenti:

1. utenti: quali utenti (_ruoli_), quanti utenti
1. dispositivi end-user: quali dispositivi, quanti dispositivi
1. collegamenti degli end-device: bluetooth, WiFi, rete dati, RFID, NFC, etc.
1. dislocazione dei server: on-premises, cloud
1. dislocazione dei database: on-premises, cloud

In ognuno di questi passaggi potete aiutarvi con dei diagrammi o disegni per chiarire meglio cosa intendete. Non abbiate timore di scrivere o disegnare: la cosa più importante in questa fase è essere chiari.

Nei passaggi in cui operate delle scelte, è fondamentale che specifichiate il perché avete optato per una determinata tecnologia piuttosto che per un'altra. Ad esempio:

- <span class="ok">OK</span><br>
Scelgo una connessione WiFi per il tablet del turista perché ha una maggiore banda che mi permette di servire adeguatamente lo streaming video
- <span class="no">NO</span><br> Scelgo la connessione WiFi
- <span class="ok">OK</span><br>Scelgo un server in cloud perché ha minori costi iniziali e mi permette di pagare solo quello che effettivamente uso
- <span class="no">NO</span><br> Scelgo un server in cloud

I fattori da tenere in considerazione nella discussione di vantaggi e svantaggi:

- costi (sia iniziali che di esercizio)
- requisiti non funzionali (prestazioni, affidabilità)
- sicurezza dei dati, vulnerabilità ad eventuali attacchi
- normativa vigente (es. GDPR)

Quando possibile è utile aggiungere anche un'analisi quantitativa, oltre che semplicemente qualitativa. Ad esempio possiamo migliorare gli esempi precedenti come segue:

- Considerando 100 utenti che guardano in contemporanea un flusso video di 4kbps, ho bisogno di 800 kbps che può essere adeguatamente sostenuto da una connessione WiFi
- Si può stimare il costo iniziale del mio servizio in una soluzione on-premises sia pari a circa €10k (server+rack) e circa €500 mensile per la gestione, mentre in cloud non ho costi iniziali ed ho un costo mensile stimabili a circa €400 euro (istanza macchina virtuale+database MySQL); scelgo quindi il server in cloud perché ha sia minori costi iniziali che di esercizio e mi permette di pagare solo quello che effettivamente uso

Nel caso di servizi in cloud, in base alle vostre conoscenze potete specificare se intendente usare servizi:

- IaaS, cioè solo infrastruttura come macchine virtuali, firewall e switch virtuali, etc. che dovranno essere configurati da noi direttamente (es. AWS EC2)
- PaaS, cioè uso una piattaforma già parzialmente pronta (es. Wordpress)
- SaaS (sconsigliato per l'esame), cioè uso dei servizi già pronti (es Wix).

Considerando che spesso l'Esame di Stato chiede di progettare anche i database e scrivere il codice di alcune pagina, in generale lo sconsiglio per l'esame (ma può essere utile per un progetto reale futuro). 


Infine, nella costruzione delle frasi, consiglio di seguire alcuni _pattern_ che aiutano a creare un discorso che sia chiaro e continuo:

- mettere l'utente come soggetto e specificare il fine dell'azione:
  - <span class="ok">OK</span><br>Il fattorino scannerizza il codice a barre del pacco per prenderlo in carico
  - <span class="no">NO</span><br>Il codice a barre è scannerizzato dal fattorino

- scrivere possibilmente un caso d'uso completo del servizio, dal momento in cui l'utente inizia ad usarlo fino alla fine
  - <span class="ok">OK</span><br>Il fattorino prende in carico il pacco scannerizzando il codice a barre, quando lo consegna al destinatario lo scannerizza di nuovo per confermare l'avvenuta consegna
  - <span class="no">NO</span><br>Il codice a barre serve per la presa in carico e la consegna

Come ultimo suggerimento, può essere utile considerare nel nostro discorso anche alcuni casi in cui avviene *qualcosa di imprevisto*. Esempi:
- cosa succede se il destinatario non è in casa? ha un impatto significativo sul mio progetto? 
- quali procedure posso prevedere  se il pacco si perde o danneggia durante il trasporto?
- se il codice a barre diventa illeggibile durante il trasporto per qualche motivo, cosa succede?
- etc.






