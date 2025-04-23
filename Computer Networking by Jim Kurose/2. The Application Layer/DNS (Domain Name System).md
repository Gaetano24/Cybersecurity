
## 🌐 **DNS (Domain Name System)**

### 📌 1. **Servizi del DNS**

Il DNS fornisce:

- 🔁 **Traduzione di nomi a indirizzi IP**  
    Es: `www.google.com` → `142.250.184.100`
    
- 🧭 **Alias** per host con nomi complicati  
    Es: `mail.google.com` può puntare a un server con nome tecnico interno
    
- 📩 **Servizio di email routing**  
    Usa record **MX** per sapere dove inviare la posta
    
- 📌 **Bilanciamento del carico**  
    Tramite più indirizzi IP per un nome (round-robin DNS)



---

### 🧱 2. **Struttura del DNS**

- È un sistema **distribuito** e **gerarchico**
    
- Organizzato in **zone** gestite da diversi server
    
- Ogni nome (es. `www.unimi.it`) viene risolto partendo dalla **radice** verso il basso

---

### 🌲 3. **Gerarchia del DNS**

![[Pasted image 20250420162454.png]]


- **Root DNS server**: sa dove trovare i TLD (Top-Level Domain) server
    
- **TLD servers**: gestiscono domini come `.com`, `.org`, `.it`
    
- **Authoritative DNS servers**: contengono i record finali per i nomi di dominio


---

### 🔁 4. **Query Iterative vs Ricorsive**

#### 🔄 **Iterative**

- Il client chiede al DNS resolver, che risponde con un **riferimento** (es. “prova questo server”)
    
- Il client continua a interrogare i server indicati

![[Pasted image 20250420162400.png]]

#### 🔃 **Ricorsive**

- Il DNS resolver si occupa **di tutto**: interroga tutti i server necessari e restituisce **la risposta finale** al client

![[Pasted image 20250420162305.png]]

---

### 📦 5. **Caching**

- I resolver memorizzano le risposte DNS in una **cache locale**.
    
- Se una query è già in cache, si **risparmia tempo e traffico**.
    
- I dati hanno una **TTL (Time-To-Live)** che indica per quanto tempo sono validi.


---

### 📋 6. **Tipi di DNS Records**


![[Pasted image 20250420162104.png]]

| Tipo  | Significato                           | Esempio                          |
| ----- | ------------------------------------- | -------------------------------- |
| A     | Nome → IPv4 address                   | `www.unimi.it → 160.78.24.6`     |
| AAAA  | Nome → IPv6 address                   | `www → 2001:db8::1`              |
| CNAME | Alias di un altro nome                | `mail → gmail.com`               |
| MX    | Mail exchange                         | Usato per routing della posta    |
| NS    | Name Server                           | Indica i DNS server autoritativi |
| TXT   | Info testuale (es. per SPF, verifica) | Usato anche per sicurezza        |
| SOA   | Start of Authority (inizio zona DNS)  | Info sulla zona e TTL default    |

---

### 📨 7. **DNS Protocol Messages**

DNS usa **UDP (porta 53)**, talvolta **TCP (per messaggi grandi o zone transfer)**

- **Header**: ID, flag, numero di record
    
- **Domanda (Question)**: nome richiesto e tipo (es. A, MX…)
    
- **Risposta (Answer)**: i record richiesti (se presenti)
    
- **Authority**: server autoritativi coinvolti
    
- **Additional**: info extra utili alla risoluzione


![[Pasted image 20250420162605.png]]

---

## 🧭 **nslookup - Network Server Lookup**

`nslookup` è un comando usato per interrogare i server DNS e ottenere informazioni su nomi di dominio o indirizzi IP.

### 📌 Comandi principali:

- `nslookup`: entra in modalità interattiva.
    
- `nslookup nome_dominio`: ottiene l’indirizzo IP di un dominio (es. `nslookup google.com`).
    
- `nslookup indirizzo_IP`: esegue una reverse lookup (es. `nslookup 8.8.8.8`).
    
- `server indirizzo_DNS`: cambia server DNS da usare.
    
- `set type=ANY | A | AAAA | MX | NS | CNAME | PTR`: specifica il tipo di record DNS da cercare.
    
    - `A`: indirizzo IPv4
    - `AAAA`: indirizzo IPv6
    - `MX`: mail server
    - `NS`: nameserver
    - `CNAME`: alias
    - `PTR`: reverse lookup

---
### **Esempio 1: Risoluzione di tipo A**

**Obiettivo:** ottenere l’indirizzo IPv4 associato a un nome di dominio.

#### 📌 Comando:

```bash
nslookup -type=A google.com
```

#### ✅ Risultato tipico:

```
Server:  8.8.8.8
Address: 8.8.8.8#53

Non-authoritative answer:
Name:    google.com
Address: 142.250.184.206
```

#### 🧠 Spiegazione:

- Il **record A** mappa un **nome di dominio** a un **indirizzo IPv4**.
- Utile quando vuoi sapere **dove si trova fisicamente** (a livello di rete) un dominio.

---

### **Esempio 2: Risoluzione di tipo NS**

**Obiettivo:** ottenere i **name server** autorevoli per un dominio.

#### 📌 Comando:

```bash
nslookup -type=NS google.com
```

#### ✅ Risultato tipico:

```
Server:  8.8.8.8
Address: 8.8.8.8#53

Non-authoritative answer:
google.com nameserver = ns3.google.com
google.com nameserver = ns1.google.com
google.com nameserver = ns2.google.com
google.com nameserver = ns4.google.com
```

#### 🧠 Spiegazione:

- Il **record NS** (Name Server) indica **quali server DNS sono responsabili** (autoritativi) per un dominio.
- Serve per sapere **chi gestisce le informazioni DNS** di quel dominio.
- I name server sono quelli interrogati per ottenere altri record (A, MX, ecc.).

---
### 🔍 **"Non-authoritative answer" — Cosa significa?**

Quando usi `nslookup` (o un altro strumento DNS) e vedi:

```
Non-authoritative answer:
```

significa che **la risposta DNS che stai ricevendo non proviene direttamente da un name server autorevole per quel dominio**, ma da un **DNS cache** intermedio — tipicamente il **resolver** del tuo provider o di Google (come 8.8.8.8), che ha **salvato in memoria** una copia recente della risposta.

---

## 🕵️‍♂️ **Wireshark - Network Protocol Analyzer**

Wireshark è un tool grafico per l'analisi dettagliata del traffico di rete, incluso il traffico DNS.

### 🎯 Filtri DNS utili:

- `dns`: mostra tutto il traffico DNS
- `udp.port == 53`: mostra tutto il traffico DNS via UDP
- `dns.qry.name == "google.com"`: richieste DNS per un dominio specifico
- `dns.flags.response == 1`: mostra solo le risposte DNS
- `dns.flags.rcode != 0`: mostra errori DNS (es. NXDOMAIN)

### 🧩 Cosa osservare nei pacchetti DNS:

- **Query**: nome richiesto (`Name`)
- **Response**: indirizzi IP restituiti (`Answers`)
- **Authority**: server autorevoli (`Authority section`)
- **Additional**: record aggiuntivi (es. IP dei name server)

---