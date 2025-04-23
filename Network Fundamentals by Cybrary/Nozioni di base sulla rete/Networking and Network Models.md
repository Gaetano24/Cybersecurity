## **Che cos'è una rete?**

Una **rete** è un insieme di dispositivi interconnessi che comunicano tra loro per condividere dati, risorse e servizi. Questi dispositivi possono includere computer, server, router, switch, smartphone e altri dispositivi intelligenti.

Le reti possono essere classificate in base a diversi criteri, come l'estensione geografica (**LAN, WAN, MAN**), la topologia, il tipo di connessione (**cablate o wireless**) e il modello di comunicazione (**client-server o peer-to-peer**).

![[Pasted image 20250315161007.png]]

---

## **I diversi tipi di rete**

- **LAN (Local Area Network):** una rete locale che copre un'area limitata, come un singolo edificio o un ufficio.
- **WAN (Wide Area Network):** una rete estesa che connette più edifici o sedi, spesso distribuite su un'ampia area geografica, come un'azienda con diverse filiali.
- **MAN (Metropolitan Area Network):** una rete che copre un'area metropolitana, più grande di una LAN ma più piccola di una WAN. Un esempio potrebbe essere la rete di una città o di un'università.
- **WLAN (Wireless Local Area Network):** una rete locale senza fili, come una rete Wi-Fi domestica o aziendale.
- **VPN (Virtual Private Network):** una rete virtuale privata che utilizza la crittografia per garantire comunicazioni sicure, consentendo agli utenti di accedere in modo protetto a una rete aziendale o navigare con maggiore privacy.

---

## **Dispositivi di rete**

- **Hub**: è un dispositivo che trasmette dati a tutti i computer o dispositivi basati su Ethernet ad esso collegati. Ricorda che a differenza di uno **switch**, un hub trasmette a tutti i nodi e non può indirizzare il traffico verso nodi specifici.
- **Switch** (o Switch Ethernet): un dispositivo che collega più nodi sulla stessa rete. Ricorda che è più sofisticato di un hub perché può indirizzare il traffico solo verso determinati nodi invece di trasmettere a tutti i nodi.
- **Router**: un dispositivo che collega e instrada il traffico tra le reti.
- **Endpoint**:  in genere, un dispositivo per l'utente finale come desktop, laptop, stampante, telefono cellulare, ecc.
- **Server**: un computer dedicato alla fornitura di un determinato servizio, come un server di posta o un server di stampa.
- **Firewall**: un dispositivo che filtra il traffico che passa tra le reti allo scopo di proteggere la rete.

![[Pasted image 20250315161527.png]]

---

## **Il Modello OSI**

Il **Modello OSI (Open Systems Interconnection Model)** descrive il meccanismo universale per le comunicazioni di rete. 

L'espressione "**Open Systems**" indica che questo modello può essere applicato a qualsiasi rete, indipendentemente dallo stack tecnologico adottato. 

### **Incapsulamento dei dati**

L'**incapsulamento** è il processo attraverso il quale i dati vengono strutturati e preparati per essere trasmessi attraverso una rete. Durante questo processo, i dati originali vengono racchiusi in pacchetti o segmenti, aggiungendo informazioni di controllo a ciascun livello del modello OSI, come gli indirizzi di destinazione, i codici di errore, o informazioni sulla sequenza. Ogni livello del modello OSI aggiunge il proprio header al pacchetto, creando un pacchetto che contiene sia i dati veri e propri che le informazioni necessarie per il corretto invio e la gestione della comunicazione.

- **Incapsulamento**: processo di aggiunta di informazioni di controllo ai dati originali per consentirne la trasmissione e gestione attraverso la rete.
- **Decapsulazione**: processo inverso, in cui questi strati di informazioni vengono rimossi mentre i dati passano dal livello inferiore a quello superiore, fino a raggiungere la destinazione finale.

### **Stack di livelli**

![[Pasted image 20250315171142.png]]

I **pacchetti** (o segmenti) si spostano da un livello all'altro, dove vengono aggiunti specifici **header** o suffissi (**footer**). Queste informazioni di controllo vengono poi rimosse al momento della destinazione. L'aggiunta di tali informazioni è fondamentale per garantire che i pacchetti non vadano persi e che rimangano correttamente ordinati durante il loro percorso.

### **Funzionamento dei 7 livelli**
 
1. **Livello fisico**: si occupa della trasmissione dei dati attraverso canali di comunicazione fisici, come circuiti e cavi, garantendo il trasferimento dei segnali elettrici o ottici.
2. **Livello data-link**: gestisce il trasferimento dei dati tra i nodi di rete, eseguendo controlli sugli errori e creando i pacchetti che verranno inviati sulla rete. Si occupa anche della sincronizzazione e dell'indirizzamento dei dispositivi.
3. **Livello di rete**: si concentra sull'instradamento dei pacchetti tra diverse reti, determinando il percorso da seguire per il trasferimento dei dati. Gestisce l'indirizzamento, il routing e le operazioni di smistamento per assicurare che i pacchetti raggiungano la loro destinazione correttamente.
4. **Livello di trasporto**: definisce come i dati vengono consegnati ai processi e assicura che vengano ricevuti nell'ordine corretto e senza perdite. I protocolli principali sono TCP/IP e UDP.
5. **Livello di sessione**: gestisce le sessioni di comunicazione tra applicazioni, garantendo che la connessione sia stabilita, mantenuta e terminata correttamente. Si occupa anche di processi come l'autenticazione e l'autorizzazione, che consentono l'accesso sicuro alle risorse.
6. **Livello di presentazione**: si occupa della formattazione, traduzione e crittografia dei dati per garantire che siano nel formato corretto per essere interpretati dai livelli superiori. Inoltre, si occupa di compressione e di altre operazioni legate alla rappresentazione dei dati.
7. **Livello applicazione**: è il livello più vicino all'utente finale e gestisce le interazioni dirette con il software applicativo. Fornisce i servizi necessari per l'esecuzione delle applicazioni come la navigazione web, l'invio di email, la gestione dei file, ecc.

![[Pasted image 20250315172855.png]]

#### **1. Livello fisico**

- **Tipo di indirizzo**: N/A (nessuno)
- **Dispositivi**: cavi, schede di rete, hubs
- **Tipo di dati**: bit

Gli hub trasmettono i dati verso tutte le porte, senza utilizzare indirizzi specifici (ecco perché non si ha alcune informazione sul tipo di indirizzi in questo livello).

---
#### **2. Livello data-link

Questo livello definisce come i dati si muovono tra nodi e usano gli indirizzi MAC, i quali sono gli indirizzi associati a questo specifico livello.

- **Tipo di indirizzo**: Indirizzi MAC
- **Dispositivi**: Switch/Bridge
- **Tipo di dati**: Ethernet Frame

Un **indirizzo MAC** (Media Access Control) è il numero seriale di un nodo composto da 48 bit. I primi 24 bit sono un identificatore per il produttore mentre i restanti 24 bit sono l'identificatore univoco per l'interfaccia di rete (nodo). L'indirizzo MAC deve essere sempre unico a livello globale. 

**Spoofing**: un utente malintenzionato potrebbe falsificare un indirizzo MAC e confondere lo switch che andrà ad inviare i dati, reindirizzando così il traffico. Il dispositivo che rimpiazzerà il dispositivo legittimo riceverà i dati al suo posto.

Il tipo di dato associato a questo livello è l'**Ethernet frame**, composto da diverse sezioni che vengono progressivamente rimosse man mano che i dati attraversano i vari livelli. Ciascuna di queste sezioni contiene informazioni essenziali per identificare i dati e determinarne la destinazione.

![[Pasted image 20250315183107.png]]

---
#### **3. Livello di rete**

Questo livello stabilisce il modo in cui i dati vengono inoltrati sottoforma di pacchetti e determina il percorso che i pacchetti attraverseranno lungo la rete per arrivare a destinazione. 

- **Tipo di indirizzo**: indirizzo IP (es. 192.168.3.1)
- **Dispositivi**: router, firewall
- **Tipo di dati**: pacchetti

##### **Tipologie di indirizzi IP**

Esistono due versioni principali di indirizzi IP:

- **IPv4 (Internet Protocol version 4)**:
    - Formato: 32 bit, rappresentato come quattro numeri decimali separati da punti (es. `192.168.1.1`).
    - Supporta circa 4,3 miliardi di indirizzi.
    - Sta diventando insufficiente a causa dell'aumento dei dispositivi connessi.
- **IPv6 (Internet Protocol version 6)**:
    - Formato: 128 bit, rappresentato in otto gruppi esadecimali separati da due punti (es. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
    - Offre un numero quasi illimitato di indirizzi.

##### **Classificazione degli IP**

Gli indirizzi IP possono essere:
- **Pubblici**: Assegnati da un provider di servizi Internet (ISP) e accessibili da tutta la rete Internet.
- **Privati**: Utilizzati all'interno di reti locali (LAN) e non direttamente accessibili da Internet (es. `192.168.1.1`, `10.0.0.1`).
- **Statici**: Rimangono invariati nel tempo.
- **Dinamici**: Assegnati temporaneamente da un server DHCP e possono cambiare nel tempo.

##### **Ruolo degli indirizzi IP 

L'indirizzo IP permette ai dispositivi di inviare e ricevere dati attraverso la rete. Funziona insieme ad altri protocolli, come il **TCP/IP**, per garantire che i pacchetti di dati raggiungano la destinazione corretta. Per la risoluzione dei nomi, il **DNS (Domain Name System)** traduce i nomi di dominio (es. `www.google.com`) nei corrispondenti indirizzi IP.

##### **Pacchetti**

Come mostrato nella figura sottostante, i pacchetti vengono estratti dall'**Ethernet frame** rimuovendo l'**header** e il **trailer** Ethernet.

![[Pasted image 20250315190359.png]]

Poiché anche  a questo livello vengono utilizzati degli indirizzi, in questo caso **indirizzi IP**, si può parlare di **spoofing**. Un utente malintenzionato potrebbe infatti falsificare un indirizzo IP per reindirizzare il traffico e condurre un **attacco Man-in-the-Middle** o un attacco di **Session Hijacking**

---
#### **4. Livello di trasporto**

Il compito principale di questo livello è garantire una comunicazione affidabile tra i dispositivi in rete, gestendo la segmentazione, il controllo di flusso e il recupero degli errori.

- **Tipo di indirizzo**: porte
- **Dispositivi**: router, firewall
- **Tipo di dati**: segmenti

Questo livello permette a più applicazioni di comunicare simultaneamente sulla stessa rete, distinguendo i processi grazie ai numeri di **porta**.

Il **numero di porta** è un valore numerico che identifica in modo univoco un'applicazione o un servizio in esecuzione su un dispositivo all'interno di una rete.

##### **Protocolli del livello di trasporto**

- **TCP (Transmission Control Protocol)**
    - Affidabile, orientato alla connessione.
    - Garantisce il corretto ordine dei pacchetti e la ritrasmissione in caso di perdita.
    - Utilizzato per applicazioni come email, web browsing, trasferimenti di file (HTTP, FTP, SMTP).
    
- **UDP (User Datagram Protocol)**
    - Non affidabile, senza connessione.
    - Più veloce, ma non garantisce l'ordine o la consegna dei pacchetti.
    - Utilizzato per streaming, VoIP, gaming online (DNS, DHCP, videochiamate).

##### **Segmenti**

I segmenti si ottengono rimuovendo dai pacchetti l'IP Header.

![[Pasted image 20250315194750.png]]

---
#### **5. Livello di sessione**

Il **livello di sessione** si occupa della gestione delle sessioni di comunicazione tra dispositivi. Il suo ruolo principale è quello di stabilire, mantenere e terminare le connessioni tra applicazioni in rete, garantendo che la comunicazione avvenga correttamente e in modo organizzato. Questo livello gestisce sia l'autenticazione che l'autorizzazione.

---
#### **6. Livello di presentazione**

Il **livello di presentazione** si occupa della traduzione, formattazione, criptazione e della compressione dei dati.

---
#### **7. Livello applicazione**

Questo livello riguarda il modo in cui i dati vengono visualizzati nell'interfaccia utente con cui gli esseri umani interagiscono e l'input degli utenti verso l'applicazione.

---

## **Il Modello TCP/IP**

Il **modello TCP/IP** è stato sviluppato dal Dipartimento della Difesa sviluppato negli anni '60 ed è ancora citato oggi. Utilizza 4 livelli per rappresentare alcune delle stesse idee che il Modello OSI rappresenta con 7 livelli. Alcune persone considerano il modello TCP / IP più pratico, mentre il modello OSI è più astratto

![[Pasted image 20250315175937.png]]

### **Inventario e sicurezza**

Un altro motivo per cui il modello OSI e il modello TCP / IP possono essere utili è perché possono aiutarci a fare un inventario di ciò che abbiamo nella nostra rete. Possiamo interrompere la rete e pensarci in termini di ciascun livello. Cosa sta succedendo in ogni livello e cosa abbiamo fissato in ogni livello?

Questi modelli possono essere utilizzati per applicare il principio di difesa in profondità (Defence in Depth) menzionato precedentemente. Possiamo infatti guardare alla nostra rete in modo astratto, strato per strato, e determinare se tutto è sicuro a tutti i livelli.

---
