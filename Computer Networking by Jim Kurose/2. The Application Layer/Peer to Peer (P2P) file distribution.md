## 📡 **Peer-to-Peer (P2P)**

Il modello **Peer-to-Peer (P2P)** è un’architettura di rete in cui **ogni nodo** della rete (**peer**) ha **uguale importanza** e può agire **sia da client che da server**. Invece di richiedere risorse da un server centrale, i peer condividono direttamente tra loro file, larghezza di banda, potenza di calcolo, ecc.


### Caratteristiche fondamentali:

- **Decentralizzazione**: assenza di un nodo centrale.
    
- **Distribuzione del carico**: ogni peer contribuisce con le proprie risorse.
    
- **Resilienza**: il fallimento di un nodo non compromette il sistema.
    
- **Autonomia**: i peer possono entrare/uscire liberamente dalla rete.
    
- **Collaborazione**: i peer sono incentivati a condividere contenuti e risorse.


### Pro e Contro:

|Pro|Contro|
|---|---|
|Riduce il carico sul server centrale|Minore controllo e sicurezza|
|Alta scalabilità|Rischi legali (es. violazione del copyright)|
|Fault tolerance elevato|Ricerca risorse più complessa|
|Efficienza nella distribuzione file grandi|Difficoltà di autenticazione e verifica|

![[Pasted image 20250424134808.png]]

---

## 🧱 **Architetture P2P**

Le architetture P2P possono essere **non strutturate** o **strutturate**, a seconda di come sono organizzate le connessioni tra i nodi e il metodo di ricerca dei contenuti.

---
###  **Architetture P2P Non Strutturate**

#### 🛠 Descrizione:

- I peer si connettono in modo casuale e formano una rete ad-hoc.
- Nessuna struttura logica per la posizione dei file.

#### 🔍 Ricerca:

- Si usa il **flooding**: una richiesta viene propagata a tutti i peer vicini.
- Non garantisce che una risorsa venga trovata anche se esiste.

#### ✅ Vantaggi:

- Semplicità di implementazione.
- Maggiore tolleranza ai guasti.

#### ❌ Svantaggi:

- Ricerca inefficiente.
- Elevato traffico in rete.
- Scalabilità limitata.

#### 🔧 Esempi:

- Gnutella
- Kazaa
- Freenet

---

### **Architetture P2P Strutturate**

#### 🛠 Descrizione:

- I peer sono organizzati secondo una struttura logica predefinita.
- Usano algoritmi come le **DHT (Distributed Hash Table)** per mappare chiavi a nodi.

#### 🔍 Ricerca:

- Ogni nodo conosce altri nodi specifici secondo regole precise.
- Le operazioni di lookup sono efficienti: **O(log N)** o meglio.

#### ✅ Vantaggi:

- Alta efficienza nella ricerca.
- Scalabilità a milioni di nodi.

#### ❌ Svantaggi:

- Più complessa da implementare.
- Più sensibile a cambiamenti dinamici nella rete (churn).

#### 🔧 Esempi:

- Chord
- Pastry
- Kademlia (usato da BitTorrent, eMule)

---

### **Distributed Hash Table (DHT)**

- Struttura dati distribuita che mappa **chiavi** (es. hash dei file) a **valori** (es. indirizzi IP dei peer che hanno il file).
    
- Ogni nodo è responsabile di un certo intervallo di chiavi.
    
- Quando un peer cerca un file, la DHT lo guida verso il nodo giusto.


---

## 📥 **BitTorrent**

### 🧾 Cos’è BitTorrent?

BitTorrent è un **protocollo P2P** progettato per facilitare il trasferimento efficiente di file molto grandi, suddividendoli in piccoli pezzi scaricati da più peer contemporaneamente. È tra i protocolli P2P più usati al mondo.

### 🛠 Funzionamento generale:

1. L’utente scarica un file **.torrent** contenente:
    
    - Metadati sul file (dimensioni, nomi, hash dei pezzi)
    - URL del **tracker**
    
2. Il client BitTorrent contatta il **tracker**, che restituisce una lista di peer.
    
3. Il file è diviso in **pezzi** (chunks).
    
4. Il client inizia a **scaricare i pezzi** da più peer contemporaneamente.
    
5. Appena un pezzo è scaricato, il client lo **condivide** con altri peer.


### 🧩 Componenti principali:

|Componente|Descrizione|
|---|---|
|**Seeder**|Peer che possiede il file completo|
|**Leecher**|Peer che sta ancora scaricando il file|
|**Tracker**|Server centrale che coordina peer, ma non distribuisce dati|
|**Swarm**|L’insieme di tutti i peer (seeder + leecher) che partecipano allo stesso file|

### ✅ Vantaggi di BitTorrent:

- **Altamente scalabile**: più peer = maggiore capacità.
- **Efficienza di banda**: ogni peer contribuisce.
- **Ridotto carico sui server centrali**: i dati sono distribuiti tra i peer.
- **Distribuzione rapida di file grandi** (es. video, ISO Linux, giochi).

### ❌ Svantaggi:

- **Dipendenza iniziale da seeder**: senza almeno un seeder, il file può diventare irrecuperabile.
- **Tracker down** = swarm difficilmente raggiungibile (risolto parzialmente dalle DHT).
- **Problemi legali**: spesso usato per condividere contenuti pirata.


![[Pasted image 20250424134726.png]]

---

