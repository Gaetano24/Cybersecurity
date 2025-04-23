## **Definizione di porta e protocollo**

- Una **porta** è un punto di accesso che può essere aperta o chiusa. Un amministratore di rete potrebbe infatti chiudere volutamente una porta per aumentare la sicurezza e potrebbe designare quale porta utilizzare per un dato protocollo o per un dato servizio. In sostanza, le **porte di rete** sono numeri che identificano i servizi in esecuzione su un dispositivo.

- Un **protocollo** è un insieme di regole e convenzioni che definiscono come avviene la comunicazione tra due o più entità. Ogni protocollo ha un suo scopo personale.

---

## **Porte e protocolli sicuri vs insicuri** 

Quando si parla di **porte e protocolli sicuri vs insicuri**, ci si riferisce ai servizi di rete che utilizzano **connessioni cifrate (sicure)** o **non cifrate (insicure)**.

![[Pasted image 20250316120953.png]]

![[Pasted image 20250316121031.png]]

### **Porte e protocolli comuni**

Partiamo dai protocolli già menzionati:

-  **IP (Internet Protocol)**
	- **Ruolo**: Indirizza i pacchetti di dati sulla rete, permettendo la comunicazione tra dispositivi.
	- **Funzionamento**: Divide i dati in pacchetti e li invia da un punto A a un punto B, senza garanzia di consegna.
	
-  **TCP (Transmission Control Protocol)**
	- **Ruolo**: Protocollo di trasporto **affidabile**, assicura che i dati arrivino completi e nell’ordine corretto.
	- **Caratteristiche**:  
	     - Connessione stabile (handshake a 3 vie)  
	     - Controllo degli errori  
	     - Ritrasmissione dei pacchetti persi

- **UDP (User Datagram Protocol)**
	- **Ruolo**: Protocollo di trasporto **veloce ma non affidabile**, non garantisce l’ordine o la ricezione dei pacchetti.
	- **Caratteristiche**:  
	     - Nessuna connessione (stateless)  
	     - Nessuna correzione di errore  
		 - Più leggero e rapido rispetto a TCP
	

| **Porta (Insicura)** | **Protocollo (Insicuro)** | **Compito**                                    | **Motivo di Insicurezza**                               | **Porta (Sicura)** | **Protocollo (Sicuro)**     | **Motivo di Sicurezza**                                   |
| -------------------- | ------------------------- | ---------------------------------------------- | ------------------------------------------------------- | ------------------ | --------------------------- | --------------------------------------------------------- |
| **21**               | FTP                       | Trasferimento di file tra client e server      | Trasmette file e credenziali in chiaro                  | **22**             | SFTP (Secure FTP)           | Usa SSH per la cifratura dei dati e autenticazione sicura |
| **23**               | Telnet                    | Accesso remoto ai dispositivi                  | Connessione remota senza crittografia, password esposte | **22**             | SSH (Secure Shell)          | Connessione remota cifrata e sicura                       |
| **25**               | SMTP                      | Invio di email tra server di posta             | Nessuna crittografia per inviare email                  | **587**            | SMTPS (SMTP con TLS)        | Crittografia TLS per protezione email                     |
| **143**              | IMAP                      | Accesso alle email da più dispositivi          | Accesso email non cifrato                               | **993**            | IMAPS (IMAP con SSL/TLS)    | Protegge la posta elettronica con crittografia            |
| **37**               | Time                      | Sincronizzazione dell'orario tra dispositivi   | Sincronizzazione oraria non sicura                      | **123**            | NTP (Network Time Protocol) | Permette sincronizzazione oraria più sicura               |
| **53**               | DNS                       | Conversione di nomi di dominio in indirizzi IP | Le richieste DNS possono essere intercettate            | **853**            | DoT (DNS over TLS)          | Crittografia delle richieste DNS per evitare attacchi     |
| **80**               | HTTP                      | Trasferimento di pagine web                    | Nessuna protezione per il traffico web                  | **443**            | HTTPS (HTTP con SSL/TLS)    | Crittografia end-to-end per la navigazione sicura         |
| **161/162**          | SNMP v1/v2                | Monitoraggio e gestione di dispositivi di rete | Comunicazione di rete non cifrata                       | **161/162**        | SNMP v3                     | Introduce autenticazione e crittografia dei dati          |
| **389**              | LDAP                      | Gestione di directory di utenti e risorse      | Trasmissione dati non cifrata                           | **636**            | LDAPS (LDAP over SSL)       | Protegge le informazioni delle directory con SSL/TLS      |

Il **SNMP (Simple Network Management Protocol)** è un protocollo di rete utilizzato per la gestione e il monitoraggio di dispositivi connessi a una rete IP, come **router, switch, server, stampanti e dispositivi IoT**.  Tramite questo protocollo è possibile collezione un sacco di informazioni sulla rete. 

**LDAP (Lightweight Directory Access Protocol)** è un protocollo standard utilizzato per accedere e gestire informazioni in **directory service**, ovvero database ottimizzati per la lettura, la ricerca e l'autenticazione degli utenti e delle risorse in rete.

#### **Un po' di più su FTPS e SFTP

Alcuni protocolli si occupano della comunicazione, altri della gestione e altri ancora della sicurezza. Spesso, questi protocolli vengono combinati per garantire sia l'efficienza che la protezione dei dati.

Ad esempio, un protocollo di comunicazione può essere integrato con un protocollo di sicurezza per proteggere le informazioni trasmesse. Un caso comune è quello delle versioni sicure del File Transfer Protocol (FTP): **FTPS** e **SFTP**.

- **FTPS** utilizza il protocollo FTP con l'aggiunta della crittografia **SSL (Secure Sockets Layer)** per garantire la sicurezza delle connessioni.
- **SFTP**, invece, sfrutta il protocollo **SSH (Secure Shell)** per stabilire un canale sicuro attraverso il quale vengono trasferiti i file, fornendo una protezione più robusta.

---

## **Che cos'è una Shell?**

- **Shell**: è un programma che consente di controllare un computer tramite un'interfaccia a riga di comando, nota come **Command-Line Interface (CLI)**. A differenza di un'interfaccia grafica, la shell si basa esclusivamente su un **prompt dei comandi**, attraverso il quale l'utente può eseguire una serie di istruzioni testuali per gestire e interagire con il sistema operativo.

- **SSH** sta per **Secure Shell**. Secondo Wikipedia, è "un protocollo di rete crittografico utilizzato per eseguire servizi di rete in modo sicuro su una rete non protetta". Le sue applicazioni più comuni includono **l'accesso remoto ai server** e **l'esecuzione di comandi da riga di comando**. 

	Per un hacker, ottenere le credenziali SSH di un server rappresenterebbe un enorme vantaggio, poiché gli consentirebbe di **accedere e controllare il sistema** da remoto. Per questo motivo, è fondamentale proteggere tali credenziali, che dovrebbero essere accessibili **solo agli amministratori autorizzati**.

- Una **web shell** è uno script malevolo utilizzato da un hacker per **accedere e controllare un server web da remoto**.

	Nel contesto della cybersecurity, l'espressione _"get a shell"_ si riferisce generalmente alla capacità di un hacker di ottenere il **controllo di un server**, consentendogli di eseguire comandi e condurre ulteriori attacchi.

