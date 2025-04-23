### 🖥️ **Host: Client e Server**

Gli **host** (o **end system**) sono dispositivi ai margini della rete, **collegati direttamente alla rete**. Si dividono principalmente in:

- **Client**: dispositivi che **richiedono servizi** (es. computer, smartphone, tablet).
- **Server**: dispositivi che **forniscono servizi** (es. siti web, servizi cloud, email).

---

### 📡 **Reti di Accesso**

Le **reti di accesso** collegano l’host alla prima parte dell’Internet. Cambiano in base al tipo di utente:

- **Accesso residenziale** (es. ADSL, fibra, Wi-Fi domestico).
    
- **Accesso aziendale** (es. reti Ethernet, VPN).
    
- **Accesso mobile** (es. rete 4G/5G, hotspot).

![[Pasted image 20250415170659.png]]

---

### 🔌 **Mezzi di Comunicazione (Communication Links)**

I dati viaggiano tra i dispositivi attraverso **collegamenti fisici o wireless**, detti **media di trasmissione**:

#### 📶 Wireless

- Utilizza onde radio.
- Esempi: **Wi-Fi, LTE, 5G, Bluetooth**.

#### 🔗 Wired (via cavo)

- Trasmette dati tramite cavi fisici.

- Tipi principali:
    
    - **Rame (coppia ritorta)**: usato per ADSL e telefonia.
    - **Cavo coassiale**: usato in alcune connessioni TV e Internet.
    - **Fibra ottica**: velocissima, trasmette con impulsi luminosi.

---

### **🔌 Cable-Based Access (Accesso via Cavo)**

- Utilizza la **rete via cavo coassiale** (la stessa usata per la TV via cavo).
    
- Molto comune in ambito residenziale, soprattutto nelle aree urbane.
    
- I dati viaggiano **insieme ai segnali TV** ma su canali separati.
    
- Offre velocità elevate grazie alla **larghezza di banda condivisa**.
    
- È tipicamente gestita tramite un **modem via cavo**, connesso al provider Internet (ISP).


![[Pasted image 20250415171423.png]]

📌 **Nota**: trattandosi di una rete condivisa tra più utenti (es. in un quartiere), la velocità può variare in base al numero di persone collegate contemporaneamente.

---

### ☎️ **Digital Subscriber Line (DSL)**

- Utilizza i **tradizionali cavi in rame della linea telefonica**.
    
- Permette di **navigare su Internet e usare il telefono** contemporaneamente, separando le frequenze di voce e dati.
    
- Ogni utente ha un collegamento **dedicato** con la centrale telefonica.
    
- La velocità dipende dalla **distanza dalla centrale DSL**:
    
    - Più si è lontani, **più la connessione è lenta e instabile**.
    

📌 Tipi di DSL:

- **ADSL (Asymmetric DSL)**: velocità di download maggiore rispetto all’upload.
- **VDSL (Very-high-bit-rate DSL)**: versione più veloce, ma con distanza ancora più limitata.


![[Pasted image 20250415171928.png]]

La connessione DSL sfrutta il cavo telefonico tradizionale in rame (quello già presente in casa) per collegarsi alla centrale telefonica del fornitore Internet, dove si trova un dispositivo chiamato **DSLAM (Digital Subscriber Line Access Multiplexer)**. 

Il DSLAM è l’apparato che raccoglie le connessioni DSL degli utenti e le collega a Internet. 

- I **dati Internet** (navigazione, video, email, ecc.) viaggiano lungo il cavo telefonico e arrivano al DSLAM, da lì vengono instradati verso Internet. 

- I **segnali vocali** (le chiamate telefoniche) invece usano una parte separata delle frequenze del cavo. Questi segnali vengono dirottati verso la rete telefonica tradizionale (PSTN – Public Switched Telephone Network) e non passano per Internet.

---

### 🏠 **Home Networks**

![[Pasted image 20250415172446.png]]

#### Componenti principali di una rete domestica

##### 1. **Modem**

- Dispositivo che **collega la rete di casa a Internet** (via cavo, fibra o DSL).
- Traduce il segnale del provider in dati utilizzabili dalla rete domestica.

##### 2. **Router**

- Smista il traffico dati tra i dispositivi della casa e Internet.
- Spesso è integrato nel modem in un unico apparecchio.
- Crea la **rete Wi-Fi** e assegna **indirizzi IP locali**.

##### 3. **Access Point (AP)**

- Espande la copertura Wi-Fi in zone più lontane.
- Utile in case grandi o con muri spessi.

##### 4. **Switch (opzionale)**

- Usato per collegare via cavo più dispositivi alla rete (es. TV, PC, console).
- Serve in caso di molte connessioni cablate.

##### 5. **Dispositivi Client**

- Tutti i dispositivi che si collegano alla rete: smartphone, PC, smart TV, tablet, ecc...

---

### 📡 **Wireless Access Network**

Una **rete di accesso wireless** permette ai dispositivi di connettersi a Internet **senza l’uso di cavi**, usando segnali radio. È il tipo di rete più comune per dispositivi mobili e portatili.

#### 📶 WLANs – Wireless Local Area Networks

- Sta per **Wireless Local Area Network** (rete locale senza fili).
    
- Utilizza la tecnologia **Wi-Fi** per collegare dispositivi in un’area ristretta, come:
    
    - Case, scuole, uffici, bar, aeroporti.
    
- Il router wireless (o **access point**) trasmette il segnale Wi-Fi ai dispositivi vicini.
    
- Copertura tipica: **decine di metri**.
    
- Standard più usati: **IEEE 802.11 (a/b/g/n/ac/ax)**.


![[Pasted image 20250415173501.png]]



#### 📱 Wide Area Cellular Access Network

- È la rete **cellulare** usata da smartphone, tablet e modem 4G/5G per accedere a Internet **ovunque ci sia copertura**.
    
- La comunicazione avviene tramite **torri cellulari** (stazioni radio base) che coprono aree chiamate **celle**.
    
- Tipi di rete cellulare:
    
    - **3G**: velocità base.
    - **4G (LTE)**: buona velocità per streaming e download.
    - **5G**: altissima velocità e bassissima latenza.


![[Pasted image 20250415173603.png]]

---

### 🏢 **Enterprise Networks (Reti Aziendali)**

- Copre più edifici o sedi (rete **privata** su più livelli).
    
- Alta **sicurezza**, **affidabilità** e **prestazioni**.
    
- Include accesso a:
    
    - File server
    - Stampanti di rete
    - Applicazioni aziendali
    - Internet e posta elettronica

![[Pasted image 20250415174252.png]]

---

### 🏬 **Data Center Networks (Reti dei Data Center)**

Un data center è una struttura che ospita server, storage, apparati di rete e sistemi per gestire grandi quantità di dati e servizi digitali.  
La data center network è l’insieme delle connessioni che permette a tutti questi dispositivi di comunicare tra loro e con l’esterno (es. Internet, aziende, utenti).

![[Pasted image 20250415174459.png]]

---

### 🧾 **Host: invio di pacchetti di dati**

Quando un **host (client o server)** invia un messaggio su Internet, segue alcuni passaggi fondamentali per prepararlo alla trasmissione.

![[Pasted image 20250415174812.png]]

#### 📦 1. Presa del messaggio applicativo

Quando **un'applicazione** sul tuo dispositivo vuole inviare dati (per esempio, quando mandi un’email, apri un sito web, o invii un file), essa **genera un messaggio**. Questo messaggio non può essere trasmesso subito "così com'è" su Internet. Deve prima essere **preparato dalla rete del dispositivo** (cioè dallo **stack protocollare** del sistema operativo).

#### ✂️ 2. Suddivisione in pacchetti

Il messaggio viene **suddiviso in porzioni più piccole** chiamate **pacchetti**. Ogni pacchetto ha una **lunghezza fissa o variabile**, ad esempio **L bit**.Questo processo serve a:
    
- Gestire meglio l’invio di dati su reti complesse.
- Rendersi compatibile con i protocolli di trasporto (es. TCP, UDP).

#### 🚀 3. Trasmissione del pacchetto nella rete di accesso

Ogni pacchetto viene **trasmesso** nella **rete di accesso** (es. Wi-Fi, Ethernet, rete mobile).

#### ⚙️ 4. Transmission Rate (R)

- Il **tasso di trasmissione (R)** indica **quanti bit al secondo** vengono inviati.
- Si misura in **bit/sec (bps)**.
- Sinonimi:
    
    - **Link transmission rate**
    - **Link capacity**
    - **Link bandwidth**


📌 Esempio: se R = 100 Mbps e il pacchetto è lungo L = 1.000.000 bit, ci vorranno **L / R = 0,01 secondi** per trasmetterlo su quel link.

![[Pasted image 20250415175424.png]]

---

## 🔗 **Links: Physical Media (Mezzi fisici di trasmissione)**

Nella rete, un **link** è il collegamento fisico o logico tra due dispositivi. Serve per **trasmettere i bit**, cioè le unità base di informazione (0 e 1).

#### 🧱 Bit

Il **bit** è la più piccola unità di informazione digitale. Viene **trasmesso attraverso un link** sotto forma di:
    
- Impulsi elettrici (rame)
- Impulsi luminosi (fibra)
- Onde radio (wireless)


#### 🔌 Physical Link

È il **mezzo fisico reale** che connette due nodi di rete (es. PC ↔ router).

- **Guided Media (Mezzi guidati)**:

	- Il segnale è **confinato** dentro un supporto fisico (cavi).
	- Esempi:
	    - Twisted Pair (coppia ritorta)
	    - Coaxial Cable (cavo coassiale)
	    - Fiber Optic Cable (fibra ottica)


- **Unguided Media (Mezzi non guidati)**:

	- Il segnale **viaggia nell’aria**, senza supporto fisico.
	- Esempio: trasmissione **wireless via onde radio**.

---
