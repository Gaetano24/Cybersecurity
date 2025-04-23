
## 🖥️ **Paradigma Client-Server**

### 🔍 Cos'è

È un modello di comunicazione in cui:

- Il **client** (utente) **richiede un servizio**.
- Il **server** (fornitore) **risponde alla richiesta**.

> Esempio: quando visiti un sito web, il tuo browser è il client e il server web (es. Apache, Nginx) fornisce la pagina.

### 📡 Server

- È un **host sempre attivo** (_always-on_).
- Ha un **indirizzo IP permanente**.
- È spesso ospitato in **data center** → per garantire **scalabilità, affidabilità e prestazioni** elevate.

### 🧑‍💻 Client

- Si connette al server per richiedere dati o servizi.
- Può essere **connesso in modo intermittente**.
- Spesso ha un **IP dinamico** (assegnato dal provider temporaneamente).
- **Non comunica direttamente con altri client**.

### 📂 Esempi di protocolli Client-Server

- **HTTP** → Web browsing
- **IMAP/POP** → Email
- **FTP** → Trasferimento file

![[Pasted image 20250418124737.png]]

---

## 🌐 **Paradigma Peer-to-Peer (P2P)**

### 🔍 Cos'è

È un modello in cui **ogni nodo è sia client che server**. Gli utenti condividono risorse **tra pari**, senza un punto centrale di controllo.

> Esempio: reti di file sharing come **BitTorrent** o sistemi decentralizzati come **blockchain**.

### 📌 Caratteristiche

- Tutti i nodi sono **equivalenti** (peers).
- La comunicazione è **diretta tra dispositivi**.
- Nessun server centrale → maggiore **resilienza**.
- I peer sono connessi ad intermittenza e possono variare i loro indirizzi IP

### 📂 Esempi di protocolli P2P

- P2P file sharing

![[Pasted image 20250418124715.png]]

---

## 🧠 **Processi**

### 🔍 Cos'è un processo?

Un **processo** è un **programma in esecuzione**. Ha un proprio spazio di memoria, variabili, e stato di esecuzione.

In rete:

- Ogni processo è identificato da:
    
    - **Indirizzo IP** (identifica l’host su cui gira)
    - **Porta** (identifica il processo specifico su quell’host)


> Esempio: un server web in ascolto su IP `192.168.1.10`, porta `80`.

---

## 🔄 **Comunicazione tra processi**

### 🔗 Cos’è

È lo **scambio di dati tra processi**, che può avvenire:

- **Localmente** (sullo stesso dispositivo): si parla in questo caso di **comunicazioni inter-processo**.
- **In Remoto** (tramite rete)

In ambito di rete, la comunicazione è tra **processi su host diversi**.

### 📬 Come avviene

- Attraverso l’uso di **socket**
- Seguendo protocolli come **TCP** o **UDP**

---

## 🧩 **Socket**

### 🔍 Cos'è

Un **socket** è un’interfaccia software che permette la comunicazione tra processi su diversi dispositivi attraverso la rete.

> Puoi vederlo come un **"punto di connessione"** tra due processi.

### 🧱 Identificatore unico:

Un socket è identificato da:

```
(IP address, numero di porta, protocollo)
```

### ⚙️ Tipi di socket

|Tipo|Protocollo|Caratteristiche|
|---|---|---|
|Stream|TCP|Affidabile, orientato alla connessione|
|Datagram|UDP|Veloce, non affidabile, senza connessione|

---

### 💬 Comunicazione con socket (semplificata)

**Client:**

1. Crea un socket
2. Specifica IP e porta del server
3. Si connette e invia richieste

**Server:**

1. Crea un socket
2. Si mette **in ascolto** su una porta specifica
3. Accetta connessioni e risponde


![[Pasted image 20250418125159.png]]

---

## 📡 **Protocolli del Livello Applicazione**

I **protocolli di livello applicazione** definiscono **come avviene la comunicazione tra processi applicativi** che girano su host diversi nella rete.

Sono fondamentali per il funzionamento di servizi come **web, email, file transfer, streaming, DNS**, ecc.

---

### 📋 Cosa definiscono?

#### 1. **Tipi di messaggi scambiati**

- Determinano **la natura della comunicazione**.
- Esempi:
    
    - `request` → richiesta di un servizio
    - `response` → risposta alla richiesta
    - altri: `acknowledgment`, `error`, `command`, etc...


#### 2. **Sintassi del messaggio**

- Struttura e formato del messaggio.
- Definisce:
    
    - **Campi presenti** (es. header, body, status code)
    - **Ordine dei campi**
    - Come i campi sono **separati e interpretati** (es. delimitatori, codifica)

> Esempio in HTTP:

```
GET /index.html HTTP/1.1
Host: www.example.com
```


#### 3. **Semantica del messaggio**

- Il **significato del contenuto** nei vari campi.
- Esempi:
    
    - In HTTP, `200 OK` significa "richiesta andata a buon fine"
    - In SMTP, il comando `MAIL FROM:` indica il mittente


#### 4. **Regole di comunicazione (protocollo di scambio)**

- Definisce **quando e come** i messaggi vengono inviati e ricevuti.
- Include:
    
    - L’**ordine delle operazioni**
    - Le condizioni in cui un messaggio può o deve essere inviato
    - Come gestire errori o timeout


> Esempio: in HTTP, il client invia sempre per primo una richiesta, e poi il server risponde.

---

### 📂 Protocolli Aperti vs Proprietari

#### 🧷 **Protocolli Aperti**

- **Pubblici e documentati**
- Tutti possono implementarli e utilizzarli
- Spesso standardizzati da enti (IETF, W3C, ISO)
- Esempi:
    
    - **HTTP**, **SMTP**, **DNS**, **FTP**, **IMAP**


#### 🔒 **Protocolli Proprietari**

- Sviluppati da aziende o organizzazioni private
- **Non sempre pubblici** o completamente documentati
- L’uso può essere **limitato o soggetto a licenza**
- Esempi:
    
    - **Skype (versioni precedenti)**, **WhatsApp (protocolli interni)**, **Microsoft Exchange**

---

