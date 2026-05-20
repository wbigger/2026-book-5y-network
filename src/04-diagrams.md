
# 4. Diagramma di rete

## 4.1 Due livelli, due domande diverse

Un progetto di rete richiede **almeno due diagrammi distinti**, che rispondono a domande diverse:

| Diagramma | Domanda | Livello ISO/OSI |
|-----------|---------|-----------------|
| **Rete fisica/logica** | Come sono collegati i dispositivi? | L2–L3 (switch, router) |
| **Architettura applicativa** | Come comunicano i servizi? | L7 (client, server, API, DB) |

Confonderli è uno degli errori più comuni nella seconda prova. Un commissario esterno si aspetta che sappiate distinguerli e usarli entrambi nel momento giusto.

---

Ecco la sezione 4.2 aggiornata, da sostituire nel documento:

---

## 4.2 Diagramma L2–L3: la rete fisica/logica

Questo schema mostra **come i pacchetti circolano fisicamente nella rete**: cavi, switch, router, firewall, access point. Ogni collegamento rappresenta un link fisico (Ethernet, fibra, wireless).

**Elementi tipici:**
- Dispositivi di rete: switch L2, router, firewall, access point
- End-device: PC, server, stampanti (ma **non** il tipo di applicazione che girano)
- Connessioni etichettate con interfaccia e indirizzo IP
- Indicazione delle VLAN se presenti
- Separazione visiva tra LAN, DMZ, Internet

**Esempio schematico:**

```
         Internet
             │
     [firewall/router]
          /        \
    [Switch DMZ]  [Switch LAN]
         │              │
    [Web Server]   ┌────┴────┐
                [PC-1]    [Server]
             192.168.1.10  192.168.1.20
```

> L'architettura interna del perimetro di sicurezza (numero di firewall, configurazione screened host o screened subnet) dipende dai requisiti del progetto e viene dettagliata nella sezione dedicata alla sicurezza perimetrale.

🎓 **Attenzione:** in questo schema lo smartphone o il laptop di un utente esterno **non si collega direttamente al web server**. Passa attraverso Internet → firewall/router → DMZ. Disegnare una freccia diretta smartphone→server è un errore concettuale grave: significa ignorare tutta l'infrastruttura di rete intermedia.

---

## 4.3 Diagramma L7: l'architettura applicativa

Questo schema mostra **come i componenti software interagiscono**: browser, web server, application server, database, servizi esterni. I collegamenti rappresentano protocolli applicativi (HTTP/S, SQL, SMTP, API REST…), non cavi fisici.

**Elementi tipici:**
- Client (browser, app mobile, desktop)
- Web server / reverse proxy
- Application server
- Database server
- Servizi esterni (autenticazione, CDN, API di terze parti)
- Protocollo e porta su ogni freccia

**Esempio schematico:**

```
[Browser utente] --HTTPS:443--> [Web Server / Nginx]
                                        │
                                  HTTP:8080
                                        ▼
                              [App Server / Node.js]
                               /                  \
                         SQL:3306             HTTPS:443
                              ▼                    ▼
                         [Database]         [Servizio email
                          MariaDB            esterno SMTP]
```

🎓 In questo schema non compaiono switch, router o firewall: non è il loro posto. Il commissario non si aspetta di vedere "switch" tra il browser e il web server in un diagramma applicativo.

---

## 4.4 Come usarli nella seconda prova

La traccia chiede spesso entrambi, anche se non lo dice esplicitamente. Un progetto completo include:

1. **Prima il diagramma L7** (architettura applicativa): aiuta a capire quali server servono e come si parlano.
2. **Poi il diagramma L2–L3** (rete fisica): definisce dove stanno fisicamente quei server, come sono collegati, quali VLAN e firewall li proteggono.

**Schema mentale da usare:**

> *"Nel diagramma applicativo metto i servizi e i protocolli. Nel diagramma di rete metto i dispositivi fisici e gli indirizzi IP."*

Se la traccia chiede un solo schema, scegliete quello più pertinente alla domanda — ma menzionate esplicitamente che esistono entrambi i livelli di rappresentazione e indicate quale state usando.

---

## 4.5 Errori frequenti da evitare

| Errore | Perché è sbagliato | Correzione |
|--------|--------------------|------------|
| Smartphone collegato con una freccia diretta al server | Ignora router, firewall, Internet | Mostrare il percorso completo o usare una nuvola "Internet" come nodo |
| Switch e router nel diagramma applicativo | Sono dispositivi L2–L3, non L7 | Tenerli nel diagramma di rete |
| Protocolli (HTTP, SQL) nel diagramma L2–L3 | Appartengono al livello applicativo | Etichettare i link con interfacce e IP, non con protocolli |
| Frecce senza etichetta | Il commissario non sa cosa rappresentano | Etichettare sempre: protocollo, porta, o tipo di link |
| Router di sede A collegato direttamente al router di sede B | Le due sedi non sono fisicamente adiacenti: tra loro c'è sempre una rete di trasporto (Internet o WAN dell'ISP) | Inserire sempre una nuvola "Internet" o "WAN" tra i due router; se il collegamento è cifrato, indicare che si tratta di un tunnel VPN |