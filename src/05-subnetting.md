# 5. Piano di indirizzamento

## 5.1 Cos'è e perché è richiesto

Il piano di indirizzamento è la **tabella che assegna indirizzi IP a ogni subnet e dispositivo della rete**. Non è un esercizio accademico: in un progetto reale (e nella seconda prova) dimostra che sapete dimensionare correttamente gli spazi di indirizzo, evitare sovrapposizioni e applicare il subnetting in modo professionale.

Il commissario esterno valuta:
- Correttezza tecnica (subnet mask valide, range coerenti, no sovrapposizioni)
- Adeguatezza delle dimensioni (abbastanza host per i dispositivi richiesti)
- Motivazione delle scelte (perché quel blocco? perché quella maschera?)

---

## 5.2 Approccio top-down

Partite sempre dalla rete globale e suddividetela progressivamente:

```
1. Rete assegnata (es. 10.0.0.0/8)
        │
2. Macro-aree (LAN uffici, DMZ, gestione, VPN)
        │
3. Subnet per ciascuna area
        │
4. Indirizzi fissi per dispositivi critici (server, router, firewall)
```

**Non partite mai dall'indirizzo di un singolo dispositivo** per poi costruire la rete intorno: è il modo più rapido per creare sovrapposizioni e sprechi.

---

## 5.3 Subnetting FLSM: blocchi aggregati e subnet uniformi

Il **Fixed Length Subnet Masking (FLSM)** divide un blocco aggregato in subnet tutte della stessa dimensione. È il metodo più comune nella seconda prova quando la traccia descrive strutture ripetute: più laboratori identici, più piani con lo stesso numero di postazioni, più filiali con la stessa configurazione.

### Il concetto di gerarchia a due livelli

In FLSM si lavora spesso su **due livelli distinti**:

| Livello | Cosa rappresenta | Esempio |
|---------|-----------------|---------|
| **Blocco aggregato** | L'intera area logica assegnata a un gruppo di reti | Tutti i laboratori: `10.1.0.0/21` |
| **Subnet uniforme** | La singola rete all'interno del blocco | Laboratorio 1: `10.1.0.0/24`, Lab 2: `10.1.1.0/24`… |

Il blocco aggregato non viene assegnato a nessun dispositivo: è solo un "contenitore" che rende l'indirizzamento ordinato e facilita il routing (una sola route aggrega tutte le subnet figlie).

### Procedura passo per passo

**1. Contare le subnet necessarie**

Quante unità identiche devo indirizzare? (es. 5 laboratori)

**2. Scegliere la maschera della singola subnet**

In base al numero di host per subnet, con la tabella del §5.3.

**3. Calcolare il blocco aggregato**

Il blocco aggregato deve contenere *tutte* le subnet figlie. Si calcola così:

```
Bit di subnet necessari = ⌈log₂(numero di subnet)⌉
Prefisso aggregato = prefisso subnet - bit di subnet
```

**Esempio:** 5 laboratori, ciascuno con /24

- Subnet necessarie: 5 → servono 3 bit (2³ = 8 ≥ 5)
- Prefisso aggregato: 24 − 3 = **/21**
- Il blocco `10.1.0.0/21` contiene 8 subnet /24: ne uso 5, ne lascio 3 libere per crescita futura

**4. Assegnare le subnet in ordine**

Le subnet si assegnano partendo dall'indirizzo base del blocco, incrementando in modo regolare:

| Subnet | Indirizzo rete | Prefisso | Range host | Uso |
|--------|---------------|----------|------------|-----|
| Blocco aggregato | 10.1.0.0 | /21 | — | Tutti i laboratori (routing) |
| Laboratorio 1 | 10.1.0.0 | /24 | 10.1.0.1–10.1.0.254 | 30 PC + docente |
| Laboratorio 2 | 10.1.1.0 | /24 | 10.1.1.1–10.1.1.254 | 30 PC + docente |
| Laboratorio 3 | 10.1.2.0 | /24 | 10.1.2.1–10.1.2.254 | 30 PC + docente |
| Laboratorio 4 | 10.1.3.0 | /24 | 10.1.3.1–10.1.3.254 | 30 PC + docente |
| Laboratorio 5 | 10.1.4.0 | /24 | 10.1.4.1–10.1.4.254 | 30 PC + docente |
| *Riservate* | 10.1.5.0–10.1.7.0 | /24 | — | Espansione futura |

### Verifica della coerenza

Prima di scrivere la tabella finale, verificate sempre questi tre punti:

- **Il blocco aggregato contiene tutte le subnet figlie?**
  `10.1.0.0/21` va da `10.1.0.0` a `10.1.7.255` → contiene tutte le /24 assegnate ✓
- **Le subnet figlie non si sovrappongono?**
  Ogni /24 inizia esattamente dove finisce la precedente ✓
- **Nessuna subnet figlia supera i confini del blocco aggregato?**
  L'ultima assegnata è `10.1.4.0/24`, che termina a `10.1.4.255` < `10.1.7.255` ✓

### Esempio completo: scuola con più aree

Scenario tipico da seconda prova: una scuola con laboratori, aule, uffici amministrativi e DMZ, tutto da indirizzare a partire da `10.0.0.0/8`.

| Area | Blocco aggregato | Subnet singola | N. subnet | Note |
|------|-----------------|----------------|-----------|------|
| Laboratori | 10.1.0.0/21 | /24 per lab | 5 (di 8) | 30 PC ciascuno |
| Aule | 10.2.0.0/22 | /24 per aula | 4 (di 4) | 10 dispositivi ciascuna |
| Uffici amministrativi | 10.3.0.0/24 | — | unica subnet | 40 PC, server locali |
| DMZ | 10.4.0.0/29 | — | unica subnet | Web server, mail server |

🎓 **Per l'esame:** quando presentate un blocco aggregato, dichiarate sempre esplicitamente che quell'indirizzo non è assegnato a nessun dispositivo ma serve per il routing aggregato. È un dettaglio che distingue una risposta precisa da una generica.

---

## 5.4 Quanti host servono?

Prima di scegliere la maschera, contateci gli host necessari **includendo quelli nascosti**:

| Voce | Dettaglio |
|------|-----------|
| Dispositivi end-user | PC, stampanti, telefoni IP, IoT |
| Server e infrastruttura | Web server, DB, NAS, backup |
| Dispositivi di rete | Router (interfaccia), firewall (interfaccia), access point |
| Indirizzi riservati | Network address + broadcast (sempre 2 per subnet) |
| Margine di crescita | +20–30% degli host attuali |

**Formula:**

```
Host necessari = dispositivi attuali × 1,3  (margine 30%)
Maschera minima tale che: 2^n - 2 ≥ host necessari
```

**Tabella di riferimento rapido:**

| Maschera | Prefisso | Host utilizzabili |
|----------|----------|-------------------|
| 255.255.255.252 | /30 | 2 (link point-to-point) |
| 255.255.255.248 | /29 | 6 |
| 255.255.255.240 | /28 | 14 |
| 255.255.255.224 | /27 | 30 |
| 255.255.255.192 | /26 | 62 |
| 255.255.255.128 | /25 | 126 |
| 255.255.255.0   | /24 | 254 |
| 255.255.254.0   | /23 | 510 |

---

## 5.5 Indirizzi privati consigliati per l'esame

Usate sempre indirizzi privati (RFC 1918) per le reti interne:

| Blocco | Range | Uso tipico |
|--------|-------|------------|
| 10.0.0.0/8 | 10.0.0.0 – 10.255.255.255 | Reti aziendali grandi, cloud |
| 172.16.0.0/12 | 172.16.0.0 – 172.31.255.255 | Campus, sedi multiple |
| 192.168.0.0/16 | 192.168.0.0 – 192.168.255.255 | Reti piccole, home/PMI |

🎓 Per l'esame, `10.0.0.0/8` è la scelta più flessibile: permette di creare molte subnet senza rischio di esaurimento.

---

## 5.6 Struttura della tabella di indirizzamento

La risposta all'esame deve presentare il piano in forma tabellare. Esempio per una rete aziendale con DMZ:

| Subnet | Indirizzo rete | Maschera | Prefisso | Gateway | Range host | Broadcast | Dispositivi |
|--------|---------------|----------|----------|---------|------------|-----------|-------------|
| LAN Uffici | 10.0.1.0 | 255.255.255.0 | /24 | 10.0.1.1 | 10.0.1.2–10.0.1.254 | 10.0.1.255 | 80 PC, stampanti |
| DMZ | 10.0.2.0 | 255.255.255.248 | /29 | 10.0.2.1 | 10.0.2.2–10.0.2.6 | 10.0.2.7 | Web server, mail server |
| Gestione | 10.0.3.0 | 255.255.255.240 | /28 | 10.0.3.1 | 10.0.3.2–10.0.3.14 | 10.0.3.15 | Switch, firewall, NAS |
| Link WAN | 203.0.113.0 | 255.255.255.252 | /30 | — | 203.0.113.1–.2 | 203.0.113.3 | Router ISP ↔ firewall |

**Convenzioni consigliate:**

- `.1` → gateway della subnet (interfaccia router/firewall)
- `.2`, `.3`, `.4`… → server con IP fisso
- Da `.11` in su → DHCP dinamico per end-user
- Documentare sempre le scelte: *"La DMZ usa /29 perché ospita al massimo 3 server pubblici con margine per 3 futuri"*

---

## 5.7 Errori frequenti da evitare

| Errore | Esempio sbagliato | Correzione |
|--------|--------------------|------------|
| Subnet sovrapposte | LAN: 10.0.1.0/24 e DMZ: 10.0.1.128/25 | Le due subnet si sovrappongono: scegliere blocchi separati |
| Maschera troppo piccola | /30 per 20 PC | /30 ha solo 2 host: usare /27 o /26 |
| Maschera esagerata | /8 per 5 dispositivi | Spreco inutile: usare /29 o /28 |
| Gateway fuori subnet | Rete 10.0.1.0/24, gateway 10.0.2.1 | Il gateway deve essere nella stessa subnet |
| Indirizzo di rete assegnato a host | Host con IP 10.0.1.0 | È il network address: non assegnabile |
| Broadcast assegnato a host | Host con IP 10.0.1.255 | È il broadcast address: non assegnabile |

---

## 5.8 Schema di risposta per l'esame

Quando la traccia chiede il piano di indirizzamento, strutturate così:

1. **Dichiarate il blocco scelto** e motivatelo: *"Si utilizza il blocco 10.0.0.0/8 (RFC 1918) per la rete privata, sufficiente per tutte le subnet previste e per eventuali espansioni future."*

2. **Elencate le subnet** necessarie in base all'architettura: LAN, DMZ, rete di gestione, link point-to-point verso ISP.

3. **Dimensionate ogni subnet** contando i dispositivi + margine.

4. **Presentate la tabella** con tutte le colonne rilevanti.

5. **Assegnate IP fissi** ai dispositivi critici (server, interfacce router/firewall) e dichiarate i range DHCP.