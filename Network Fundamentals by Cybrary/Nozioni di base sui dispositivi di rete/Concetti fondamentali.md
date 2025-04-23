## **Dispositivi di rete comuni**

Un **dispositivo di rete** è semplicemente qualsiasi dispositivo che facilita la comunicazione locale o ad ampia area tra i sistemi. L'immagine seguente mostra alcuni dei tipi più comuni di dispositivi di rete utilizzati oggi.

![[Pasted image 20250321185222.png]]

### **Scheda di Interfaccia di Rete (NIC)**

La **scheda di interfaccia di rete (NIC, Network Interface Card)** è un componente hardware fondamentale che consente a un computer, server o dispositivo di rete di connettersi a una rete locale (LAN) o a una rete geografica (WAN).

Le NIC possono essere di due tipi principali:
- **Cablata**: utilizza una connessione Ethernet tramite cavi di rete come il doppino intrecciato (UTP) o la fibra ottica.
- **Wireless**: utilizza il Wi-Fi per la connessione senza fili, basandosi su standard come IEEE 802.11.

### **Connessioni Fisiche e Cablaggio**

Un **cavo a doppino intrecciato non schermato (UTP, Unshielded Twisted Pair)** è comunemente utilizzato per le connessioni di rete cablate. La sequenza tipica del cablaggio in una rete cablata è la seguente:

1. **Connessione del dispositivo**: Il cavo UTP collega la NIC di un computer o server a una presa a muro.
2. **Punto di terminazione**: Dalla presa a muro, un altro cavo UTP corre fino a un pannello patch situato in una sala server o in un armadio di rete.
3. **Connessione allo switch**: Un terzo cavo UTP collega il pannello patch a una porta su uno switch di rete.

### **Switch (Layer 2 e Layer 3)**

Uno **switch** è un dispositivo di rete che opera al **Livello 2** del Modello OSI (collegamento dati). La sua funzione principale è quella di instradare i pacchetti di dati tra dispositivi all'interno della stessa LAN (Local Area Network), utilizzando gli indirizzi MAC per determinare la destinazione dei pacchetti.

Se un dispositivo sulla LAN deve comunicare con un altro dispositivo locale, il traffico verrà semplicemente instradato dallo switch senza coinvolgere un router. Tuttavia, se il traffico deve uscire dalla LAN per raggiungere una rete esterna, lo switch inoltrerà il traffico a un router.

Esistono anche **switch di livello 3**, in grado di operare sia come switch tradizionali che come router. Gli switch Layer 3 possono:
- Creare **LAN virtuali (VLANs)**, separando logicamente i dispositivi anche se fisicamente connessi allo stesso switch.    
- Instradare il traffico tra VLAN senza la necessità di un router separato.
- Migliorare la sicurezza segmentando il traffico di rete.

### **Router (Layer 3)**

Un **router** è un dispositivo di rete che opera al **Livello 3** del Modello OSI (livello di rete). La sua funzione principale è quella di instradare il traffico tra diverse reti. Il router determina il percorso ottimale per inviare i pacchetti e li inoltra verso la rete di destinazione utilizzando indirizzi IP.

Se un dispositivo in una LAN deve comunicare con un dispositivo in un'altra LAN (ad esempio, su Internet), il traffico passa dallo switch locale al router, che lo inoltrerà verso un altro switch o un altro router fino a raggiungere la destinazione.

I router possono supportare funzionalità avanzate come:
- **NAT (Network Address Translation)**, che consente a più dispositivi di condividere un unico indirizzo IP pubblico.
- **Firewall integrato**, che protegge la rete filtrando il traffico indesiderato.
- **VPN (Virtual Private Network)**, che consente connessioni sicure tra reti remote.

### **Punti di Accesso Wireless (Access Point - AP)**

Un **punto di accesso wireless (AP)** consente ai dispositivi wireless di connettersi alla LAN. L'AP è collegato a uno switch tramite un cavo UTP e trasmette il segnale Wi-Fi ai client wireless. Gli AP moderni supportano standard avanzati come Wi-Fi 6 (802.11ax), che offrono maggiore velocità e capacità di connessione per più dispositivi simultanei.

Gli AP possono operare in diverse modalità:
- **Standalone**: configurati manualmente per servire una specifica area.
- **Gestiti da un controller**: centralizzati per una gestione più efficiente.
- **Mesh**: che si collegano dinamicamente tra loro per estendere la copertura senza cablaggio aggiuntivo.

---

## **Dispositivi di rete legacy**

Sebbene oggi siano ormai rari, nelle reti più datate era comune trovare dispositivi come **hub, ponti e ripetitori**.

- **Hub**: simile a uno switch, ma molto meno efficiente. Un hub inoltra il traffico a tutte le porte indiscriminatamente ogni volta che un dispositivo comunica, causando collisioni e rallentamenti della rete. Gli switch, invece, memorizzano una tabella degli indirizzi e inviano i dati solo alla porta corretta. Gli hub erano diffusi quando gli switch erano costosi, ma con la loro riduzione di prezzo sono stati completamente sostituiti.
- **Ponte (Bridge)**: collega due segmenti di rete LAN, unificandoli in un'unica LAN. A differenza dei router, che separano le reti, i ponti permettono la comunicazione trasparente tra i segmenti collegati.
- **Ripetitore (Repeater)**: ogni cavo di rete ha una lunghezza massima oltre la quale il segnale si degrada. I ripetitori servono a rigenerare e amplificare il segnale, permettendo di estendere la distanza della connessione senza perdita di qualità.

---

## **Dispositivi di rete aggiuntivi**

Le moderne reti LAN includono spesso dispositivi e funzionalità avanzate per migliorare sicurezza, accessibilità e gestione del traffico. Tra questi, i più comuni sono:

- **Firewall**: Regola il flusso di traffico tra una rete sicura (ad esempio, una LAN aziendale) e una rete non attendibile (come Internet). I firewall filtrano il traffico in base a porte e protocolli, consentendo solo le connessioni necessarie (ad esempio, HTTPS in uscita) e limitando l'accesso ai server interni (ad esempio, un server web). Forniscono anche **Network Address Translation (NAT)**, che permette a tutti i dispositivi interni di condividere un unico indirizzo IP pubblico (NAT molti-a-uno) o di esporre specifici server interni su Internet (NAT uno-a-uno).
- **Proxy**: Funziona come intermediario tra i client interni e Internet. Tutto il traffico viene instradato attraverso il proxy, che può filtrare e bloccare contenuti dannosi utilizzando liste di siti vietati. In molte configurazioni, solo il proxy è autorizzato ad accedere direttamente a Internet, obbligando tutti gli utenti della rete a passare attraverso di esso per navigare.
- **Virtual Private Network (VPN)**: Consente a dispositivi esterni di connettersi alla LAN come se fossero fisicamente presenti nella rete locale. Questo avviene creando un "tunnel" sicuro tramite protocolli come **IPsec**, garantendo così la protezione dei dati trasmessi.

 **Nota**: Molti firewall moderni integrano funzionalità di VPN e proxy, fornendo un'unica soluzione per sicurezza e accesso remoto.

---

## **Reti ad Ampia Area (WAN)**

Le **Wide Area Network (WAN)** sono reti che collegano dispositivi e infrastrutture su lunghe distanze, spesso attraverso servizi forniti da operatori di telecomunicazioni. A differenza delle LAN, che operano in un ambiente locale con velocità elevate, le WAN devono affrontare sfide legate alla latenza, alla larghezza di banda e alla sicurezza.

Una WAN è composta da una combinazione di **hardware di rete** e **protocolli di comunicazione** che consentono la trasmissione dei dati tra sedi remote, come uffici aziendali, data center o filiali. Alcuni elementi chiave di una WAN includono:

- **Router**: gestiscono il traffico tra le reti locali e la WAN, instradando i dati verso le destinazioni corrette.
- **Circuiti dedicati**: linee affittate da operatori di telecomunicazioni per garantire una connessione stabile e privata tra sedi remote.
- **Protocolli WAN**: utilizzati per il trasporto dei dati su lunghe distanze, come **Frame Relay**, **MPLS (Multiprotocol Label Switching)** e, più recentemente, **SD-WAN (Software-Defined WAN)**.

**Esempio: Frame Relay**
Uno dei protocolli storici utilizzati nelle WAN è **Frame Relay**, che consente la trasmissione di dati tra router collegati tramite linee seriali affittate da operatori di telecomunicazioni. Queste connessioni formano tipicamente una **topologia a stella** (con un hub centrale) o una **topologia mesh** (con collegamenti diretti tra più siti).

Le WAN sono generalmente più lente delle LAN, con velocità di trasmissione limitate dalla tecnologia disponibile e dai costi operativi. Per migliorare le prestazioni e prevenire congestioni sono necessarie specifiche precauzioni.

![[Pasted image 20250321200313.png]]

