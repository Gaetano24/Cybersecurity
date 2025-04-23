
## 🌐 **Multimedia**

### 📹 **Video**

Il **video digitale** è una sequenza di immagini statiche (chiamate **frame**) che scorrono rapidamente per creare l’illusione del movimento. 

La frequenza con cui i frame vengono mostrati è chiamata **frame rate**, e può essere ad esempio di 24, 30 o 60 fps (frame per second). 

---

### 🖼️ **Immagine Digitale**

Un’**immagine digitale** è costituita da una griglia di punti chiamati pixel. Ogni pixel contiene informazioni sul colore, spesso rappresentate nei canali RGB (rosso, verde, blu).

- La **risoluzione dell’immagine**, come 1920x1080, indica il numero totale di pixel in larghezza e altezza. 
  
- La **profondità di colore** specifica quanti bit sono usati per rappresentare ogni pixel: più bit, maggiore la fedeltà e il peso dell’immagine. 

Aumentando risoluzione e profondità, crescono anche le dimensioni del file, motivo per cui anche in questo caso si fa largo uso di compressione.

---

### 🔄 **Codifica (uso della ridondanza)**

La **codifica** serve a rappresentare i dati in modo più efficiente, sfruttando diverse forme di ridondanza. 

- **Ridondanza spaziale**: riguarda la somiglianza tra pixel vicini all'interno della stessa immagine: molti algoritmi, come JPEG, comprimono le immagini riducendo l’informazione ripetitiva. 

- **Ridondanza temporale**: nei video si sfrutta il fatto che i frame successivi spesso differiscono solo leggermente: tecnologie come MPEG e H.264 memorizzano infatti solo le differenze tra un frame e l’altro. 

- **Ridondanza statistica**: si verifica quando alcuni valori compaiono con maggiore frequenza, e può essere gestita con algoritmi come la codifica di Huffman. 

![[Pasted image 20250423140941.png]]


La **compressione** può essere:

- **lossless**: senza perdita di dati (come PNG)
- **lossy**: con una perdita controllata di qualità a favore di una riduzione più drastica delle dimensioni (come JPEG o MP4).

---

## 🔢 **Bit Rate**

### 📈 Bit Rate Costante (CBR)

Il **bit rate costante** prevede che la quantità di dati trasmessi per secondo rimanga sempre la stessa, indipendentemente dal contenuto. Questa scelta rende il flusso più prevedibile e facile da gestire, soprattutto nelle trasmissioni in tempo reale o quando la banda disponibile è limitata. Tuttavia, non è efficiente dal punto di vista della qualità: scene semplici ricevono più bit di quanto serva, mentre quelle complesse potrebbero non avere abbastanza dati per essere rappresentate con fedeltà.

---

### 📉 Bit Rate Variabile (VBR)

Il bit rate variabile adatta invece dinamicamente la quantità di dati usati in base alla complessità del contenuto. Scene statiche o poco dettagliate possono essere compresse con pochi bit, mentre quelle più ricche di movimento o particolari ricevono una maggiore quantità di dati per mantenere alta la qualità. Questo metodo è più efficiente e garantisce una qualità media superiore a parità di dimensione del file finale. Tuttavia, può risultare meno adatto in contesti di streaming in tempo reale, poiché richiede una gestione più flessibile della banda e una codifica più complessa.

---

## 📡 **Stored Video Streaming**

Lo streaming di video memorizzato consiste nella **trasmissione in tempo reale di contenuti video pre-registrati**, memorizzati su un server. A differenza del download tradizionale, il video viene riprodotto mentre i dati vengono ricevuti dal client.

![[Pasted image 20250423141510.png]]

---

### 🚧 **Problemi Principali nello Streaming**

#### 📉 Variazione della Banda

La **larghezza di banda disponibile tra server e client non è costante**. Può diminuire o aumentare nel tempo a causa della congestione di rete, della distanza dal server, di interferenze nel segnale (soprattutto su reti wireless), o della competizione con altri utenti. Questo rende difficile garantire uno streaming fluido e continuo.

#### 📦 Perdita di Pacchetti

Nelle reti IP, può succedere che alcuni pacchetti non arrivino a destinazione. Questo fenomeno si chiama **packet loss**. Nel contesto video, può causare artefatti visivi, interruzioni o perdita di sincronizzazione tra audio e video.

---

### ⏯️ **Playout Buffering**

Il **playout buffer** è una memoria temporanea che si trova lato client. Serve per **accumulare un certo numero di secondi di video prima dell'inizio della riproduzione**, in modo da poter compensare eventuali ritardi o fluttuazioni nella trasmissione.

#### ⏳ Start-Up Delay

Quando un video inizia lo streaming, non parte subito. Il lettore aspetta di avere un minimo di contenuto nel buffer (ad esempio 2-5 secondi) prima di iniziare la riproduzione. Questo ritardo iniziale è chiamato **start-up delay**, e serve a garantire che la riproduzione possa continuare anche se la rete rallenta per brevi periodi.

#### 🔄 Funzionamento del Buffer

Durante la riproduzione, il video viene scaricato continuamente e il buffer si riempie in tempo reale. Se la rete rallenta temporaneamente, il lettore continua a usare i dati presenti nel buffer senza interruzioni. Tuttavia, se il problema persiste e il buffer si svuota, il video si blocca: si verifica così il **re-buffering**, ovvero una pausa nella visione per permettere al buffer di riempirsi di nuovo.

#### ⚖️ Equilibrio Qualità-Prestazioni

Il **dimensionamento del buffer** è una scelta di compromesso:

- Un buffer più grande riduce il rischio di interruzioni, ma aumenta il ritardo iniziale.
- Un buffer più piccolo avvia la riproduzione prima, ma è più sensibile ai problemi di rete.


![[Pasted image 20250423141911.png]]

---

## 🌐 **DASH (Dynamic Adaptive Streaming over HTTP)**

### 📱 Cos'è DASH?

DASH è una **tecnologia di streaming adattivo** che permette la trasmissione di contenuti video su **HTTP**, adattando dinamicamente la qualità del video in base alle **condizioni della rete** e alle capacità del dispositivo client. L'obiettivo è migliorare l'esperienza utente durante la visione, riducendo i rallentamenti o le interruzioni causate da variabili come la larghezza di banda disponibile.

DASH è uno **standard aperto**, definito dalla **MPEG (Moving Picture Experts Group)**, che non dipende da un protocollo proprietario. Per questo motivo, è compatibile con diversi dispositivi e piattaforme, come browser, smart TV e dispositivi mobili.

---

### 🖥️ Funzionamento del Server in DASH

Il server ha il compito di **preparare e distribuire i video** per il loro streaming. Questo processo prevede diverse fasi:

#### 🔹**Divisione del Video in Chunk**

Il video originale viene **diviso in piccoli segmenti** (chiamati **chunk**), ognuno dei quali contiene una porzione di video. Ogni chunk di video rappresenta una parte che può essere scaricata e riprodotta singolarmente. Tipicamente, ogni chunk ha una durata che va dai 2 ai 10 secondi, e vengono creati tanti chunk quanti sono necessari per coprire tutta la durata del video.

#### 🔹**Codifica dei Chunk a Differenti Bit Rate**

Per ogni chunk, il server crea **versioni multiple a differenti bit rate e risoluzioni**. Ad esempio:

- Un chunk potrebbe essere codificato a **1080p** e a **5 Mbps**, un altro a **720p** e a **2 Mbps**, e un altro ancora a **480p** e a **1 Mbps**. Questa differenza nei bit rate permette di avere diverse **qualità video** che possono essere utilizzate dal client in base alla larghezza di banda disponibile.

#### 🔹**Memorizzazione in Diversi File**

Le versioni a diversi bit rate vengono **salvate in file separati**, in modo che il client possa scegliere quale file scaricare in base alla sua connessione. Ogni file rappresenta un diverso livello di qualità per lo stesso segmento di video.

#### 🔹**Replica dei File nei CDN**

I file che rappresentano i vari segmenti video vengono **replicati in vari nodi di una rete CDN (Content Delivery Network)**. I nodi CDN sono server distribuiti geograficamente per migliorare la velocità di accesso al contenuto da parte degli utenti. La replica dei file nei CDN riduce i tempi di latenza e assicura che il contenuto sia sempre disponibile vicino all'utente finale, migliorando l'efficienza e l'affidabilità.

#### 🔹**Manifesto del Video (MPD)**

Il **manifesto (MPD - Media Presentation Description)** è un file che descrive la struttura del video e fornisce **gli URL di tutti i segmenti**. Questo file contiene informazioni su:

- I vari bit rate disponibili per ogni chunk.
- La durata dei chunk.
- I link per scaricare i vari chunk da diversi server CDN.

In questo modo, il server fornisce tutte le informazioni necessarie al client per navigare tra i segmenti video e scegliere la qualità migliore in base alle sue esigenze.

---

### 📱 Funzionamento del Client in DASH

Il client è il dispositivo (come un browser, uno smartphone o una smart TV) che riproduce il video e gestisce l'interazione con il server. Il processo di streaming per il client si svolge come segue:

#### 🔹**Stima Periodica della Larghezza di Banda**

Il client monitora costantemente la **larghezza di banda disponibile** tra il server e se stesso. Ogni volta che il client riceve nuovi chunk o dati, stima la velocità di download attuale. Questo processo aiuta a determinare quanto velocemente i dati possono essere ricevuti senza compromettere la qualità del video.

#### 🔹**Consultazione del Manifesto**

Per sapere quali chunk sono disponibili e a quali bit rate, il client consulta il **manifesto (MPD)**, che fornisce una panoramica di tutti i segmenti del video e delle varie opzioni di qualità. In base alle informazioni contenute nel manifesto, il client è in grado di **identificare gli URL** per scaricare i vari chunk e i file video codificati in diversi bit rate.

#### 🔹**Richiesta dei Chunk**

Il client richiede i chunk uno alla volta. Ad esempio, il client scarica il primo chunk, quindi, una volta che è stato ricevuto e riprodotto, richiede il successivo. Ogni richiesta include informazioni sulla **qualità desiderata** per il prossimo chunk, in base alla larghezza di banda disponibile.

#### 🔹**Scelta del Bit Rate Ottimale**

In ogni momento, il client può **scegliere il bit rate più alto** che può essere sostenuto dalla **banda disponibile**. Ad esempio, se la connessione è veloce, il client può scaricare un chunk a 1080p e 5 Mbps. Se la connessione rallenta, il client può passare automaticamente a una qualità inferiore, come 720p o 480p, per evitare il buffering.

#### 🔹**Adattamento Dinamico**

Una delle principali caratteristiche di DASH è che il client può **modificare il bit rate in tempo reale** durante la riproduzione. Man mano che la larghezza di banda cambia (ad esempio, se ci sono fluttuazioni nella connessione di rete), il client può passare a un livello di qualità superiore o inferiore per ottimizzare l’esperienza di visione. Questo processo è continuo, quindi la qualità del video è sempre adattata in tempo reale alle condizioni della rete.

#### 🔹**Selezione di Server Diversi**

DASH permette anche di selezionare server diversi da cui scaricare i segmenti. Se il client rileva che un server è troppo lento o congestionato, può passare a un altro server replicato nella rete CDN per migliorare le prestazioni e ridurre la latenza.

---

## 🌍 **Content Distribution Networks (CDNs)**

### 🧩 Cos'è una CDN?

Una **Content Distribution Network** (o Content Delivery Network) è un **insieme di server distribuiti geograficamente** che collaborano per **distribuire contenuti (video, immagini, pagine web, ecc.) in modo rapido, efficiente e affidabile** agli utenti finali.  
L’obiettivo è **ridurre la latenza**, **evitare congestioni** e **migliorare la disponibilità** del contenuto, specialmente in caso di traffico elevato.

---

### 🏗️ Architettura e Funzionamento

#### 📍 **Distribuzione Geografica dei Nodi**

I **nodi CDN** (chiamati anche **edge servers**) sono sparsi in tutto il mondo e **replicano copie del contenuto** originale che risiede su un **server centrale (origin server)**.  
Quando un utente richiede un contenuto, la richiesta viene **reindirizzata al nodo più vicino** in termini di latenza (non necessariamente il più vicino fisicamente).

#### 🔄 **Caching dei Contenuti**

Le CDN utilizzano una tecnica chiamata **caching**, cioè **memorizzano temporaneamente i contenuti** statici richiesti frequentemente (es. immagini, video, fogli di stile, script). Questo riduce il carico sui server principali e velocizza la consegna.

---

### ⚙️ Funzionamento nel Dettaglio

1. **L'utente richiede un contenuto** (es. un video o una pagina web).
    
2. La richiesta viene indirizzata a un **edge server** vicino
    
3. Se il contenuto è già nella cache dell’edge server (cache hit), viene servito immediatamente.
    
4. Se non è presente (cache miss), il contenuto viene richiesto al server originario, poi memorizzato nel nodo CDN per future richieste.


![[Pasted image 20250423144338.png]]


> [!NOTE] OTT (Over the top)
> 
> "Over The Top" letteralmente significa **"sopra"** o **"al di sopra"**. In pratica:
> 
> 👉 **Un servizio OTT** _si appoggia a una rete esistente (come Internet), ma non è gestito da chi fornisce quella rete_.
> 
> **Esempio**: 
> Se guardi Netflix, stai usando un servizio OTT: Netflix ti dà contenuti **attraverso Internet**, ma non è fornito da TIM o Vodafone, anche se usi la loro rete.


![[Pasted image 20250423145003.png]]

---

### 📡 Enter deep (Entrare in profondità)

**"Enter deep"** è un approccio utilizzato dalle **reti di distribuzione dei contenuti (CDN)** per migliorare la velocità e l'efficienza della consegna dei contenuti, come i video.

Letteralmente, "entrare in profondità" significa **collocare i server della CDN molto vicini agli utenti finali**, all'interno delle **reti di accesso** (come quelle dei provider Internet locali). Invece di avere pochi server centrali in posizioni strategiche, con l'approccio "enter deep", i server vengono distribuiti **più capillarmente** in tanti punti della rete.

---