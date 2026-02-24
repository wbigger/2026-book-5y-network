## 2. Come leggere il testo

La seconda prova presenta sempre uno scenario realistico (azienda, scuola, ente pubblico, ecc.) con una serie di richieste. Prima di iniziare a scrivere, è fondamentale leggere il testo almeno due volte e analizzarlo in modo sistematico.

### 2.1 Individuare i requisiti espliciti

I requisiti espliciti sono quelli scritti chiaramente nel testo. Durante la prima lettura, sottolinea o evidenzia:

**Dati numerici:**
- Numero di piani, sale, uffici
- Numero di postazioni, dispositivi, utenti
- Eventuali indicazioni su distanze o metrature

**Componenti già presenti:**
- Rete esistente (switch, router, server)
- Connessione Internet già attiva
- Sistemi già in uso

**Richieste specifiche:**
- Cosa deve essere installato o configurato
- Vincoli tecnici ("deve usare la rete esistente", "deve essere separato")
- Requisiti di sicurezza o accesso remoto

**Esempio dalla prova 2024 (biblioteca con totem):**
> "...fornitura e installazione di un totem informativo per ogni sala e per gli spazi comuni..."

Qui il requisito esplicito è: un totem per sala + uno per ogni spazio comune. Devo contarli.

---

### 2.2 Dedurre i requisiti impliciti

I requisiti impliciti non sono scritti, ma si ricavano dal contesto o dal buon senso tecnico.

**Domande da porsi:**
- Se c'è un server, avrà bisogno di un gruppo di continuità?
- Se ci sono utenti che accedono via web, servirà HTTPS?
- Se la rete deve essere "indipendente", significa VLAN separate o fisicamente separate?
- Se c'è accesso da remoto, servirà una VPN?

**Esempio:**
> "I servizi accessibili dai totem sono basati su Web Application con possibilità di accesso degli utenti tramite nome utente e password"

Requisiti impliciti:
- Serve un database per le credenziali
- La connessione dovrebbe essere cifrata (HTTPS)
- Potrebbe servire un sistema di autenticazione centralizzato

---

### 2.3 Formulare ipotesi aggiuntive

Quando il testo non fornisce informazioni sufficienti, è necessario formulare ipotesi. Questo è esplicitamente previsto: *"fatte le eventuali ipotesi aggiuntive ritenute necessarie"*.

**Quando servono le ipotesi:**
- Mancano dati numerici (es. numero di utenti previsti)
- Non è specificata la tecnologia (es. tipo di connessione Internet)
- Non sono indicati requisiti di prestazioni o disponibilità

**Come formularle:**
- Essere ragionevoli e realistici
- Dichiarare sempre l'ipotesi esplicitamente
- Motivare brevemente la scelta

**Esempio:**
> "Si ipotizza che la biblioteca abbia una connessione Internet in fibra ottica da 100 Mbps, sufficiente per il traffico previsto dei totem e della rete esistente."

> "Si ipotizza un'affluenza media di 500 utenti al giorno, con un picco di 100 utenti concorrenti."

**Ipotesi comuni da considerare:**
- Banda della connessione Internet
- Numero di utenti concorrenti
- Requisiti di disponibilità (es. 99,9%)
- Budget (se si chiede una stima costi)

---

### 2.4 Sottolineare e schematizzare prima di rispondere

Prima di iniziare a scrivere la soluzione, dedica 15-20 minuti a:

**1. Evidenziare il testo**
- Colore 1: dati numerici e vincoli
- Colore 2: componenti esistenti
- Colore 3: richieste specifiche (punti A, B, C, D)

**2. Fare una lista dei componenti**

| Elemento | Quantità | Note |
|----------|----------|------|
| Totem | 19 | Uno per sala + spazi comuni |
| Switch esistenti | 4 | Uno per piano + sala computer |
| Server nuovo | 1 | Per le web application dei totem |

**3. Abbozzare uno schema di rete**

Anche solo a matita, disegna la struttura generale prima di dettagliarla. Ti aiuta a non dimenticare componenti e a visualizzare i flussi di comunicazione.

**4. Verificare di aver coperto tutti i punti**

La prima parte chiede sempre più cose (A, B, C, D...). Prima di scrivere, verifica di avere un'idea per ciascun punto. Se un punto non ti è chiaro, rileggilo.

---

### Checklist di lettura

Prima di iniziare a rispondere, verifica di saper rispondere a queste domande:

- [ ] Quanti dispositivi/utenti devo gestire?
- [ ] Cosa c'è già e cosa devo aggiungere?
- [ ] Le reti devono essere separate o integrate?
- [ ] Ci sono requisiti di sicurezza o accesso remoto?
- [ ] Quali ipotesi devo dichiarare?
- [ ] Ho capito cosa chiede ciascun punto (A, B, C, D)?