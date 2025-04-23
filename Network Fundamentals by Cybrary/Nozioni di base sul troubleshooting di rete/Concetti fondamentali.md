## **Metodologia di risoluzione dei problemi di rete**

Ecco un esempio di lista di controllo semplificata per la risoluzione dei problemi:

1. **Definisci il problema**: inizia comprendendo a fondo il problema segnalato, raccogliendo quante più informazioni possibili dagli utenti o dai sistemi di monitoraggio per individuare i sintomi del problema.

2. **Identifica i sistemi interessati**: determina quali dispositivi o sistemi stanno riscontrando il problema.

3. **Isola il problema**: determina se il problema è **localizzato** o **sistemico**. Il problema riguarda un singolo utente, una particolare applicazione, un dipartimento specifico, un segmento di rete specifico o l'intera rete?

4. **Controlla la connettività fisica**

5. **Revisiona la configurazione**: esamina le configurazioni dei dispositivi di rete (router, switch, firewall) per assicurarti che siano configurate correttamente. Verificare la presenza di indirizzi IP, sottoreti, VLAN o elenchi di controllo accessi non configurati correttamente.

6. **Ping and Trace Route**: usa gli strumenti ping e traceroute per testare la connettività di rete di base e identificare potenziali strozzature o problemi di routing. Inizia con i test locali e muoviti gradualmente verso l'esterno.

7. **Controlla i DNS e la risoluzione dei nomi**: usare **nslookup** (Windows) o **dig** (Unix) per verificare la risoluzione DNS. Assicurarsi che i server DNS siano raggiungibili e configurati correttamente.

8. **Esamina il traffico di rete**: se necessario, acquisire pacchetti di rete utilizzando strumenti come **Wireshark** o **TCDump** e analizzare il traffico acquisito per identificare anomalie, errori o traffico eccessivo che potrebbe causare il problema.


---

## **Strumenti del mestiere**

È possibile eseguire un'efficace risoluzione dei problemi di rete utilizzando strumenti semplici. Ecco alcuni esempi comuni:

- **Ping**: Il comando `ping` è uno strumento di base che utilizza il **protocollo ICMP** per verificare la raggiungibilità di un host su una rete IP (Internet Protocol) e misurare il tempo di andata e ritorno (latency) dei pacchetti inviati.

> [!ICMP protocol]
> 
> 	ICMP (Internet Control Message Protocol) è un protocollo della suite TCP/IP utilizzato per inviare messaggi di errore e diagnostica tra dispositivi di rete. Non viene impiegato per il trasferimento di dati, ma per segnalare problemi come l'inaccessibilità di un host o il superamento del tempo limite di un pacchetto. Strumenti come ping e traceroute si basano su ICMP per monitorare la connettività di rete. 
> 	
> 	Nel caso del comando ping, ICMP viene utilizzato per inviare messaggi Echo Request all'host di destinazione, che risponde con un messaggio Echo Reply se è raggiungibile. Misurando il tempo tra l'invio della richiesta e la ricezione della risposta, ping calcola la latenza della connessione e verifica eventuali perdite di pacchetti.

- **Traceroute** (su sistemi Unix) e **Tracert** (su Windows): sono strumenti di diagnostica di rete che tracciano il percorso seguito dai pacchetti dal proprio computer fino all'host di destinazione. Questi comandi aiutano a individuare eventuali ritardi o guasti nella rete, mostrando l'elenco dei nodi attraversati e i tempi di risposta di ciascuno.

- **Netstat**: è un comando da riga di comando che fornisce informazioni dettagliate sulle connessioni di rete attive, le porte in ascolto, le tabelle di routing e le statistiche dell’interfaccia di rete. È uno strumento utile per diagnosticare problemi di connettività e monitorare il traffico di rete.

- **Nslookup** (su Windows) e **Dig** (su Unix): sono strumenti di rete utilizzati per interrogare i server **DNS** (Domain Name System) e ottenere informazioni sulla risoluzione dei nomi di dominio in indirizzi IP (e viceversa). Sono utili per diagnosticare problemi di DNS, verificare la configurazione dei record e analizzare il funzionamento dei server DNS.

- **Ipconfig/Ifconfig/ip a**: `ipconfig` (su Windows) e `ifconfig / ip a` (su sistemi basati su Unix) sono comandi utilizzati per visualizzare e gestire la configurazione delle interfacce di rete. Sono utili per verificare le impostazioni di rete sul tuo computer locale.

> [!Interfaccia loopback (lo)]
> 
> 	L'interfaccia lo (loopback) fa riferimento all'interfaccia di loopback del sistema operativo, che consente a un dispositivo di comunicare con sé stesso senza passare attraverso una rete fisica. L'indirizzo IP associato all'interfaccia lo è tipicamente 127.0.0.1 (IPv4) o ::1 (IPv6). Questa interfaccia è spesso utilizzata per testare servizi di rete locali o per la comunicazione tra processi all'interno dello stesso sistema.

- **TCPDump**: è un analizzatore di pacchetti per sistemi Unix/Linux, simile a **Wireshark**, ma utilizzabile da riga di comando. Permette di catturare e visualizzare il traffico di rete in tempo reale, offrendo un potente strumento per l’analisi e la diagnostica delle comunicazioni di rete.

- **Tester per cavi**: sono strumenti utilizzati per verificare la corretta funzionalità dei cavi di rete, individuando eventuali problemi come cortocircuiti, interruzioni o connessioni difettose. Questi tester sono utili per diagnosticare guasti hardware, come cavi danneggiati o connettori malfunzionanti, che possono causare problemi di connettività nella rete.

---

## **Risoluzione dei problemi livello per livello**

La connettività di rete è suddivisa in tre livelli primari:

- Livello 1: fisico
- Livello 2: collegamento dati
- Livello 3: rete

### **Risoluzione dei problemi al livello 1 (Fisico)**

Se il livello fisico presenta problemi, tutti i livelli superiori falliranno. L'analisi si concentra su **scheda di rete (NIC), cavi e porte di commutazione**.

1. **Verifica della NIC**: Controllare i registri di sistema per guasti hardware. Se necessario, sostituire la scheda NIC o testare con una NIC USB.
    
2. **Controllo dei cavi**: Sostituire il cavo **UTP** tra l'host e il jack a parete, nonché quello tra il **pannello patch** e lo switch.
    
3. **Ispezione della porta dello switch**: Verificare eventuali problemi o blocchi (es. restrizioni MAC su switch Cisco). Se necessario, spostare l’host su un’altra porta della stessa **VLAN**.
    
4. **Test del cablaggio nel muro**: Sebbene raro, un cavo interno difettoso può causare problemi. Se non è disponibile un **tester per cavi**, provare un altro jack vicino.

### **Risoluzione dei problemi al livello 2 (Collegamento dati)**

A questo livello si analizza la **comunicazione locale nella LAN** tra host e switch.

1. **Verifica della connettività**: Controllare se l'host può comunicare con altri dispositivi nella stessa sottorete.
    
2. **Cache ARP**: Esaminare la cache ARP su host locali e remoti per individuare eventuali mappature errate tra **indirizzi MAC e IP**.
    
3. **Tabella MAC dello switch**: La **tabella CAM** (Content Addressable Memory) associa gli indirizzi MAC alle porte dello switch. Se le informazioni sono obsolete o errate, potrebbe essere necessario cancellarle e aggiornarle.
    
4. **Configurazione VLAN**: Assicurarsi che la porta dello switch sia assegnata alla VLAN corretta per garantire la connettività tra gli host.

### **Risoluzione dei problemi al livello 3 (Rete)**

A questo livello si analizza il movimento dei pacchetti **IP** tra reti diverse, coinvolgendo host e router.

#### **Verifiche di base:**

1. **Indirizzo IP**: L’host ha un IP corretto?
2. **Maschera di sottorete**: È configurata correttamente?
3. **Gateway predefinito**: L’host ha il gateway giusto?
4. **Connettività**:
    - L’host può raggiungere il gateway?
    - Il gateway può comunicare con l’host?
    
#### **Configurazione DHCP:**

- Gli indirizzi IP possono essere assegnati manualmente o tramite **DHCP**.
- Con **DHCP**, gli host ottengono IP, subnet mask, gateway e server **DNS**.
- Se la connessione è instabile, provare a **rilasciare e rinnovare** il lease DHCP.

#### **Risoluzione dei nomi:**

Se l’host può raggiungere un server remoto tramite **IP** ma non tramite **nome**, il problema è nel **DNS**.

- Controllare la configurazione DNS dell’host (es. `/etc/resolv.conf` su Linux).
- Se il server DNS è corretto, verificare la sua configurazione (es. **record A** mancanti o errati).
- Un riavvio del servizio DNS potrebbe risolvere il problema.