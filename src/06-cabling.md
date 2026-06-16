# 5. Cablaggio strutturato

## 1. Cos'è il cablaggio strutturato

Il **cablaggio strutturato** è l'insieme di cavi, connettori, pannelli e apparati passivi che
costituisce l'infrastruttura fisica di una rete LAN. È progettato in modo **indipendente dalle
applicazioni**: la stessa infrastruttura supporta dati, voce e video.

Gli standard di riferimento internazionali sono:
- **TIA-568** (americano, ANSI/TIA)
- **ISO/IEC 11801** (internazionale)

Entrambi definiscono i sottosistemi, le categorie dei cavi e le distanze massime ammissibili.

🎓 **All'esame:** se la traccia chiede di "progettare il cablaggio" è implicito che si seguano
questi standard. Non è necessario citarli esplicitamente, ma le scelte devono essere coerenti
con essi.

---

## 2. I sottosistemi del cablaggio

Il cablaggio strutturato è suddiviso in **sottosistemi gerarchici**:

```
Postazione di lavoro
       │
  [Cablaggio orizzontale]   ← da postazione a TO (Telecommunications Outlet)
       │
  Presa a muro (TO)
       │
  [Cablaggio orizzontale]   ← da TO al pannello patch nel rack
       │
  Pannello patch (patch panel)
       │
  Switch di piano / reparto (access layer)
       │
  [Cablaggio verticale / backbone]
       │
  Switch core (distribution/core layer) — nel CED
       │
  Firewall → Router → Internet
```

| Sottosistema | Descrizione | Limite di distanza |
|---|---|---|
| **Cablaggio orizzontale** | Dalla postazione al pannello patch nel rack | 90 m (link permanente) |
| **Patch cord** (lato postazione) | Dal PC alla presa a muro | ≤ 5 m |
| **Patch cord** (lato rack) | Dal pannello patch allo switch | ≤ 5 m |
| **Canale completo** | Tutto il percorso postazione→switch | **100 m** totali |
| **Cablaggio verticale (backbone)** | Tra rack di piano e CED | variabile (vedi fibra) |

🎓 **Regola dei 90+10:** il cavo fisso nel controsoffitto/canalina non può superare 90 m;
i 10 m rimanenti sono divisi tra le patch cord alle due estremità.

---

## 3. Topologia: stella a due livelli

La topologia standard per una LAN d'ufficio è la **stella gerarchica** (o stella a due livelli):

```
         [CED]
        SW-CORE  ←── firewall, server, router
       /   |   \
    SW-A  SW-B  SW-C      ← switch di reparto (access layer)
    /|\   /|\   /|\
  PC PC  PC PC  PC PC    ← postazioni di lavoro
```

- Ogni postazione è collegata **solo** al proprio switch di reparto (non ci sono cavi diretti
  tra postazioni o tra switch di reparto).
- Lo switch core si trova nel **CED (Centro Elaborazione Dati)** o in un armadio rack centrale.
- La topologia garantisce **fault isolation**: un guasto in un reparto non abbatte gli altri.

---

## 4. Tipi di cavo e categorie

### Cavo in rame — UTP/FTP/STP

| Categoria | Banda | Velocità supportata | Uso tipico |
|---|---|---|---|
| **Cat5e** | 100 MHz | 1 Gbps (Gigabit Ethernet) | reti esistenti, retrofit |
| **Cat6** | 250 MHz | 1 Gbps (fino a 55 m: 10 Gbps) | **standard attuale per nuove installazioni** |
| **Cat6A** | 500 MHz | 10 Gbps su 100 m | uplink ad alte prestazioni |
| Cat7 / Cat8 | > 600 MHz | 10/25/40 Gbps | data center, backbone |

**Schermatura:**
- **UTP** (Unshielded Twisted Pair): nessuna schermatura, uso in ambienti senza disturbi EM
- **FTP** (Foil Twisted Pair): schermo globale in alluminio, ambienti con moderati disturbi
- **STP** (Shielded Twisted Pair): schermo globale + schermo per ogni coppia, ambienti industriali

🎓 **Scelta tipica all'esame:** Cat6 UTP per il cablaggio orizzontale di un ufficio standard.
Se la traccia menziona ambienti industriali o disturbi elettromagnetici → Cat6 FTP/STP.

### Fibra ottica

Usata per il **backbone** (tra rack, tra piani, tra edifici) quando le distanze superano i 100 m
o si richiedono velocità molto elevate.

| Tipo | Sigla | Distanza tipica | Uso |
|---|---|---|---|
| **Multimodale** | OM3 / OM4 | fino a 300–550 m (a 10 Gbps) | backbone intra-edificio |
| **Monomodale** | OS2 | fino a decine di km | backbone inter-edificio, WAN |

- La fibra è **immune ai disturbi elettromagnetici** e garantisce **isolamento elettrico**
  tra edifici (importante per la sicurezza).
- Non trasmette tensione → non c'è rischio di ground loop tra edifici separati.

🎓 **Regola pratica:** se nel testo la distanza tra due rack è > 90 m, o i rack sono in
edifici diversi → **fibra ottica**, specificando OM3/OM4 o OS2 a seconda del caso.

---

## 5. Connettori e apparati passivi

| Componente | Descrizione |
|---|---|
| **RJ-45** | Connettore standard per cavi in rame Cat5e/6/6A |
| **Presa a muro (TO)** | Terminazione del cavo orizzontale lato postazione; alloggia 1 o 2 porte RJ-45 |
| **Pannello patch (patch panel)** | Terminazione del cavo orizzontale lato rack; permette di fare il patching verso lo switch |
| **Armadio rack (19")** | Contenitore standard per apparati attivi (switch, router) e passivi (patch panel) |
| **Connettori fibra** | LC (più comuni), SC, ST — dipende dagli apparati |

**Il pannello patch è fondamentale:** evita di collegare direttamente i cavi fissi agli switch
(che si usurano), e rende semplice riconfigurare le connessioni.

---

## 6. Il CED (Centro Elaborazione Dati)

Il CED ospita:
- Lo **switch core** (o distribution switch), che interconnette tutti gli switch di reparto
- Il **firewall**
- Il **router** verso Internet/WAN
- I **server** aziendali (file server, DNS, DHCP…)
- I **gruppi di continuità (UPS)**
- I pannelli patch del backbone

**Posizione ideale:** al centro dell'edificio, per minimizzare le lunghezze dei cavi e
rispettare il limite dei 90 m di cablaggio orizzontale.

---

## 7. Dimensionamento: numero di porte e riserva

Per dimensionare correttamente il cablaggio:

1. **Contare le postazioni** per reparto (PC, stampanti, telefoni IP, access point…)
2. **Aggiungere una riserva del 20–25%** per espansioni future e guasti
3. **Scegliere gli switch** in base al numero di porte necessarie per reparto
4. **Verificare le porte dello switch core** (una porta trunk verso ogni switch di reparto)

**Esempio:**

| Reparto | Postazioni | Riserva 20% | Porte switch |
|---|---|---|---|
| Amministrazione | 20 | 4 | **24** (switch 24p) |
| Produzione | 40 | 8 | **48** (switch 48p) |
| Direzione | 8 | 2 | **12** → **24** (switch 24p) |

🎓 **All'esame:** giustifica sempre la riserva ("Si prevede una riserva del 20% per future
espansioni"). Arrotonda sempre verso l'alto alla taglia di switch disponibile (24 o 48 porte).

---

## 8. Schema riassuntivo per un ufficio tipo

Scenario: azienda con 3 reparti in un edificio a piano singolo, CED centrale.

```
           ┌──────────────────────────────────────────┐
           │                EDIFICIO                  │
           │                                          │
           │  [Reparto A]        [Reparto B]          │
           │  SW-A (24p)         SW-B (48p)           │
           │   │  UTP Cat6        │  UTP Cat6         │
           │   └────────┐ ┌──────┘                   │
           │            ▼ ▼                           │
           │         ┌───────┐                        │
           │         │  CED  │                        │
           │         │SW-CORE│──── Firewall ── Router │
           │         │       │──── File Server        │
           │         └───────┘                        │
           │            │ │                           │
           │   ┌────────┘  └──────────┐              │
           │   ▼                      ▼               │
           │  [Reparto C]       [Reparto D]           │
           │  SW-C (24p)        SW-D (24p)            │
           └──────────────────────────────────────────┘

Cablaggio orizzontale:  UTP Cat6  (≤ 90 m link permanente)
Backbone CED→switch:    UTP Cat6 se ≤ 90 m, altrimenti fibra OM3/OM4
```

---

## 9. Checklist per la seconda prova

Quando la traccia richiede di progettare il cablaggio, verifica di aver risposto a:

- [ ] **Topologia:** stella gerarchica con switch di reparto e switch core nel CED
- [ ] **Tipo di cavo:** UTP Cat6 per il cablaggio orizzontale; fibra se > 90 m o inter-edificio
- [ ] **Distanze:** cablaggio orizzontale ≤ 90 m (link permanente), canale totale ≤ 100 m
- [ ] **Apparati passivi:** prese a muro (TO), pannelli patch, armadi rack
- [ ] **Dimensionamento switch:** numero di porte ≥ postazioni + riserva 20–25%
- [ ] **CED:** posizione centrale, ospita switch core, firewall, router, server
- [ ] **Ipotesi dichiarate:** se la traccia non specifica le distanze, dichiara le tue ipotesi
      (es. "Si ipotizza che ogni reparto si trovi entro 80 m dal CED")
- [ ] **Coerenza:** le scelte tecniche devono essere giustificate e coerenti tra loro

🎓 **Ricorda:** la commissione premia la coerenza del ragionamento e la capacità di
giustificare le scelte, non la perfezione assoluta. Se fai un'ipotesi, dichiarala sempre.