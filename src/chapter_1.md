# VADEMECUM SECONDA PROVA – SISTEMI E RETI
**Guida strategica per affrontare l'esame di Stato con commissario esterno**

---

## PREMESSA: COSA VALUTA IL COMMISSARIO ESTERNO

Il commissario esterno non conosce il vostro percorso, non sa come lavorate abitualmente, e valuterà principalmente:

- ✓ Correttezza tecnica e terminologia appropriata
- ✓ Completezza della risposta (avete capito TUTTA la richiesta?)
- ✓ Capacità di argomentare e motivare le scelte tecniche
- ✓ Ordine, chiarezza espositiva e presentazione formale

**NON può valutare** "l'impegno", "quanto avete studiato" o "le vostre intenzioni". Valuta solo ciò che scrivete sul foglio.

---

## 1. PRIMA DELLA PROVA: PREPARAZIONE STRATEGICA

### □ RIPASSARE I FONDAMENTALI, non i dettagli estremi
- Meglio padroneggiare bene i concetti base che sapere poco di tutto
- Focus su: definizioni precise, differenze tra tecnologie, quando/perché si usa una soluzione

### □ ALLENARSI CON IL TEMPO
- La seconda prova ha una durata limitata: abituatevi a scrivere risposte complete in tempi realistici
- Durante le simulazioni, cronometrate ogni fase

### □ PREPARARE UN "GLOSSARIO MENTALE"
- Ripassate la terminologia tecnica corretta in italiano (non solo acronimi!)
- Es: "Network Address Translation", "demilitarized zone", "lista di controllo degli accessi"

---

## 2. DURANTE LA PROVA: METODO DI LAVORO

### A) PRIMI 10-15 MINUTI: LETTURA E PIANIFICAZIONE

1. **Leggere TUTTA la traccia almeno 2 volte** (senza scrivere nulla)
   - Prima lettura: capire il contesto generale
   - Seconda lettura: sottolineare parole chiave e richieste specifiche

2. **Identificare TUTTE le domande/richieste** (anche quelle nascoste)
   - Spesso una frase contiene più richieste: "Spiega cos'è e quando si usa"
   - Numerare mentalmente i punti da affrontare

3. **Pianificare il tempo per ciascuna sezione**
   - Quale domanda vale più punti? Richiede più tempo?
   - Lasciare sempre 15-20 minuti finali per rilettura

### B) GESTIONE DEL TEMPO

⏱ **REGOLA D'ORO:** Non rimanere bloccati su una domanda
- Se non sapete rispondere completamente, scrivete almeno le definizioni base e passate oltre
- Meglio rispondere parzialmente a tutto che benissimo a metà traccia

⏱ **ALLOCAZIONE SUGGERITA** (es. prova da 6 ore):
- 15 min: lettura e pianificazione
- 4h 30min: sviluppo risposte (distribuito proporzionalmente ai punti)
- 45 min: revisione, controllo, integrazione
- 30 min: ricopiatura in bella (se necessario) e controllo formale

### C) COME STRUTTURARE LE RISPOSTE

📌 **SCHEMA VINCENTE:**

1. Definizione/Inquadramento teorico
2. Spiegazione tecnica (come funziona)
3. Applicazione pratica (quando/perché si usa)
4. Eventuale esempio o schema

**ESEMPIO PRATICO:**

*Domanda: "Descrivi cos'è una DMZ e quando viene utilizzata"*

❌ **RISPOSTA INSUFFICIENTE:**
> "La DMZ è una zona dove si mettono i server pubblici per proteggerli."

✅ **RISPOSTA COMPLETA:**
> "La DMZ (DeMilitarized Zone) è un segmento di rete isolato, posizionato tra la rete interna (LAN) e la rete esterna (Internet), protetto da due firewall. 
>
> Dal punto di vista architetturale, nella DMZ vengono collocati i server che devono essere accessibili dall'esterno (web server, mail server, FTP) mantenendo protetta la rete interna aziendale. Il primo firewall filtra il traffico proveniente da Internet verso la DMZ, mentre il secondo firewall protegge la LAN interna da eventuali compromissioni dei server in DMZ.
>
> Questa configurazione viene utilizzata quando un'organizzazione deve esporre servizi pubblici minimizzando i rischi: se un server in DMZ viene compromesso, l'attaccante non ha accesso diretto alla rete interna."

---

## 3. COSA VALORIZZARE (cosa fa la differenza)

### ✓ TERMINOLOGIA TECNICA CORRETTA
- Usare i termini precisi, non "all'incirca"
- Es: "subnet mask" non "maschera", "indirizzo MAC" non "codice della scheda"

### ✓ MOTIVARE LE SCELTE TECNICHE
- Non scrivere solo "si usa X", ma "si usa X perché..."
- Il commissario vuole capire se avete compreso il PERCHÉ, non solo il COSA

### ✓ CITARE NORME E STANDARD quando rilevanti
- Es: raccomandazioni X.800, modello ISO/OSI, RFC, protocolli standard
- Dimostra professionalità e visione sistemica

### ✓ DISEGNARE SCHEMI quando utile
- Un'architettura di rete, uno schema di crittografia asimmetrica
- Uno schema chiaro vale quanto 20 righe di testo confuso

---

## 4. ERRORI DA EVITARE ASSOLUTAMENTE

❌ **Rispondere "a sensazione" senza rileggere la domanda**
- Rileggete la domanda PRIMA di scrivere ogni risposta

❌ **Usare gergalismi o termini inventati**
- "La chiave pubblica cripta" → NO. "La chiave pubblica cifra" → SÌ
- Evitare: "hackare", "bucare", "proteggere forte"

❌ **Lasciare risposte vuote o scrivere "non lo so"**
- Scrivete SEMPRE qualcosa di sensato, anche definizioni base

❌ **Scrivere risposte generiche e vaghe**
- "Il firewall serve per la sicurezza" → troppo generico
- "Il firewall analizza il traffico di rete secondo regole (ACL) per bloccare/consentire pacchetti in base a IP, porte e protocolli" → specifico

❌ **Dimenticare unità di misura, formati, notazioni**
- Es: "255.255.255.0", "192.168.1.0/24", "AES-256", "RSA-2048"

---

## 5. ASPETTI FORMALI E PRESENTAZIONE

### 📝 SCRITTURA:
- Calligrafia leggibile (il commissario deve capire cosa scrivete!)
- Usare penna blu/nera, evitare cancellature eccessive
- Organizzare risposte con paragrafi, non blocchi unici

### 📝 STRUTTURA:
- Numerare chiaramente le risposte secondo la traccia
- Usare titoletti se la risposta è articolata
- Lasciare margini e spazi bianchi (migliora la leggibilità)

### 📝 LINGUAGGIO:
- Registro formale, ma non artificioso
- Frasi chiare e sintattiche corrette
- Evitare abbreviazioni non standard

---

## 6. GESTIONE DELLO STRESS

### 💪 PRIMA DELLA PROVA:
- Dormire bene la notte precedente (più importante del ripasso last-minute)
- Arrivare con 15 minuti di anticipo per ambientarsi

### 💪 DURANTE LA PROVA:
- Se vi bloccate: respirare, rileggere la domanda, scrivere almeno le definizioni
- Se il tempo stringe: sintetizzare le risposte rimanenti ma completarle tutte
- Ricordate: il commissario valuta ciò che c'è scritto, non le vostre intenzioni

### 💪 TRUCCHI ANTI-PANICO:
- "Non so questa risposta" → Scrivi definizione + esempio generico
- "Il tempo sta finendo" → Priorità alle domande che valgono più punti
- "Ho sbagliato qualcosa" → Se c'è tempo, correggete; altrimenti andate avanti

---

## CHECKLIST FINALE (ultimi 15 minuti prima di consegnare)

- □ Ho risposto a TUTTE le domande?
- □ Ho riletto ogni risposta verificando che sia completa?
- □ Ho controllato terminologia tecnica, acronimi, unità di misura?
- □ Gli schemi/disegni sono chiari ed etichettati?
- □ Nome, data e numerazione pagine sono presenti?
- □ La scrittura è leggibile?

---

## PROMEMORIA FINALE

Questo vademecum è uno strumento di **METODO**, non sostituisce lo studio dei contenuti.

La seconda prova valuta la vostra preparazione tecnica, ma anche la capacità di comunicare competenze in modo professionale.

Un commissario esterno deve poter leggere il vostro elaborato e pensare: *"Questo studente sa di cosa parla ed è pronto per il mondo del lavoro o l'università"*.

**Mostrate competenza, precisione e professionalità.**

**Buon lavoro! 💻🔒**

---

*Prof. [Il tuo nome] – Sistemi e Reti – A.S. 2024/2025*