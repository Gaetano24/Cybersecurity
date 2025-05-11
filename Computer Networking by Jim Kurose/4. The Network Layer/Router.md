## **Architettura dei router**

Un **router** è un dispositivo di rete che instrada pacchetti tra reti differenti, basandosi sulle informazioni contenute nell'intestazione del pacchetto e nella sua tabella di instradamento. La sua architettura è composta da quattro componenti principali:

![[Pasted image 20250510153829.png]]

---

## **Input Ports (Porte di Ingresso)**

Le **porte di ingresso** hanno il compito di ricevere i pacchetti dalla rete e prepararli per l’inoltro all’interno del router. Sono composte da più moduli funzionali, ciascuno responsabile di una fase dell'elaborazione del pacchetto.

### **Componenti principali:**

1. **Physical Layer (Livello Fisico)**
    
    - Gestisce la **ricezione del segnale fisico** (es. elettrico, ottico).
    - Conversione del segnale in una rappresentazione digitale.
    - Interfaccia con cavi Ethernet, fibra ottica, ecc.
    
2. **Link Layer (Livello Collegamento Dati)**
    
    - Decapsula il **frame di livello 2** (es. Ethernet).
    - Verifica l’integrità tramite il **CRC**.
    - Estrae il **pacchetto IP** dal frame ricevuto.
    
3. **Decentralized Switching (Commutazione Decentralizzata)**
    
    - L’**elaborazione dell’intestazione IP** e la **decisione di forwarding** possono avvenire direttamente nell'input port.
    - Utilizza una **copia locale della tabella di routing/forwarding** (detta anche FIB – Forwarding Information Base).
    - Riduce il carico sul routing processor e aumenta la velocità di inoltro.


![[Pasted image 20250510154530.png]]

---

## **Destination-Based Forwarding (Instradamento basato sulla destinazione)**

Questa tecnica determina **la porta di uscita** in base all’indirizzo IP **di destinazione** del pacchetto. È il metodo usato nei router IP per inoltrare i pacchetti.

### **IP Interval Ranges (Intervalli IP)**

- La **tabella di routing** contiene **intervalli di indirizzi IP**, tipicamente rappresentati in notazione CIDR (es. `192.168.1.0/24`).
    
- Ogni intervallo è associato a una **porta di uscita** (o interfaccia) e, talvolta, a un **next hop**.
    
- Questi intervalli definiscono **subnet** o **blocchi di indirizzi** che il router è in grado di raggiungere.


Esempio:

```
Destinazione         Next Hop
10.0.0.0/8           Porta 1
192.168.1.0/24       Porta 2
0.0.0.0/0            Porta 3  (default route)
```


> [!NOTE] **Osservazione**
> 
> Cosa succederebbe se all'interno di uno range di indirizzi bisognasse specificare un sottoinsieme di indirizzi con un Next Hop diverso? 
> 	
> Una soluzione (non efficiente) potrebbe essere quella di dividere il range di indirizzi in più parti. 

![[Pasted image 20250510155951.png]]


### **Longest Prefix Matching (Corrispondenza al prefisso più lungo)**

- Quando un pacchetto arriva, il router cerca **tutti i prefissi** nella tabella che **corrispondono** all’indirizzo di destinazione.
    
- **Regola del prefisso più lungo:** tra le corrispondenze, il router sceglie quella con il **numero maggiore di bit coincidenti** all’inizio (cioè il prefisso più specifico).


Esempio:

- IP di destinazione del pacchetto: `192.168.1.45`
    
- La tabella ha:
    
    - `192.168.0.0/16` → match
    - `192.168.1.0/24` → match più lungo
    - `0.0.0.0/0` → default route (match universale)

 Il router seleziona `192.168.1.0/24` perché è il **match più specifico**.


![[Pasted image 20250510155551.png]]

Il **Longest Prefix Matching (LPM)** viene spesso **accelerato in hardware** tramite l'uso di **TCAMs (Ternary Content-Addressable Memories)**.

#### Che cos'è una TCAM?

- Una **TCAM (Ternary Content Addressable Memory)** è un tipo speciale di memoria che permette **ricerche parallele** di chiavi rispetto a tutte le voci memorizzate.
    
- Il "ternary" si riferisce alla capacità di ogni bit di assumere tre valori: `0`, `1`, o **“don’t care” (`*`)**, permettendo **mascheramento dei bit** nei confronti di rete.

---

## **Switching Fabrics**

La **switching fabric** è il **cuore del router**: è il meccanismo che trasferisce i pacchetti dalle **porte di ingresso** a quelle di **uscita**, cioè spostare i pacchetti dalla porta di ingresso alla porta di uscita calcolata con il **longest prefix matching**. 

### **Switching rate**

Il **switching rate** indica la **velocità alla quale la switching fabric può trasferire dati** dalle input ports alle output ports. È solitamente espresso in **Gbps** o **packets per second (pps)**.

Formula:
$$
Switching Rate≥N×R
$$

- **N** = numero di porte (input/output)
- **R** = velocità di ciascuna porta


### **Tipologie principali**

#### 1. Memory-Based Switching

- **Struttura:** Tutti i pacchetti passano attraverso **la memoria centrale** (RAM condivisa).
- La **CPU** copia i pacchetti dalla porta di ingresso in memoria, poi li legge e li scrive sulla porta di uscita.

✅ Vantaggi:

- Architettura semplice.
- Facile da gestire.

❌ Svantaggi:

- **Non scalabile:** una sola operazione per volta.
- **Lenta** per router con molte porte o traffico elevato.

> 💡 Usata solo nei **router di fascia bassa** o storici.

![[Pasted image 20250510161856.png]]


#### 2. Bus-Based Switching

- **Struttura:** Tutti i moduli di input/output condividono un **bus interno comune**.
- I pacchetti sono posti sul bus e inviati alla porta di uscita.

✅ Vantaggi:

- Relativamente semplice da implementare.
- Supporta più operazioni rispetto al modello con memoria.

❌ Svantaggi:

- **Collo di bottiglia:** un solo pacchetto alla volta può attraversare il bus.
- Problemi di **scalabilità** con molte porte ad alta velocità.

> 💡 Adatto a router di **fascia media**.

![[Pasted image 20250510162006.png]]


#### 3. Interconnection Network

- **Struttura avanzata**, simile a quelle usate nei supercomputer.
- Utilizza una rete di switch interni (es. **crossbar** o **reti multistadio come Clos**).
- Permette a **più input e output di comunicare contemporaneamente**.

✅ Vantaggi:

- **Altamente scalabile.**
- Supporta **commutazione parallela**.
- Essenziale per router ad **altissime prestazioni**.

❌ Svantaggi:

- Maggiore **complessità hardware e controllo**.
- Costo superiore.

> 💡 Usata nei **core router** e data center.

![[Pasted image 20250510162152.png]]

---

## **Input Port Queuing**

Quando i pacchetti arrivano più velocemente di quanto la **switching fabric** possa smistarli, devono essere **temporaneamente memorizzati** nei **buffer delle porte di ingresso**.

### **Funzionamento**

- Ogni porta di ingresso ha una **coda (queue)** per i pacchetti in arrivo.
- I pacchetti vengono accodati **in ordine di arrivo (FIFO)**.
- Se la switching fabric è occupata o lenta, i pacchetti restano in attesa.

### **Head-of-Line (HOL) Blocking**

Si verifica quando il **pacchetto in testa alla coda** (quello più vecchio) **non può essere inoltrato** perché la porta di uscita è occupata o la switching fabric è congestionata.

Anche se i **pacchetti successivi** nella coda potrebbero essere indirizzati verso **porte diverse e disponibili**, **non possono avanzare** perché sono **bloccati dal primo**.

Esempio:

1. Pacchetto A (in testa alla coda) vuole uscire dalla porta 1 → porta occupata.
2. Pacchetto B (dietro A) vuole uscire dalla porta 2 → porta libera.
3. Pacchetto B **non può essere inoltrato** finché A non viene servito.

![[Pasted image 20250510164916.png]]

---

## **Output Port Queuing**

Quando i pacchetti raggiungono la **porta di uscita**, potrebbero non essere immediatamente trasmessi sul collegamento successivo, specialmente se:

- Arrivano **più pacchetti di quanti il link possa trasmettere** in un dato istante.
- Il traffico è **burst traffic** (molto traffico in poco tempo).

In questo caso, i pacchetti vengono **accodati** in un buffer di uscita.

![[Pasted image 20250510165012.png]]

### **Funzionamento**

- Ogni **porta di uscita** ha una **coda** (o più code) in cui si accodano i pacchetti in attesa di trasmissione.
- Se la **capacità del link** è inferiore al traffico in arrivo, la coda cresce.
- Se la coda si riempie → **packet loss** (pacchetti scartati).


### **Scheduling (Schedulazione delle code)**

Quando ci sono più pacchetti in coda, il router deve decidere **in che ordine** inviarli.

**Principali algoritmi di scheduling**:

- **FIFO (First-In First-Out):** ordine di arrivo, semplice ma non prioritario.
    
- **Priority Queuing:** classi di traffico con livelli di priorità (es. VoIP prima del file transfer).
    
- **Round Robin / Weighted Fair Queuing (WFQ):** ripartisce equamente la banda o assegna **quote di banda** a flussi diversi (QoS).


### **Strategie di gestione del Buffer**

#### Drop Tail

- Il pacchetto viene scartato solo quando il buffer è pieno.

- ✅ Semplice
- ❌ Non previene la congestione, causa burst di perdite.

> [!NOTE] 
> I pacchetti da scartare potrebbero anche essere scelti in base a delle priorià

#### Random Early Detection (RED)

- Inizia a **scartare pacchetti casualmente** quando il buffer **inizia a riempirsi**.

- ❗ Funziona bene con TCP: i pacchetti persi attivano la riduzione della finestra di congestione.
- ✅ Riduce burst di packet loss.
- ❌ Più complesso da configurare.

#### Explicit Congestion Notification (ECN)

- Invece di scartare, il router **marca i pacchetti** per segnalare congestione ai dispositivi finali.

- ✅ Meno perdite, TCP reagisce comunque.
- ❗ Richiede supporto da parte degli endpoint.

---



