## **Cyber Kill Chain: Le Fasi di un Attacco Informatico**

Il **Cyber Kill Chain** è un framework sviluppato da **Lockheed Martin** per descrivere le diverse fasi di un attacco informatico. Questo modello aiuta le organizzazioni a comprendere e contrastare le minacce informatiche analizzando le tecniche utilizzate dagli aggressori.

L'attacco non sempre segue una sequenza lineare: un hacker può **ripetere, saltare o modificare le fasi** a seconda delle circostanze. Ecco i **7 passaggi del Cyber Kill Chain**:

1. **Ricognizione (Reconnaissance)** – L'attaccante raccoglie informazioni sul bersaglio, studiando la rete, le vulnerabilità e le potenziali vie di accesso.
2. **Armamento (Weaponization)** – Viene creato il malware o lo strumento di attacco che verrà utilizzato contro la vittima, come un trojan, un exploit o una backdoor.
3. **Consegna (Delivery)** – L'attaccante introduce il malware nella rete della vittima, ad esempio tramite email di phishing, download dannosi o exploit su siti web compromessi.
4. **Sfruttamento (Exploitation)** – Una volta che il malware è attivo nel sistema, l'hacker sfrutta vulnerabilità per ottenere privilegi e muoversi nella rete.
5. **Installazione (Installation)** – Il malware viene installato in modo persistente, spesso con l'aggiunta di backdoor o rootkit per garantire l'accesso continuo.
6. **Comando e Controllo (C2 - Command and Control)** – L'attaccante stabilisce un canale di comunicazione con il malware installato, consentendo il controllo remoto del sistema compromesso.
7. **Azioni sugli Obiettivi (Actions on Objectives)** – Una volta ottenuto il pieno accesso, l'hacker esegue il vero scopo dell'attacco, come il furto di dati, la compromissione di sistemi o la distruzione di infrastrutture.

![[Pasted image 20250316160855.png]]
**Figura**: Cyber Kill Chain

---

## **MITRE ATT&CK Framework: Analisi delle Tattiche e Tecniche degli Attacchi Informatici**

Un altro modello fondamentale per comprendere il comportamento degli attori delle minacce informatiche è il **MITRE ATT&CK Framework**.

ATT&CK è l'acronimo di **Adversarial Tactics, Techniques & Common Knowledge** (Tattiche, Tecniche e Conoscenze Comuni Contraddittorie). Questo framework fornisce un’analisi dettagliata del modo in cui gli aggressori conducono attacchi informatici, identificando le metodologie utilizzate nelle varie fasi.

Pur presentando alcune **sovrapposizioni** con il modello **Cyber Kill Chain** di Lockheed Martin, MITRE ATT&CK offre una visione più dettagliata e modulare degli attacchi.


### **Struttura del MITRE ATT&CK Framework**

MITRE ATT&CK è organizzato in **tre livelli principali**:

- **Tattiche** → Gli obiettivi di un attacco.
- **Tecniche** → I metodi utilizzati per raggiungere gli obiettivi.
- **Procedure** → Esempi reali di attacchi che sfruttano queste tecniche.

L’intero framework è visualizzato in una **matrice** che elenca tutte le possibili tattiche e le relative tecniche di attacco


### **Le 14 Tattiche del MITRE ATT&CK Framework**

MITRE ATT&CK identifica **14 tattiche principali**, ognuna rappresentante una fase o un obiettivo specifico all'interno di un attacco informatico.

1. **Ricognizione (Reconnaissance)** – Raccolta di informazioni sulla vittima dall'esterno per pianificare l’attacco.
2. **Sviluppo delle risorse (Resource Development)** – Creazione o acquisizione di strumenti, credenziali e infrastrutture per l’attacco.
3. **Accesso iniziale (Initial Access)** – Compromissione della rete bersaglio tramite phishing, exploit o credenziali rubate.
4. **Esecuzione (Execution)** – Esecuzione di codice dannoso all'interno del sistema compromesso.
5. **Persistenza (Persistence)** – Mantenere un accesso continuo al sistema infetto, ad esempio attraverso backdoor.
6. **Escalation di privilegi (Privilege Escalation)** – Ottenere privilegi più elevati all'interno del sistema per accedere a più risorse.
7. **Evasione della difesa (Defense Evasion)** – Tecniche per evitare il rilevamento da parte di antivirus e sistemi di sicurezza.
8. **Accesso alle credenziali (Credential Access)** – Furto di credenziali per accedere ad altri account o sistemi.
9. **Scoperta (Discovery)** – Esplorazione della rete e dei sistemi interni per identificare informazioni sensibili o punti deboli.
10. **Movimento laterale (Lateral Movement)** – Espandere la compromissione spostandosi su altri dispositivi della rete.
11. **Collezione (Collection)** – Raccolta di dati sensibili, come file, credenziali o informazioni aziendali.
12. **Comando e controllo (Command and Control, C2)** – Creazione di un canale di comunicazione per controllare i sistemi compromessi da remoto.
13. **Esfiltrazione (Exfiltration)** – Trasferimento dei dati rubati all'attaccante.
14. **Impatto (Impact)** – Manipolazione, distruzione o interruzione dei sistemi e dei dati, come ransomware o attacchi DoS.
15. 

![[Pasted image 20250316162142.png]]

Gli attori delle minacce sviluppano costantemente nuove tecniche di attacco. Per questo motivo, **MITRE aggiorna regolarmente la sua matrice** per includere le TTP documentate e osservate nel mondo reale.

Oltre alla matrice per le **reti aziendali (Enterprise)**, MITRE ATT&CK ha sviluppato altre **matrici specializzate**, tra cui:

- **Mobile** – Attacchi alle piattaforme mobili come Android e iOS.
- **ICS (Industrial Control System)** – Attacchi alle infrastrutture industriali e ai sistemi SCADA.

### **Attacchi di rete comuni**

#### **Minaccia (Threat)**

Una **minaccia** è qualsiasi circostanza o evento che ha il potenziale di **compromettere le operazioni di un'organizzazione** attraverso **accessi non autorizzati, distruzione, divulgazione, modifica di informazioni o attacchi di tipo Denial of Service (DoS)**.  Inoltre, una minaccia rappresenta la possibilità che una fonte di minaccia sfrutti con successo una vulnerabilità di un sistema informatico.

**Ricorda il Triangolo CIA** _(Confidenzialità, Integrità, Disponibilità)_


#### **Vulnerabilità (Vulnerability)**

Una vulnerabilità è una **debolezza** presente in un sistema informatico, nelle procedure di sicurezza, nei controlli interni o nella loro implementazione. Questa debolezza può essere **sfruttata o attivata da una fonte di minaccia**, causando un impatto sulla sicurezza.

**CVE** – _(Common Vulnerabilities and Exposures)_: un database pubblico che raccoglie e classifica le vulnerabilità note.
	
**Esempio:**  
**CVE-2021-44228** – _Log4Shell_ (una grave vulnerabilità di sicurezza nel software Log4j).

**Raccomandazione**: è consigliato controllare i corsi su "CVE" e "OWASP Top 10" i quali trattano in modo approfondito i più famosi attacchi basati sul web.


#### **Attacchi più comuni:**

- **Spoofing**: è una tecnica di attacco in cui un aggressore maschera la propria identità falsificando l'origine dei dati trasmessi, ad esempio modificando l'indirizzo IP o l'indirizzo email. L'obiettivo è ingannare il destinatario per farlo credere che il messaggio o la richiesta provenga da una fonte attendibile, facilitando così accessi non autorizzati o il furto di informazioni.

- **Phishing**: è una tecnica di attacco informatico che sfrutta l'ingegneria sociale per indurre le vittime a fornire informazioni sensibili, come credenziali di accesso o dati bancari. Gli aggressori inviano messaggi (solitamente email) che appaiono provenire da fonti affidabili, inducendo l'utente a cliccare su link fraudolenti o a scaricare allegati dannosi.
	
	- **Spearphishing**: si concentra su singoli individui o organizzazioni specifiche.
	- **Vishing**: si utilizzano chiamate o messaggi vocali fasulli per ingannare le vittime.

- **Man-in-the-Middle (MITM)**: è un tipo di attacco in cui un malintenzionato si inserisce tra due comunicanti (ad esempio, tra un utente e un server) senza che le vittime ne siano consapevoli. L'attaccante intercetta, altera o manipola i dati in transito, ottenendo l'accesso a informazioni sensibili come credenziali, messaggi o transazioni. Un altro termine associato a questo tipo di attacco è **On-Path Attack**, che sta a intendere la stessa cosa.

- **DoS (Denial of Service)** e **DDoS (Distributed Denial of Service)** sono tipi di attacchi informatici mirati a rendere un servizio o una rete inaccessibile agli utenti legittimi.

	- **DoS**: In un attacco DoS, un singolo attaccante sovraccarica un server o una rete con richieste di connessione che non possono essere gestite, causando il malfunzionamento o l'interruzione del servizio. Questo può essere fatto, ad esempio, inviando traffico in eccesso o sfruttando vulnerabilità del sistema.
    
	- **DDoS**: In un attacco DDoS, l'attacco è portato da una **rete distribuita di dispositivi compromessi**, come computer o dispositivi IoT infetti, che inviano grandi volumi di traffico verso il bersaglio. Poiché provengono da molteplici fonti, è più difficile da fermare rispetto a un attacco DoS tradizionale. 

	- **Fragment Attack**: è una tecnica che sfrutta il meccanismo di frammentazione dei pacchetti IP per compromettere il processo di ricomposizione dei dati nei sistemi di rete. Durante la trasmissione, i pacchetti IP vengono suddivisi in frammenti per adattarsi alle diverse dimensioni di trasmissione. Se un attaccante interferisce con questo processo, il sistema target potrebbe non riuscire a ri-assemblare correttamente i pacchetti, interrompendo la comunicazione o sfruttando vulnerabilità nel sistema. Questa tecnica può essere integrata in attacchi più ampi, come DoS o DDoS, per rendere inaccessibili servizi o reti.
	
	- **Over-Sized Packet Attack**: è un attacco che sfrutta l'invio di pacchetti di dimensioni superiori a quelle previste dai protocolli di rete. In pratica, l'attaccante invia pacchetti abbastanza grandi da sovraccaricare il sistema target, sfruttando vulnerabilità nella gestione dei buffer e dei processi di elaborazione dei dati. Questo tipo di attacco può portare a errori di overflow, rallentamenti significativi o addirittura al crash del sistema, compromettendo la disponibilità e la stabilità dei servizi di rete.

- **Remote Code Execution (RCE):** si tratta di una vulnerabilità che consente a un attaccante di eseguire codice arbitrario su un sistema remoto. Sfruttando errori nella gestione degli input o bug del software, l'aggressore può installare malware, modificare dati o ottenere accesso privilegiato, compromettendo così la sicurezza dell'intero sistema.

	- Il termine **Living off the Land** indica una tecnica in cui gli aggressori sfruttano strumenti e utility già presenti e legittimi all'interno di un sistema operativo per condurre attività malevoli.

- **SQL Injection:**  questa tecnica sfrutta la mancanza di adeguata validazione degli input nei database. L'attaccante inserisce comandi SQL malevoli in moduli o URL, inducendo il sistema a eseguire query non autorizzate. Il risultato può essere la fuga di dati sensibili, la manipolazione delle informazioni o addirittura il controllo completo del database.

- **Privilege escalation**: è una tecnica in cui un aggressore sfrutta vulnerabilità o errori di configurazione per ottenere livelli di accesso superiori a quelli originariamente concessi. In pratica, partendo da un account con privilegi limitati, l'attaccante riesce a "scalare" il sistema acquisendo privilegi di amministratore o root. Questo consente di compiere azioni malevoli più estese, come installare malware, modificare configurazioni di sistema o accedere a dati sensibili. Le tecniche di privilege escalation possono sfruttare bug del software, errori nei permessi o configurazioni errate del sistema operativo.


**Alcuni termini utili**

- **Virus**: è un software malevolo che deve essere avviato dall'utente
- **Worm**: è un codice malevolo che può replicarsi
- **Living off the land**: questa tecnica prevede l’uso degli strumenti e delle utility già presenti e legittimi sul sistema per condurre operazioni malevole.
- **Side-Channel Attack**: é un attacco che sfrutta informazioni indirette derivanti dall’implementazione fisica di un sistema, anziché dalle vulnerabilità del software. Misurando segnali come il consumo energetico, le emissioni elettromagnetiche o il tempo di esecuzione, un attaccante può dedurre informazioni sensibili.