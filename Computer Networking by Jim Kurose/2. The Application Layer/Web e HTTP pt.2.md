
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

### **HTTP/1.0**

- **Zero multiplexing**: una singola richiesta per connessione.
- Il client apre una connessione TCP, invia la richiesta, aspetta la risposta, chiude.
- Nessuna possibilità di parallellismo.

 Conseguenze:

- Altissima latenza per siti con molte risorse.
- Overhead di apertura/chiusura TCP per ogni risorsa.

---

### **HTTP/1.1**

- **Connessioni persistenti** (`Connection: keep-alive`) → una connessione può servire più richieste.
- **Pipelining**: permette di inviare più richieste **in sequenza**, **senza aspettare la risposta**.


Problemi:

- **Head-of-line blocking**: se una risposta è lenta, blocca tutte le successive.
- Molti server e proxy intermedi **non gestivano bene** il pipelining.    
- Per simulare il parallelismo, i browser aprivano **più connessioni TCP (di solito 6)** per dominio → spreco di risorse.

---

### **HTTP/2**

- **Multiplexing reale**: una sola connessione TCP per tutte le richieste.    
- Le richieste e risposte sono suddivise in **frame binari**, ciascuno con un **Stream ID**.
- I frame di stream diversi possono essere **intercalati** nel flusso di byte TCP.


**Gestione avanzata**:

- **Priorità tra stream**: ogni stream può indicare priorità o dipendenze.    
- Compressione header (HPACK) → meno overhead.


**Limite tecnico:**

- Tutto viaggia su **un’unica connessione TCP**.    
- Se un pacchetto viene perso, **TCP blocca tutto finché non viene ritrasmesso**.
- → **Head-of-line blocking a livello trasporto**, anche se HTTP è multiplexato.


![[Pasted image 20250420155646.png]]

---

### **HTTP/3**

- Multiplexing **a livello nativo del trasporto**, grazie a **QUIC**.
- Ogni richiesta HTTP viaggia su un **flusso indipendente** all’interno della stessa connessione QUIC.


![[Pasted image 20250508012528.png]]

---
