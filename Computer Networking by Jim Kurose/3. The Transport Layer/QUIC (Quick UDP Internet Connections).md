
## **Cos'è QUIC?**

QUIC è un **protocollo di trasporto moderno** sviluppato da Google e ora standardizzato da IETF. È progettato per offrire **connessioni Internet più rapide, sicure e resilienti** rispetto a TCP. QUIC opera sopra **UDP**, ma incorpora funzionalità avanzate normalmente fornite da TCP e TLS, spostando molte responsabilità al **livello applicativo**.

---

## **Contesto e motivazione**

QUIC nasce per superare alcune limitazioni strutturali di TCP, in particolare:

- Lentezza nella fase di handshake iniziale
    
- Blocco per head-of-line (HOL) in presenza di stream multipli
    
- Scarsa mobilità (TCP non sopporta bene il cambio di IP)
    
- Modifiche lente al protocollo TCP a causa della sua integrazione nel kernel


> [!NOTE] 
> Il **blocco Head-of-Line (HOL blocking)** è un problema che si verifica quando un **pacchetto in testa a una coda** impedisce l'elaborazione di altri pacchetti **anche se questi ultimi non dipendono da esso**. In altre parole, **un ritardo o una perdita su un flusso blocca anche gli altri flussi**, rallentando l'intera comunicazione.

---

## **Caratteristiche principali di QUIC**

###  **Basato su UDP**

- QUIC utilizza **UDP come trasporto grezzo**, evitando le rigidità del TCP.
    
- Questo consente una **maggiore flessibilità nell’evoluzione** del protocollo, implementato spesso in **user space**, senza modifiche al kernel.


### **Sicurezza integrata**

- QUIC **integra TLS 1.3 direttamente nel protocollo** di trasporto.
    
- La crittografia è obbligatoria e fa parte del core design.
    
- La negoziazione crittografica e di trasporto avviene in un **unico handshake**, completabile in **1 RTT** (round-trip time) o **0-RTT** per le connessioni riutilizzate.


###  **Multiplexing di stream indipendenti**

- QUIC supporta **stream multipli indipendenti** all’interno della stessa connessione.
    
- Ogni stream ha buffering e controllo separato, evitando l’**HOL blocking** (problema tipico di HTTP/2 su TCP).
    
- Se un pacchetto viene perso su uno stream, **non blocca gli altri stream**.


### **Controllo della congestione**

- QUIC implementa un **controllo della congestione simile a TCP**, ma può essere aggiornato più rapidamente poiché è fuori dal kernel.
    
- Supporta algoritmi moderni come **CUBIC** o **BBR**.


### **Connessioni resilienti**

- Supporta **migrazione di connessione**, permettendo il cambio di indirizzo IP o rete (es. da Wi-Fi a LTE) **senza dover ristabilire la connessione**.
    
- Le connessioni sono identificate tramite **Connection ID** indipendenti dall’IP.


---

### **Vantaggi di QUIC**

| Aspetto          | Vantaggio                                                   |
| ---------------- | ----------------------------------------------------------- |
| **Latenza**      | Handshake combinato TLS + trasporto → minore tempo di avvio |
| **Affidabilità** | Meccanismi di ritrasmissione, cifratura, congestion control |
| **Efficienza**   | Multiplexing nativo → elimina il blocco head-of-line        |
| **Mobilità**     | Cambi di rete/IP gestiti senza interrompere la connessione  |
| **Sicurezza**    | TLS 1.3 integrato obbligatorio, cifratura end-to-end        |

---

### **QUIC in pratica: HTTP/3**

QUIC è il protocollo di trasporto su cui si basa **HTTP/3**, la nuova versione del protocollo HTTP:

- HTTP/1.1 e HTTP/2 usano TCP → soggetti a head-of-line blocking.
    
- HTTP/3 su QUIC evita questo problema e migliora la velocità di caricamento delle pagine web, soprattutto su reti mobili o instabili.


---