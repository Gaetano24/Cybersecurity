
Il **network core** è la parte centrale e più complessa di una rete di telecomunicazioni, dove i **router** sono **interconnessi** tra loro per gestire e instradare il traffico dati in modo efficiente. Si tratta di una rete **ad alta capacità** che collega tra loro diverse **reti locali** o **reti di accesso**, permettendo la comunicazione tra utenti e sistemi in tutto il mondo.

---
### 🌍 **Funzione del Network Core**

- **Instradamento dei pacchetti**: I pacchetti di dati viaggiano attraverso il core della rete, passando da un **router all'altro**.
    
- **Alta velocità**: I router nel core sono progettati per trasmettere dati molto velocemente, grazie a **alte capacità di banda** e **architetture ottimizzate**.
    
- **Affidabilità e ridondanza**: Il network core è progettato per garantire che, se una parte della rete si guasta, i dati possano essere **reindirizzati** tramite altri percorsi, minimizzando i disservizi.

---

### 🧱 **Router nel Core della Rete**

- **Router**: dispositivi di rete che instradano i pacchetti da una rete all’altra, utilizzando le informazioni contenute nelle intestazioni dei pacchetti (indirizzi IP).
    
- **Interconnessione**: I router nel core sono connessi tramite **link ad alta capacità** (fibra ottica, per esempio), che permettono il trasferimento di enormi quantità di dati.
    
- Questi router **non hanno contatti diretti con gli utenti finali**. La loro funzione è più simile a quella di **"smistatori"** di traffico che assicurano che i dati viaggino lungo i percorsi più efficienti.

---

### 🔁 **Switching (Commutazione)**

- Usato per **inoltrare frame** all'interno di una rete locale (LAN).
    
- Funziona con il **MAC address**.
    
- Il **commutatore (switch)** impara quale MAC si trova su quale porta e inoltra i frame solo lì.
    
- Nessuna analisi del percorso tra reti diverse.

---

### 🧭 **Routing (Instradamento)**

- Usato per **collegare reti diverse** tra loro (es. LAN → Internet).
    
- Funziona con **IP address**.
    
- Il **router** analizza la destinazione IP e decide il **miglior percorso** possibile per raggiungerla.
    
- Usa protocolli di routing (es. OSPF, BGP).

---

## 📦 **Packet Switching (Commutazione a pacchetto)**

Il **packet switching** (commutazione a pacchetto) è una tecnica di trasmissione dati usata su Internet e altre reti moderne.

### Come funziona?

- I dati vengono **spezzati in pacchetti** (chunk di lunghezza fissa o variabile).
    
- Ogni pacchetto viaggia **indipendentemente** verso la destinazione.
    
- Al contrario del **circuit switching** (come le vecchie chiamate telefoniche), **non viene riservato un canale fisso** per tutta la comunicazione.


![[Pasted image 20250415190704.png]]

### 🧳 Store-and-Forward

- I pacchetti **vengono ricevuti per intero** da un router prima di essere inoltrati al prossimo nodo.
- Il router:
    
    1. **Riceve il pacchetto**
    2. Lo **memorizza temporaneamente**
    3. **Lo inoltra** verso il prossimo hop

✅ Garantisce che il pacchetto sia integro prima dell'inoltro.  
⛔ Introduce **latenza** (ritardo), specialmente su collegamenti lenti.


### ⏳ Queuing (Accodamento)

Quando un pacchetto arriva a un router, deve **aspettare in coda** se:

- Il **link di uscita è occupato**
- Ci sono **altri pacchetti in attesa**

I pacchetti vengono **messi in una coda FIFO** (First-In, First-Out).

⛔ I pacchetti potrebbero andare persi se il buffer del router fosse già saturo all'arrivo del pacchetto.

![[Pasted image 20250415191102.png]]

---

## ☎️ **Circuit Switching (Commutazione a circuito)**

La **commutazione a circuito (circuit switching)** è una tecnica di comunicazione in cui viene **stabilito un percorso fisso e dedicato** tra mittente e destinatario **prima** che inizi la trasmissione dei dati.

Durante tutta la durata della comunicazione, **l'intero circuito rimane occupato**, anche se non vengono trasmessi dati in un certo momento.

**Nota**: È usata principalmente nelle **reti telefoniche tradizionali**.

### Come funziona?

1. **Stabilisce il circuito** (connessione iniziale).
2. **Trasmette i dati** (usando tutto il circuito).
3. **Termina la connessione** (quando la comunicazione finisce).


![[Pasted image 20250415191953.png]]

In questa illustrazione viene utilizzata la Frequency Division Multiplexing (FDM) (guarda giù).

✅ **Costante qualità** del servizio.  
⛔ **Spreco di risorse**: se non si parla, il canale resta inutilizzato.

---

## 🔀 **Tecniche di Multiplexing nel Circuit Switching**


### FDM – Frequency Division Multiplexing

- La **larghezza di banda** del canale viene **divisa in frequenze diverse**.
    
- Ogni comunicazione ha una **sua frequenza dedicata**.

🟢 Simile a: più stazioni radio che trasmettono su frequenze diverse.
🔊 Usato per: reti analogiche, radio, TV, telefoni analogici.


### TDM – Time Division Multiplexing

- Tutte le comunicazioni **condividono lo stesso canale**, ma in **tempi diversi**.
    
- Il tempo è diviso in **slot**: ogni utente ha un proprio "turno" per trasmettere.
    

🟢 Simile a: un microfono condiviso tra più persone che parlano uno alla volta.

🖥 Usato per: reti digitali, come il vecchio ISDN, o connessioni T1/E1.


![[Pasted image 20250415192359.png]]

---

## 🌐 **ISP – Internet Service Provider**

Un **ISP** (Internet Service Provider) è un'azienda che **fornisce accesso a Internet** a utenti, aziende o altre reti. Gli ISP gestiscono **infrastrutture di rete** e permettono la **connessione alla rete globale Internet**.

Gli ISP possono essere di **vario livello**, dai più piccoli (locali) a quelli di livello mondiale.


### 🏠 Access ISP (ISP di accesso)

Un **Access ISP** è un tipo di ISP che fornisce la **connessione diretta a Internet** agli utenti finali, come:

- Famiglie
- Uffici
- Piccole aziende

Esempi di connessioni offerte

- DSL
- Fibra ottica
- Cavo (coax)
- Reti mobili (4G/5G)
- Wi-Fi pubblico

✅ **Funzione principale**: collegare **host individuali alla rete ISP** (e quindi a Internet).


### 🏗 Gerarchia tra ISP

Gli Access ISP **non si collegano direttamente tra loro**. Per far passare il traffico da una rete a un’altra, si appoggiano a:

#### 🏢 ISP di livello superiore (Transit ISP o Tier 1, Tier 2)

- Collegano più Access ISP tra loro.
- Forniscono connessioni ad alta velocità e **trasporto su lunga distanza**.
- Possono **interconnettersi tra loro** tramite punti di interscambio (IXP - Internet Exchange Points).


![[Pasted image 20250415194713.png]]

---

### 🌍 **Content Provider Networks (Reti dei fornitori di contenuti)**

Una **Content Provider Network** è una rete costruita da un fornitore di contenuti per **gestire e distribuire i propri dati** e contenuti (video, immagini, file, applicazioni, etc.) agli utenti finali, **riducendo la latenza e aumentando le prestazioni**.

### Caratteristiche

- **Prestazioni elevate**: Grazie a data center distribuiti globalmente, i contenuti possono essere distribuiti con una bassa latenza e alta velocità, migliorando l'esperienza dell'utente.

- **Contenuti Distribuiti Globalmente**: I fornitori di contenuti creano **data center** e **server** sparsi in diverse aree geografiche, per servire i contenuti agli utenti in modo rapido.

- **Reti Private e Proprietarie**: A differenza degli **ISP di accesso** o dei **Transit ISP**, queste reti sono **private** e dedicate esclusivamente alla distribuzione dei contenuti.

- **Utilizzo di Peering**: Molti Content Providers stabiliscono accordi di **peering** con gli ISP, per scambiare traffico direttamente, senza dover passare attraverso Transit ISP, migliorando la **velocità di trasferimento** e riducendo i costi.


![[Pasted image 20250415195421.png]]

![[Pasted image 20250415195531.png]]

---

