
## 🔐 **Network Security: Sniffing, Spoofing e DoS**

La **sicurezza di rete** riguarda la protezione dei dati e delle risorse in una rete da accessi non autorizzati, attacchi e perdite. È fondamentale per garantire che le comunicazioni siano affidabili e protette.

---

### 🕵️‍♂️ Packet Interception (Sniffing)

- Consiste **nell'intercettare i pacchetti** trasmessi in una rete.
- Gli attaccanti usano strumenti chiamati **sniffer** (es. Wireshark).
- Funziona soprattutto in reti non criptate o con hub.
- Obiettivo: **rubare informazioni sensibili** (es. password, cookie, email).

![[Pasted image 20250417201643.png]]

---

### 🎭 IP Spoofing

- L’attaccante **falsifica l’indirizzo IP** di origine nei pacchetti.
- Serve per:
    
    - Mascherare la propria identità.
    - **Ingannare un host** per fargli credere di parlare con un altro.
    - Facilitare altri attacchi (es. DoS, hijacking).
    
- Compromette **autenticità e integrità** della comunicazione.

![[Pasted image 20250417201733.png]]

---

### 💥 Denial of Service (DoS)

- Obiettivo: **rendere un servizio o rete inutilizzabile** sovraccaricandolo di richieste.
- Variante più potente: **Distributed DoS (DDoS)** → attacco da più fonti simultanee.
- Effetti:
    
    - Blocco temporaneo di servizi.
    - Possibili danni economici e reputazionali.


![[Pasted image 20250417201817.png]]


---

## 🛡️ **Linee di Difesa nella Sicurezza di Rete**

Per proteggere una rete si usano diverse misure combinate:

### 1. ✅ Autenticazione

- Verifica **l’identità** di utenti/sistemi.
- Esempi: password, OTP, certificati digitali, autenticazione a due fattori.

### 2. 🔒 Confidenzialità

- Protegge i dati da accessi non autorizzati.
- Si ottiene tramite **crittografia** (es. TLS, VPN, AES).

### 3. 🧾 Integrità

- Garantisce che i dati **non siano stati alterati** durante il trasferimento.
- Tecniche: hash (SHA-256), firme digitali.

### 4. 🚫 Restrizione negli Accessi

- Controllo su **chi può accedere** a cosa.
- Si realizza con **ACL (Access Control Lists)**, ruoli, autorizzazioni.

### 5. 🔥 Firewalls

- Filtrano il traffico in entrata/uscita **in base a regole**.
- Possono essere:
    
    - Hardware o software.
    - Basati su IP, porte, protocolli, contenuto.

---

## 🤖 **Botnet – Cosa Sono e Perché Sono Pericolose**


### 🔍 Definizione

Una **botnet** (da _robot network_) è una rete di dispositivi infettati da **malware**, controllati **remotamente da un attaccante** (chiamato _botmaster_ o _bot herder_), **senza che l’utente se ne accorga**.

Ogni dispositivo infetto è chiamato **bot** o **zombie**.

---

### ⚙️ Come Funziona

1. L’attaccante **diffonde malware** (es. tramite email, siti infetti o software pirata).
2. I dispositivi infettati **si connettono a un server di comando e controllo (C&C)**.
3. Il botmaster invia comandi a tutta la rete (o parte di essa), ad esempio per:
    
    - **Lanciare attacchi DDoS**
    - **Inviare spam**
    - **Rubare dati**
    - **Minare criptovalute**
    - **Distribuire altri malware**

---

### 📡 Modalità di Controllo

- **C&C centralizzato**: tutti i bot comunicano con un server specifico.
- **Peer-to-peer (P2P)**: i bot comunicano tra loro → più difficile da fermare.
- **Botnet-as-a-Service (BaaS)**: affitto botnet pronte all’uso nel dark web.

---

### ⚠️ Perché Sono Pericolose

- **Difficili da rilevare**: i dispositivi infetti funzionano normalmente.
- **Danno distribuito**: migliaia o milioni di bot → attacchi potenti e su larga scala.
- Possono colpire **PC, server, router, IoT, smartphone** (qualsiasi cosa connessa a Internet).

---
