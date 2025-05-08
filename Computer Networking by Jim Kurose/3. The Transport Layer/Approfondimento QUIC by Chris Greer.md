
## **QUIC**

QUIC è un protocollo di trasporto sviluppato inizialmente da Google e poi standardizzato da IETF. Mira a migliorare le prestazioni di HTTP/2 e successivi, riducendo la latenza e migliorando la sicurezza rispetto a TCP + TLS.

---

## 🔹 **QUIC su UDP**

QUIC utilizza **UDP** (User Datagram Protocol) come trasporto sottostante anziché TCP, per diversi motivi:

- **Controllo Utente**: Usando UDP, QUIC può implementare le sue logiche di trasporto (come congestion control, ritrasmissioni, flow control) a livello applicativo, superando le limitazioni del TCP.
    
- **Evita handshake TCP**: TCP richiede un 3-way handshake per ogni nuova connessione, QUIC no.
    
- **Multiplexing integrato**: Evita il problema del "Head-of-Line blocking" tipico del TCP grazie alla sua struttura di stream indipendenti.
    
- **Aggiramento NAT/firewall**: UDP è più semplice da gestire in ambienti NAT/firewalled, soprattutto per peer-to-peer o mobile networking.

**Nota**: UDP è "connection-less", ma QUIC costruisce sopra un layer che offre **connessioni affidabili e sicure** come TCP, ma con più efficienza.

---

## 🔹 **0-RTT (Zero Round-Trip Time Resumption)**

QUIC supporta **0-RTT** per ridurre la latenza durante la ripresa di connessioni precedenti.

- Funziona solo con **sessioni precedentemente stabilite** tra client e server.
    
- Il client invia dati **applicativi nel primo pacchetto** insieme all’handshake (prima risposta del server).
    
- Utilizza **session ticket o PSK (Pre-Shared Key)** ricevuti durante la prima connessione.
    
- **Rischi di sicurezza**: 0-RTT è vulnerabile al replay attack. QUIC adotta contromisure, come anti-replay windows.
    

📌 **Vantaggi**:

- Riduce la latenza iniziale.
    
- Migliora le prestazioni su connessioni instabili (es. mobile).

---

## 🔹 **TLS in QUIC (TLS 1.3 Integration)**

QUIC integra **TLS 1.3** direttamente nel protocollo di trasporto, a differenza di TCP che richiede uno strato separato.

- TLS fornisce **confidenzialità, integrità e autenticazione**.
    
- L'handshake TLS avviene **all’interno del flusso QUIC stesso** (stream criptati).
    
- Nessuna necessità di handshake TCP → meno round-trip.
    

🧠 **Benefici**:

- Più veloce: TLS handshake e trasporto sono unificati.
    
- Più sicuro: Nessuna esposizione dei metadati TLS a livello inferiore.
    
- Migliore gestione delle chiavi: QUIC usa **separate encryption keys** per ogni fase (Initial, Handshake, 1-RTT, 0-RTT).

---

## 🔹 **Flow Control**

Il **flow control** in QUIC evita che il mittente inondi il ricevente con troppi dati.

Gestito a **due livelli**:

1. **Stream-level**: ogni stream ha limiti separati.
    
2. **Connection-level**: limite globale per tutta la connessione.
    

📥 **Meccanismo**:

- Il ricevente invia **crediti di ricezione (WINDOW frames)**.
    
- Il mittente può inviare dati solo entro quei limiti.
    
- Se il ricevente è lento a processare, può ridurre le finestre per evitare congestione.
    

➡️ **Vantaggi rispetto a TCP**:

- Multiplexing senza interferenza: ogni stream può essere gestito in modo indipendente.
    
- Migliore gestione del buffering.

---

## 🔹 **Loss Recovery (Gestione delle Perdite)**

QUIC non usa gli algoritmi di ritrasmissione TCP, ma implementa un proprio sistema più moderno.

🔍 **Caratteristiche**:

- **ACKs espliciti**: i pacchetti QUIC hanno numeri di sequenza unici e i ricevuti vengono confermati tramite ACK.
    
- **ACK Delay**: il mittente può stimare l’RTT (Round Trip Time) considerando il ritardo noto negli ACK.
    
- **Ritrasmissione selettiva**: solo i pacchetti mancanti vengono ritrasmessi.
    
- **Pacing**: invio dei pacchetti con timing controllato per evitare burst di traffico.
    
- Supporta **congestion control personalizzato**, ad esempio Cubic o BBR.
    

📌 **Importante**: QUIC non è vincolato dalle meccaniche TCP → può evolvere più velocemente (senza dover cambiare kernel dei sistemi operativi).

---

## **Confronto tra Handshake TCP e QUIC**

### 🔄 **TCP + TLS + HTTP (Tradizionale)**

#### 🔹 **1. TCP Handshake (3-Way)**

- Il client invia un **SYN**.
    
- Il server risponde con **SYN-ACK**.
    
- Il client risponde con **ACK**.

> 👉 Serve **1 RTT** solo per stabilire la connessione TCP.


#### 🔹 **2. TLS Handshake (es. TLS 1.2 o 1.3)**

- Il client invia un messaggio `ClientHello`.
    
- Il server risponde con `ServerHello` e chiavi.
    
- Il client e il server completano la negoziazione di chiavi.

> 👉 TLS 1.2 richiede **2 RTT**; TLS 1.3 richiede **1 RTT**.


#### 🔹 **3. Richiesta HTTP**

- Dopo che TLS è terminato, il client può inviare la **prima richiesta HTTP** (es. `GET /`).

> ⏱️ **Totale: 2 o 3 RTT** prima della prima richiesta utile.

---

### ⚡ **2. QUIC (con TLS 1.3 integrato)**

QUIC **integra** il handshake **TLS 1.3** direttamente **nel trasporto** (sopra UDP).

#### 🔹 **1. Client Hello (Initial)**

- Il client invia un pacchetto con:
    
    - Inizio handshake TLS 1.3 (`ClientHello`)
        
    - Numero di connessione QUIC
        
    - Dati applicativi **(se 0-RTT è possibile)**
    

#### 🔹 **2. Server Hello (Handshake)**

- Il server risponde con:
    
    - `ServerHello` e parametri TLS
        
    - Conferma e chiavi
    

#### 🔹 **3. Stream Applicativo**

- Una volta derivata la chiave di 1-RTT, il client può **immediatamente inviare dati HTTP/3** su uno stream QUIC.

> ⏱️ **Totale: 0-1 RTT** (con 0-RTT la richiesta HTTP può essere nel primo pacchetto).



![[Pasted image 20250508133442.png]]


---


