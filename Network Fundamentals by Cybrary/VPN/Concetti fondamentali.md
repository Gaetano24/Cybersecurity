## **Panoramica**

Una **rete privata virtuale (VPN)** è una tecnologia che consente di creare una connessione sicura e crittografata su reti pubbliche o non affidabili, come Internet. Grazie alla VPN, gli utenti possono accedere in modo protetto alle risorse interne e trasmettere dati in totale sicurezza.

Utilizzando avanzati protocolli di crittografia, una VPN protegge la privacy e la riservatezza delle informazioni, crittografando i dati mentre viaggiano tra i dispositivi connessi. Inoltre, supporta diversi metodi di autenticazione, come password e certificati digitali, garantendo un ulteriore livello di sicurezza.

Oltre alla protezione dei dati, una VPN può mascherare la posizione reale e l'indirizzo IP dell'utente, offrendo così un maggiore anonimato durante la navigazione online.

## **Come funziona una VPN?**

Quando un utente attiva la VPN sul proprio dispositivo, tutti i dati trasmessi vengono crittografati e instradati attraverso il server VPN. Questo processo nasconde i dettagli del traffico Internet e dell'indirizzo IP, proteggendoli da provider di servizi Internet (ISP) e altri soggetti indesiderati. Una volta che i dati richiesti raggiungono il dispositivo dell'utente, l'app VPN li decifra, rendendoli accessibili e utilizzabili.

Un aspetto distintivo di un server VPN è l'impiego di una gamma di **protocolli di sicurezza** progettati per garantire privacy e protezione avanzata. Alcuni protocolli si concentrano sulla crittografia dei dati, altri assicurano la loro integrità, mentre altri ancora bloccano accessi non autorizzati e potenziali minacce informatiche.

![[Pasted image 20250329194407.png]]


---

## **Protocolli VPN Comuni**

Ecco una panoramica dei principali protocolli VPN utilizzati per garantire sicurezza, stabilità e velocità nelle connessioni private:

- **Protocollo di Tunneling Punto-Punto (PPTP)**  
    PPTP è uno dei protocolli VPN più datati, sviluppato principalmente per i sistemi Windows. Sebbene sia facile da configurare e integrato gratuitamente in Windows, presenta vulnerabilità significative. Utilizza il metodo di autenticazione **MS-CHAP**, noto per essere insicuro, e il vecchio algoritmo di crittografia **RC4**, considerato obsoleto.
    
- **Protocollo di Tunnel di Livello 2 (L2TP)**  
    L2TP è un'evoluzione del PPTP e offre maggiore affidabilità. A differenza di PPTP, che utilizza il protocollo TCP per la stabilità, L2TP sfrutta **UDP** per garantire velocità superiori. Tuttavia, i tunnel L2TP di per sé non forniscono crittografia, motivo per cui vengono spesso combinati con **IPsec** per una protezione avanzata.
    
- **Secure Socket Tunneling Protocol (SSTP)**  
    SSTP utilizza **SSL 3.0** per stabilire connessioni sicure ed è particolarmente utile per bypassare firewall restrittivi, poiché opera sulla porta **TCP 443**, la stessa utilizzata per il traffico HTTPS. Tuttavia, l’uso di SSL 3.0 comporta un rischio di sicurezza dovuto alla vulnerabilità **POODLE**, rendendo questo protocollo meno consigliato.
    
- **Protocollo di Sicurezza Internet (IPsec)**  
    IPsec è un insieme di protocolli progettati per migliorare la sicurezza del traffico IP. Offre autenticazione, crittografia, integrità dei dati e uno scambio sicuro delle chiavi crittografiche. È spesso utilizzato in combinazione con L2TP o come soluzione indipendente per connessioni altamente sicure.
    
- **OpenVPN**  
    OpenVPN è una delle soluzioni VPN più sicure e flessibili, completamente open source. Utilizza la **libreria OpenSSL** per implementare una crittografia avanzata ed è compatibile con diverse tecnologie di autenticazione, tra cui **certificati digitali** e **chiavi pre-condivise** per verificare l'identità di client e server. Grazie alla sua elevata configurabilità, è ampiamente utilizzato sia in ambito aziendale che personale.

---

## **IPsec**

**IPsec** è un'estensione del protocollo **IP**, progettata per aggiungere sicurezza alla trasmissione dei dati in rete. Il protocollo IP, di per sé, ha la funzione di instradare i pacchetti dati tra reti diverse, ma non include misure di protezione contro intercettazioni o modifiche non autorizzate.

Un tipico pacchetto IP è strutturato in modo che l'**intestazione TCP** avvolga i dati trasmessi, mentre l'intero pacchetto viene poi incapsulato all'interno dell'**intestazione IP**. 

![[Pasted image 20250329183616.png]]

IPsec utilizza il protocollo **Authentication Header (AH)**, **Encapsulation Security Protocol (ESP)** o entrambi per fornire autenticazione e crittografia. Di seguito, vediamo un pacchetto IP con il protocollo AH e uno che utilizza il protocollo ESP:

![[Pasted image 20250329183704.png]]

È importante notare che la struttura dei pacchetti varia a seconda della modalità **IPsec** utilizzata. IPsec supporta due modalità operative: **Transport Mode** e **Tunnel Mode**.

- **Transport Mode** viene utilizzato per proteggere le comunicazioni dirette tra due dispositivi (peer-to-peer). In questa modalità, solo il payload del pacchetto IP viene crittografato, mentre l'intestazione IP originale rimane visibile.

	![[Pasted image 20250329183704.png]]

- **Tunnel Mode** (noto anche come **site-to-site**) è impiegato per connettere due reti remote, come sedi aziendali distinte. In questa configurazione, l'intero pacchetto IP originale viene incapsulato in un nuovo pacchetto con una seconda **intestazione IP**, garantendo una protezione completa durante la trasmissione.

	![[Pasted image 20250329183841.png]]

Il punto chiave da comprendere è che **il protocollo IP, da solo, non offre alcuna protezione**, ma può essere incapsulato con altri protocolli di sicurezza, come **IPsec**, per garantire una comunicazione sicura.

Per stabilire una connessione **IPsec**, sono necessari **cinque passaggi fondamentali**:

1. **Attivazione del tunnel** (_noto anche come traffico interessante_) – Il tunnel IPsec viene avviato quando viene rilevato traffico che necessita di protezione.

2. **Fase 1 di Internet Key Exchange (IKE)** – Viene stabilito un canale sicuro tra le due parti, autenticandole e negoziando i parametri di sicurezza.
    
3. **Fase 2 di Internet Key Exchange (IKE)** – Viene creata la sessione IPsec vera e propria, negoziando le chiavi crittografiche per la protezione dei dati.
    
4. **Trasferimento dati** – I pacchetti vengono crittografati e trasmessi in modo sicuro attraverso il tunnel IPsec.
    
5. **Terminazione del tunnel** – La connessione IPsec viene chiusa quando non è più necessaria o quando il tempo di vita della sessione scade.

### **Come funziona una connessione IPsec ?**

Il **primo passo** nell'avvio di una connessione **IPsec** avviene quando un router, un firewall, un'appliance VPN o un software client VPN rilevano traffico **interessante**, ovvero dati che devono essere protetti.

Ad esempio, consideriamo due uffici collegati tramite un **tunnel VPN site-to-site**.
- Il primo ufficio ha una sottorete interna **192.168.1.0/24**
- Il secondo ufficio ha una sottorete interna **10.10.10.0/24**

Quando il firewall della rete **192.168.1.0/24** rileva traffico destinato alla rete **10.10.10.0/24**, lo considera **traffico interessante** e avvia automaticamente una connessione **IPsec sicura** con il firewall della rete di destinazione.

> **Nota:** Nelle connessioni VPN site-to-site, spesso l'amministratore di rete avvia manualmente il tunnel, invece di attendere che venga attivato dal traffico di rete.

#### **IKE Phase 1 e IKE Phase 2: Un tunnel dentro un tunnel**

Una volta attivato il tunnel, entrano in gioco due fasi fondamentali di **Internet Key Exchange (IKE)**:

1. **IKE Phase 1**
    - Si occupa dell’**autenticazione** tra le due parti
    - Stabilisce un canale sicuro per negoziare i parametri della fase successiva
    - È computazionalmente più pesante e più lenta rispetto alla fase 2
    
2. **IKE Phase 2**
    - Gestisce la **crittografia** dei dati e il loro trasferimento sicuro
    - Avviene all’interno del tunnel creato nella fase 1
    - È più veloce e ottimizzata per la trasmissione continua dei dati

Questi tunnel vengono chiamati **Associazioni di Sicurezza (Security Associations - SA)**. La separazione tra fase 1 e fase 2 è fondamentale per **ottimizzare le prestazioni**, poiché consente di utilizzare un tunnel iniziale per operazioni lente e complesse, mentre un secondo tunnel incapsulato gestisce la crittografia in modo efficiente e rapido.

![[Pasted image 20250329185007.png]]

I pacchetti vengono trasmessi tra l'**iniziatore** e il **ricevitore** finché l'**Associazione di Sicurezza (SA)** rimane valida. Una volta che la SA scade o diventa non valida, il tunnel viene chiuso automaticamente.

In alcuni casi, problemi di connettività possono causare il **timeout** e la chiusura imprevista di una SA, interrompendo la comunicazione sicura. Per questo motivo, gli amministratori di rete dovrebbero monitorare costantemente lo stato dei tunnel VPN, assicurandosi che eventuali SA scadute o interrotte vengano riavviate tempestivamente per mantenere la connessione operativa.

Per uno sguardo approfondito su IKE, guarda questo video su YouTube: [https://www.youtube.com/watch?v=15amNny_kKI](https://www.youtube.com/watch?v=15amNny_kKI)


---
