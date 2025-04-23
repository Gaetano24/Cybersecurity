## **Strumenti utilizzati per proteggere le reti**

### **IDS (Intrusion Detection System)**  

Un IDS è un sistema che monitora il traffico di rete e/o i sistemi host alla ricerca di attività sospette o comportamenti anomali. Non interviene attivamente per bloccare gli attacchi, ma segnala le potenziali minacce agli amministratori di sicurezza per una successiva analisi. Le due varianti sono NIDS (Network IDS) e HIDS (Host IDS).

---
### **IPS (Intrusion Prevention System)**  

L'IPS è simile all’IDS per quanto riguarda il monitoraggio, ma agisce in maniera proattiva. Quando rileva un'attività anomala o un attacco, può intervenire automaticamente per bloccare il traffico malevolo o isolare il sistema interessato, contribuendo così a prevenire incidenti. Le varianti sono NIPS (Network IPS) e HIPS (Host IPS).

---
### **SIEM (Security Information and Event Management)**  

Il SIEM raccoglie, aggrega e analizza i log e gli eventi provenienti da diverse fonti (firewall, IDS/IPS, server, applicazioni, ecc.). Questo sistema consente una visione centralizzata della sicurezza, facilitando il rilevamento di minacce, la correlazione degli eventi e la risposta agli incidenti in tempo reale.

---
### **EDR (Endpoint Detection and Response)**  

L’EDR è focalizzato sugli endpoint (computer, laptop, dispositivi mobili, ecc.). Monitora in modo continuo le attività sui dispositivi finali, rilevando comportamenti sospetti, analizzando anomalie e, in alcuni casi, automatizzando la risposta agli attacchi. È particolarmente utile per rilevare minacce avanzate che possono bypassare soluzioni di sicurezza tradizionali.

---
### **SOAR (Security Orchestration, Automation and Response)**  

Il SOAR integra strumenti di sicurezza diversi, automatizzando e orchestrando le risposte agli incidenti. Grazie all’automazione, permette agli analisti di ridurre il tempo di reazione, eseguire playbook predefiniti e coordinare le azioni tra vari sistemi di sicurezza, migliorando così l’efficacia delle difese.

---
### **Honeypot**  

Un honeypot è una risorsa (o sistema) volutamente vulnerabile e isolata, progettata per attirare gli attaccanti. Il suo scopo è duplice: distrarre gli aggressori dai sistemi reali e raccogliere informazioni utili sul loro modus operandi, contribuendo così ad affinare le strategie di difesa.

---

### **Riepilogo**:

In sintesi, questi strumenti rappresentano componenti fondamentali di una strategia di cybersecurity moderna. Mentre l’IDS e l’IPS si occupano di monitoraggio e prevenzione del traffico malevolo, il SIEM aggrega e analizza gli eventi per una visione completa della sicurezza. L’EDR si concentra sugli endpoint, il SOAR automatizza e orchestra la risposta agli incidenti e il honeypot serve a studiare e mitigare le minacce attive. Integrando questi strumenti, le organizzazioni possono ottenere una difesa a più livelli, in grado di rilevare, prevenire e rispondere efficacemente a una vasta gamma di minacce.

---

## **Come si costruisce una rete sicura?**

### **Defense in Depth**

**Defense in Depth (Difesa in profondità)**: è un approccio multilivello alla sicurezza, basato sull'idea che nessuna singola misura di sicurezza sia sufficiente da sola. Si basa su diversi livelli di protezione, che includono:

- **Perimetro della rete**: Firewall, IDS/IPS per monitorare e filtrare il traffico in entrata e in uscita.
- **Protezione degli endpoint**: Antivirus, EDR (Endpoint Detection and Response) per difendere i dispositivi dai malware.
- **Controllo degli accessi**: Autenticazione a più fattori (MFA), gestione degli accessi privilegiati (PAM).
- **Cifratura dei dati**: Protezione dei dati sensibili tramite crittografia sia in transito che a riposo.
- **Monitoraggio e rilevamento delle minacce**: SIEM per la raccolta e analisi dei log, strumenti di threat intelligence.
- **Backup e disaster recovery**: Soluzioni di backup e piani di continuità operativa in caso di attacco o guasto.

L’idea è che anche se un livello di sicurezza viene compromesso, ce ne siano altri a proteggere il sistema.

### **Zero Trust**

**Zero Trust (Fiducia Zero)**: questo concetto si basa sul principio fondamentale di **non fidarsi di nessuno a priori**, richiedendo che **tutti gli utenti, dispositivi e applicazioni si autentichino e vengano verificati in ogni punto di accesso** prima di ottenere qualsiasi autorizzazione.

### **Segmentazione della rete**

**Segmentazione della Rete (Network Segmentation)**: questo principio si basa sulla divisione della rete in segmenti per rendere più semplice la loro messa in sicurezza.

Esempio: **DMZ Network (Demilitarized Zone)**

![[Pasted image 20250319101824.png]]

---

## **VLAN & VPN**

### **VLAN**

Una **VLAN (Virtual Local Area Network)** è una rete logica che separa dispositivi all'interno della stessa rete fisica. Serve per segmentare il traffico e migliorare la sicurezza e l'efficienza della rete aziendale.
#### **Come funziona?**

- Una VLAN divide una rete fisica in più reti logiche indipendenti.
- I dispositivi appartenenti a VLAN diverse non possono comunicare direttamente tra loro senza un router o un firewall.
- Usa switch gestiti e tag VLAN (IEEE 802.1Q) per separare il traffico.
#### **Esempi di utilizzo:**

- **Segmentazione della rete aziendale**: Separare i dipendenti dal reparto IT o dai server.
- **Reti guest**: Creare una VLAN per ospiti senza accesso alla rete interna.

---

### **VPN**

Una **VPN (Virtual Private Network)** è una tecnologia che crea una connessione sicura e crittografata tra un dispositivo e una rete privata su Internet.

#### **Come funziona?**

- Crea un **tunnel sicuro** tra il client e un server remoto.
- **Cifra il traffico**, impedendo a terze parti di intercettarlo.
- Può essere basata su protocolli come OpenVPN, IPsec, WireGuard.

#### **Esempi di utilizzo:**

- **Per il lavoro da remoto**, garantisce connessioni aziendali protette.
- **Per la navigazione su reti pubbliche**, protegge da attacchi hacker.
- **Per superare restrizioni geografiche**, consente di accedere liberamente a contenuti e servizi.

---

### **Detection & Prevention (Rilevamento e Prevenzione)**

Per proteggere le nostre reti abbiamo bisogno di **rilevare le minacce**:

- Alcuni modi per farlo includono l'uso di strumenti come gli **IDS (Intrusion Detection System)** e i **SIEM (Security Information and Event Management)**.

Allo stesso tempo, dobbiamo **prevenire le minacce**:

- Alcuni modi per farlo includono l'uso di **Antivirus**, **Scanner di vulnerabilità**, **Firewalls**, **IPS**.

---

## **Virtualizzazione & Cloud**

Un **data center on-premise** (o "on-prem") è un'infrastruttura IT situata fisicamente presso l'azienda. Tutti i server, lo storage e le reti sono gestiti e mantenuti internamente. 

Il **cloud** fornisce risorse IT (server, storage, database, networking, software) attraverso Internet, senza la necessità di hardware locale.

### **On-Premise vs Cloud**

I data center richiedono:
- **Potenza**
- **HVAC (Heating, ventilation, and air conditioning)**, ossia riscaldamento, ventilazione e aria condizionata
- **Sistemi antincendio**
- **Ridondanza**

Con il cloud, le aziende possono affidare la gestione e la manutenzione dell'infrastruttura IT a un provider, evitando così i costi e la complessità associati ai data center on-premise. In questo modo, pagano solo per le risorse utilizzate, senza doversi occupare direttamente dell'hardware, degli aggiornamenti e della sicurezza.


### **Modelli di Distribuzione del Cloud**

- **Cloud Pubblico**: Un provider di servizi cloud mette a disposizione l’infrastruttura e le risorse per più aziende su una piattaforma condivisa. **Esempi**: AWS, Microsoft Azure, Google Cloud.
- **Cloud Privato**: L’infrastruttura cloud è dedicata a una singola azienda, che la possiede e gestisce in modo esclusivo, garantendo maggiore controllo e sicurezza.
- **Cloud Ibrido**: Combina un cloud pubblico con un’infrastruttura on-premise o un cloud privato, consentendo flessibilità e ottimizzazione delle risorse.
- **Cloud Comunitario**: Un’infrastruttura condivisa tra più organizzazioni con esigenze simili, come enti governativi o aziende dello stesso settore, per ridurre i costi e migliorare la collaborazione.


### **Modelli di Servizio del Cloud**

I servizi cloud si suddividono in tre principali modelli, a seconda del livello di gestione e responsabilità tra l’azienda e il provider:

- **IaaS (Infrastructure as a Service) – Infrastruttura come Servizio**
	- Fornisce risorse IT di base come **server, storage, rete e macchine virtuali**.
	- L'azienda gestisce i sistemi operativi, le applicazioni e la configurazione dell’infrastruttura.
	- Adatto a chi necessita di **flessibilità e controllo sull’ambiente IT** senza investire in hardware fisico.

- **PaaS (Platform as a Service) – Piattaforma come Servizio**
	- Fornisce un ambiente preconfigurato per lo sviluppo, il testing e il deployment di applicazioni.
	- Include **sistemi operativi, database, middleware e strumenti di sviluppo**, riducendo la necessità di gestione dell'infrastruttura.
	- Ideale per sviluppatori che vogliono concentrarsi sul codice senza preoccuparsi della gestione dei server.

- **SaaS (Software as a Service) – Software come Servizio**
	- Offre **applicazioni già pronte** accessibili via web senza necessità di installazione o manutenzione.
	- Il provider gestisce interamente l'infrastruttura, la sicurezza e gli aggiornamenti.
	- Ideale per aziende che vogliono utilizzare software senza preoccuparsi dell’hosting o della gestione tecnica.


#### **Gestione della Responsabilità tra Provider e Cliente nei Modelli Cloud**

La gestione della responsabilità tra **provider cloud** e **cliente** varia a seconda del modello di servizio adottato (**IaaS, PaaS, SaaS**). Il principio chiave è il **"Shared Responsibility Model" (Modello di Responsabilità Condivisa)**, secondo cui alcune funzioni sono gestite dal provider e altre dal cliente.

In generale, **il provider ha la responsabilità di ciò che fornisce/gestisce al/per il cliente**.

