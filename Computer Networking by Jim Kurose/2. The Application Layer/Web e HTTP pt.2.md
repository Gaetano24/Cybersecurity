
## **🗃️ Web Cache (o Proxy Cache)**

### 🔍 Cos'è

Una **web cache** è un sistema (es. server proxy o browser) che **memorizza copie delle risposte HTTP** (es. pagine, immagini...) per **servirle più velocemente** a future richieste identiche.

### 🎯 Obiettivi

- **Ridurre la latenza**: serve contenuti localmente, senza contattare il server.
- **Alleggerire il carico sui server**.
- **Risparmiare banda**.

### 🧪 Funzionamento base

1. Il client fa una richiesta a un oggetto.
2. La cache controlla se ha una copia **valida e aggiornata**:
    
    - ✅ Se sì → serve l’oggetto direttamente.
    - ❌ Se no → inoltra la richiesta al server, aggiorna la cache e poi serve la risposta.

---

## 🧾 **Conditional GET**

### 🔍 Cos'è

È un tipo speciale di richiesta HTTP usata **per aggiornare la cache solo se necessario**.

### 🧠 Come funziona

Il client invia un `GET` includendo:

- `If-Modified-Since` oppure
    
- `If-None-Match` (con etag)


Se **l'oggetto non è cambiato**:

> Il server risponde con `304 Not Modified` e **non invia il corpo** → risparmio di tempo e banda.

Se **l'oggetto è stato aggiornato**:

> Il server risponde con `200 OK` e invia la nuova versione.

---

## 🌐 **Versioni HTTP: 1.0 vs 1.1 vs 2 vs 3**

|Caratteristica|**HTTP/1.0**|**HTTP/1.1**|**HTTP/2**|**HTTP/3**|
|---|---|---|---|---|
|Anno introduzione|1996|1997|2015|2022|
|Connessione|Non persistente|Persistente di default|Multiplexing su 1 conn.|Multiplexing su **QUIC** (UDP)|
|Pipeline|❌|✅ ma con limiti|❌ (sostituito da mux)|✅ migliorato|
|Compress. header|❌|❌|✅ (HPACK)|✅ (QPACK)|
|Protocollo di trasporto|TCP|TCP|TCP|**UDP con QUIC**|
|Performance|🐢|🐢|⚡ molto meglio|⚡⚡ ancora più veloce|

---

### Schema HTTP/2

![[Pasted image 20250420155646.png]]

---

### 🧩 Note chiave

- **HTTP/1.0**:
    
    - Non supporta connessioni persistenti
    - Ogni oggetto richiede una nuova connessione
    
- **HTTP/1.1**:
    
    - Connessione persistente (`keep-alive`)
    - Aggiunge caching, pipelining (ma non sempre efficiente)
    - Introduce `Host:` header (multi-sito su stesso IP)
    
- **HTTP/2**:
    
    - Una sola connessione TCP con **multiplexing** (più richieste contemporanee)
    - Compressione header (HPACK)
    - Più efficiente e veloce
    
- **HTTP/3**:
    
    - Usa **UDP** + **QUIC** invece di TCP
    - Migliora la **latenza e affidabilità** su connessioni instabili
    - Multiplexing senza blocchi in caso di perdita pacchetti
    

---