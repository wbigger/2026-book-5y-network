# Dimensionamento di un Progetto Informatico

*Guida alla stima di risorse per l'Esame di Stato*

[Formulario dimensionamento](./Formulario_Dimensionamento.pdf)

# Indice

1. Introduzione al dimensionamento  
2. Stima degli utenti  
3. Stima dello storage  
4. Stima della banda  
5. Dimensionamento dei server  
6. Dimensionamento del database  
7. Infrastruttura on-premise  
8. Alta disponibilità e ridondanza  
9. Esempi svolti completi

# 1\. Introduzione al dimensionamento

Il dimensionamento di un progetto informatico consiste nel determinare le risorse hardware, software e di rete necessarie per soddisfare i requisiti funzionali e non funzionali di un sistema.

Un dimensionamento corretto deve:

* Garantire prestazioni adeguate nelle condizioni normali  
* Gestire i picchi di carico senza degrado significativo  
* Prevedere margini di crescita futura  
* Ottimizzare i costi evitando sovradimensionamenti

## Grandezze fondamentali

| Grandezza | Simbolo | Unità di misura |
| ----- | :---: | ----- |
| Utenti totali | U | numero |
| Utenti concorrenti | Uc | numero |
| Richieste al secondo | RPS | req/s |
| Throughput | T | MB/s, Gbps |
| Latenza | L | ms |
| Capacità storage | S | GB, TB |

## Fattori di conversione utili

| Da | A | Fattore |
| ----- | ----- | :---: |
| 1 Byte | 8 bit | × 8 |
| 1 KB | 1.000 Byte | × 10³ |
| 1 MB | 1.000 KB | × 10⁶ |
| 1 GB | 1.000 MB | × 10⁹ |
| 1 TB | 1.000 GB | × 10¹² |
| 1 Mbps | 0,125 MB/s | ÷ 8 |
| 1 Gbps | 125 MB/s | ÷ 8 |

**Nota per l'esame:** nei calcoli rapidi si usano i prefissi decimali (1 KB \= 1000 Byte). Nei sistemi reali si usano spesso i prefissi binari (1 KiB \= 1024 Byte), ma la differenza è trascurabile per le stime.

# 2\. Stima degli utenti

## Dalla base utenti agli utenti concorrenti

Non tutti gli utenti registrati usano il sistema contemporaneamente. La stima degli utenti concorrenti è fondamentale per dimensionare correttamente.

**Formula base:**   Utenti concorrenti (Uc) \= Utenti totali (U) × Fattore di concorrenza (Fc)

### Fattori di concorrenza tipici

| Tipo di sistema | Fc | Note |
| ----- | :---: | ----- |
| E-commerce generico | 5-10% | Picchi durante promozioni |
| Social network | 10-15% | Dipende dall'ora |
| Servizio aziendale interno | 20-30% | Orario lavorativo |
| Streaming video | 15-25% | Picchi serali |
| Gaming online | 20-40% | Picchi serali e weekend |

## Calcolo del picco

Il sistema deve reggere non solo il carico medio, ma anche i picchi. Si introduce un **fattore di picco (Fp)**.

**Formula:**   Utenti di picco (Up) \= Uc × Fp

| Tipo di sistema | Fp | Situazione di picco |
| ----- | :---: | ----- |
| E-commerce | 3-5× | Black Friday, saldi |
| News/Media | 5-10× | Breaking news |
| Aziendale | 1,5-2× | Inizio giornata, scadenze |
| Biglietteria | 10-20× | Apertura vendite eventi |

## Dalle utenti alle richieste

**Formula:**   RPS \= Up × Richieste per utente al minuto / 60

| Tipo di applicazione | Richieste/utente/minuto |
| ----- | :---: |
| Sito statico/blog | 2-5 |
| E-commerce (browsing) | 10-20 |
| E-commerce (checkout) | 30-50 |
| Social network | 20-40 |
| Dashboard real-time | 30-60 |

### Esempio di calcolo

**Scenario:** pizzeria online con 5.000 clienti registrati

10. Utenti concorrenti: 5.000 × 10% \= **500 utenti**  
11. Picco (venerdì sera): 500 × 3 \= **1.500 utenti**  
12. Richieste al minuto: 1.500 × 15 \= 22.500  
13. Richieste al secondo: 22.500 / 60 \= **375 RPS**

# 3\. Stima dello storage

## Tipologie di dati e dimensioni tipiche

### Dati testuali

| Tipo | Dimensione tipica |
| ----- | :---: |
| Record database semplice | 0,5 \- 2 KB |
| Documento JSON medio | 2 \- 10 KB |
| Email senza allegati | 5 \- 50 KB |
| Pagina HTML | 50 \- 200 KB |
| Documento Word/PDF semplice | 100 KB \- 2 MB |

### Immagini

| Tipo | Risoluzione | Dimensione |
| ----- | :---: | :---: |
| Thumbnail | 150×150 px | 5-15 KB |
| Immagine web bassa qualità | 800×600 px | 50-100 KB |
| Immagine web alta qualità | 1920×1080 px | 300-800 KB |
| Foto alta risoluzione | 4000×3000 px | 2-5 MB |

### Audio

| Formato | Bitrate | Dim./minuto |
| ----- | :---: | :---: |
| Audio chiamata VoIP | 32 kbps | 0,24 MB |
| Podcast / Audio medio | 128 kbps | 0,96 MB |
| Musica streaming | 256 kbps | 1,92 MB |
| Audio alta qualità | 320 kbps | 2,4 MB |

### Video

| Qualità | Risoluzione | Bitrate | Dim./minuto |
| ----- | :---: | :---: | :---: |
| SD | 480p | 2,5 Mbps | 18,75 MB |
| HD | 720p | 5 Mbps | 37,5 MB |
| Full HD | 1080p | 8 Mbps | 60 MB |
| 4K | 2160p | 25 Mbps | 187,5 MB |

## Formula per lo storage totale

Storage \= (Dati iniziali) \+ (Crescita giornaliera × Giorni retention) \+ Margine 20-30%

### Esempio calcolo storage e-commerce

| Tipo dato | Per ordine | Ordini/giorno | Totale/giorno |
| ----- | :---: | :---: | ----- |
| Record ordine | 2 KB | 200 | 400 KB |
| Immagini prodotti | 300 KB × 3 | 200 | 180 MB |
| Log transazioni | 5 KB | 200 | 1 MB |
| **Totale** |  |  | **\~180 MB/giorno** |

Retention 1 anno: 180 MB × 365 \= **\~65 GB/anno**

# 4. Stima della banda

## Formula fondamentale

Banda richiesta (bps) \= Utenti concorrenti × Banda per utente

Per convertire in Mbps dividere per 1.000.000.

## Banda per tipologia di contenuto

### Contenuti statici (download)

| Tipo contenuto | Banda per utente |
| ----- | :---: |
| Testo/HTML | 50-100 Kbps |
| Immagini bassa risoluzione | 200-500 Kbps |
| Immagini alta risoluzione | 1-2 Mbps |
| Download file | 2-10 Mbps |

### Contenuti streaming (continui)

| Tipo contenuto | Banda per utente |
| ----- | :---: |
| Audio VoIP | 32-64 Kbps |
| Audio streaming musica | 128-320 Kbps |
| Video SD (480p) | 1-2,5 Mbps |
| Video HD (720p) | 3-5 Mbps |
| Video Full HD (1080p) | 5-8 Mbps |
| Video 4K | 15-25 Mbps |
| Videoconferenza HD | 2-4 Mbps |

### Applicazioni interattive

| Tipo applicazione | Banda per utente |
| ----- | :---: |
| Chat testuale | 10-50 Kbps |
| Web browsing medio | 500 Kbps \- 2 Mbps |
| Gaming online | 1-3 Mbps |
| Desktop remoto | 2-10 Mbps |

## Calcolo con fattore di contemporaneità

Non tutti gli utenti scaricano alla massima velocità simultaneamente.

| Tipo traffico | Fattore contemporaneità |
| ----- | :---: |
| Streaming continuo | 0,9 \- 1,0 |
| Download grandi file | 0,3 \- 0,5 |
| Navigazione web | 0,1 \- 0,2 |
| Traffico background | 0,05 \- 0,1 |

### Esempio calcolo banda

**Scenario:** piattaforma e-learning con 1.000 studenti concorrenti

| Attività | Utenti | Banda/ut. | Fattore | Banda tot. |
| ----- | :---: | :---: | :---: | ----- |
| Video lezione HD | 300 | 5 Mbps | 0,95 | 1.425 Mbps |
| Slide/documenti | 400 | 1 Mbps | 0,15 | 60 Mbps |
| Chat/forum | 200 | 100 Kbps | 0,20 | 4 Mbps |
| Download materiali | 100 | 10 Mbps | 0,30 | 300 Mbps |
| **Totale** |  |  |  | **\~1.800 Mbps** |

Banda necessaria con margine: **\~2 Gbps**

# 5\. Dimensionamento dei server

## Risorse principali

| Risorsa | Cosa influenza |
| ----- | ----- |
| CPU (core/vCPU) | Numero di richieste gestibili |
| RAM | Utenti contemporanei, cache |
| Storage | Dati persistenti |
| Rete | Traffico in/out |

## Taglie server tipiche

| Taglia | vCPU | RAM | Uso tipico |
| ----- | :---: | :---: | ----- |
| Micro | 1 | 1 GB | Test, microservizi |
| Small | 2 | 4 GB | Siti piccoli, API |
| Medium | 4 | 8-16 GB | Applicazioni medie |
| Large | 8 | 32 GB | E-commerce, DB medi |
| XLarge | 16+ | 64+ GB | Enterprise |

## Scaling orizzontale vs verticale

| Tipo | Descrizione | Pro | Contro |
| ----- | ----- | ----- | ----- |
| **Verticale** | Server più potente | Semplice | Limite fisico |
| **Orizzontale** | Più server in parallelo | Scalabile | Più complesso |

**Regola pratica:** progettare per scaling orizzontale quando possibile.

# 6\. Dimensionamento del database

## Stima rapida dimensione

Dimensione DB ≈ Numero record × Dimensione media record × 1,5

Il fattore 1,5 include indici e overhead.

## Dimensioni tipiche record

| Tipo applicazione | Dimensione record |
| ----- | :---: |
| Anagrafica semplice | 200-500 byte |
| Ordine e-commerce | 1-2 KB |
| Documento con metadati | 2-5 KB |
| Record con BLOB/immagini | 100 KB \- 1 MB |

### Esempio rapido

E-commerce con 50.000 ordini/anno, record da 1,5 KB:

* Anno 1: 50.000 × 1,5 KB × 1,5 \= **\~110 MB**  
* 5 anni con margine: **\~1 GB**

# 7\. Infrastruttura on-premise

## Componenti di un data center

| Componente | Funzione |
| ----- | ----- |
| Server | Elaborazione |
| Storage (SAN/NAS) | Dati condivisi |
| Switch | Connettività LAN |
| Router | Connettività WAN |
| Firewall | Sicurezza perimetrale |
| UPS | Continuità elettrica |
| Gruppo elettrogeno | Backup alimentazione |
| Condizionamento | Raffreddamento |

## Dimensionamento rack

Un rack standard è 42U (unità rack), dove 1U \= 44,45 mm di altezza.

| Dispositivo | Altezza tipica |
| ----- | :---: |
| Server standard | 1U \- 2U |
| Server blade (chassis) | 6-10U |
| Switch 24-48 porte | 1U \- 2U |
| UPS piccolo | 2-3U |
| UPS medio | 6-12U |

**Regola pratica:** lasciare il 20-30% di spazio libero per aerazione e crescita.

## Dimensionamento alimentazione

Potenza totale (W) \= Σ Potenza dispositivi × Fattore utilizzo (0,6-0,8)

| Dispositivo | Consumo |
| ----- | :---: |
| Server entry-level | 200-400 W |
| Server mid-range | 400-700 W |
| Server high-end | 700-1500 W |
| Switch 24-48 porte | 30-100 W |
| Firewall | 50-200 W |

## Dimensionamento UPS

Capacità UPS (VA) \= Potenza totale (W) / Fattore di potenza (0,8-0,9)

**Autonomia tipica:** 10-30 minuti (sufficiente per shutdown o avvio generatore).

## Dimensionamento raffreddamento

BTU/ora \= Watt × 3,41

**Regola pratica:** 1 kW di potenza IT richiede circa 0,5-1 kW di raffreddamento.

# 8\. Alta disponibilità e ridondanza

## Concetti chiave

| Termine | Significato |
| ----- | ----- |
| **RTO** | Recovery Time Objective — tempo massimo per ripristinare il servizio |
| **RPO** | Recovery Point Objective — quantità massima di dati che posso perdere |

## Livelli di disponibilità

| Livello | Uptime | Downtime/anno |
| ----- | :---: | :---: |
| 99% | "due nove" | 3,65 giorni |
| 99,9% | "tre nove" | 8,76 ore |
| 99,99% | "quattro nove" | 52,6 minuti |

## Come aumentare la disponibilità

| Strategia | Effetto |
| ----- | ----- |
| RAID storage | Protegge dai guasti disco |
| Backup regolari | Permette recovery (non previene downtime) |
| Server ridondato (failover) | Elimina single point of failure |
| Multi-sito | Protegge da disastri locali |
| Load balancer | Distribuisce carico e gestisce failover |

**Regola pratica:** sistema singolo \~99%, con failover \~99,9%, multi-sito attivo-attivo \~99,99%.

# 9\. Esempi svolti completi

## Esempio 1: Pizzeria online "PizzaExpress"

**Requisiti:** 5.000 clienti registrati, picco venerdì sera, menu con foto, storico ordini 2 anni.

**Stima utenti:**

* Concorrenti: 5.000 × 10% \= 500  
* Picco (×3): 1.500 utenti  
* RPS: 1.500 × 15 / 60 \= 375 req/s

**Stima storage:**

* Menu: 100 prodotti × 500 KB \= 50 MB  
* Ordini: 200/giorno × 2 KB × 730 giorni \= 290 MB  
* **Totale con margine: \~1 GB**

**Stima banda:**

* 1.500 utenti × 500 Kbps × 0,15 \= 112 Mbps  
* **Banda necessaria: 150-200 Mbps**

**Server consigliato:**

* Web: 2 vCPU, 4 GB RAM  
* Database: 2 vCPU, 4 GB RAM, 20 GB storage

## Esempio 2: Piattaforma e-learning "ScuolaDigitale"

**Requisiti:** 10.000 studenti, 500 docenti, video lezioni HD, quiz online, picco durante esami.

**Stima utenti:**

* Concorrenti: 10.500 × 15% \= 1.575  
* Picco esami (×2): 3.150 utenti  
* RPS: 3.150 × 20 / 60 \= 1.050 req/s

**Stima storage:**

* Video: 500 corsi × 10 ore × 2 GB/ora \= 10 TB  
* Materiali: 500 corsi × 100 MB \= 50 GB  
* **Totale: \~10 TB**

**Stima banda:**

* Video HD: 800 utenti × 5 Mbps \= 4.000 Mbps  
* Altri: \~300 Mbps  
* **Banda necessaria: \~5 Gbps**

**Infrastruttura consigliata:**

* Web server: 3 × (4 vCPU, 8 GB RAM) con load balancer  
* Database: 4 vCPU, 16 GB RAM, 100 GB SSD  
* Storage video: 15 TB \+ CDN

## Esempio 3: Sistema gestionale PMI "GestioPlus"

**Requisiti:** 50 dipendenti, fatturazione/magazzino/contabilità, solo rete aziendale, disponibilità 99,5%.

**Stima utenti:**

* Concorrenti: 50 × 80% \= 40  
* RPS: 50 × 30 / 60 \= 25 req/s

**Stima storage:**

* Database: 5 GB, Documenti: 50 GB, Backup: 100 GB  
* **Totale: \~200 GB**

**Infrastruttura on-premise:**

* Server: 4 vCPU, 16 GB RAM, 500 GB RAID1  
* Switch 48 porte gigabit \+ Firewall  
* UPS 1.500 VA, NAS backup 1 TB  
* **Potenza totale: \~800 W**

# Tabella riassuntiva per l'esame

| Parametro | Formula / Stima rapida |
| ----- | ----- |
| Utenti concorrenti | Utenti totali × 10% |
| Utenti picco | Utenti concorrenti × 3 |
| RPS | Utenti picco × 15 / 60 |
| Storage/utente | 10-100 MB (semplice), 1-10 GB (media) |
| Banda/utente | 500 Kbps (web), 5 Mbps (video HD) |
| vCPU per 1000 RPS | 2-4 (web), 10-20 (app complessa) |
| Overhead DB (indici) | \+40-50% |
| Margine sicurezza | \+30% |
| UPS (VA) | Potenza (W) / 0,85 |
| Raffreddamento | Watt × 3,41 \= BTU/ora |

## Schema per rispondere all'esame

Quando ti chiedono di stimare un'architettura:

14. **Elenca i componenti** con le specifiche  
15. **Stima gli utenti** (totali → concorrenti → picco → RPS)  
16. **Calcola lo storage** (dati × retention \+ margine)  
17. **Calcola la banda** (utenti × banda/utente × contemporaneità)  
18. **Scegli i server** (taglia in base a RPS e RAM)  
19. **Considera la ridondanza** (in base all'RTO/RPO richiesto)

**Esempio di risposta:** "L'architettura proposta prevede: 2 server web (2 vCPU, 4GB), 1 server database (4 vCPU, 8GB, 50GB SSD), switch 24 porte, firewall, UPS 2000VA. La banda richiesta è \~200 Mbps. Con failover attivo-passivo si garantisce disponibilità 99,9%. Costo stimato: ..."