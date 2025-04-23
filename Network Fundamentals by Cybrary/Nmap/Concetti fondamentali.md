## **Scansione ed Enumerazione con Nmap**

La scansione e l'enumerazione sono due tecniche fondamentali per la raccolta di informazioni su host e servizi all'interno di una rete.

- **Scansione**: consiste nell'utilizzo di strumenti e metodi per identificare host attivi, porte aperte e i servizi in esecuzione su tali porte.
- **Enumerazione**: implica la raccolta di dettagli più approfonditi sugli host scoperti, come il sistema operativo in uso, la versione dei software presenti e le eventuali vulnerabilità.

### **Nmap: Il Network Mapper**

Uno degli strumenti più potenti per la scansione e l'enumerazione è **Nmap** (Network Mapper). Inizialmente progettato per mappare rapidamente grandi reti, Nmap si è evoluto fino a includere numerose funzionalità per l'analisi e la sicurezza delle reti. È lo strumento ideale per comprendere la struttura di una rete e individuare eventuali vulnerabilità.

In questo laboratorio ci concentreremo su quattro fasi principali della scansione con Nmap (su un totale di undici):

1. **Host Discovery (Scansione Ping)** – Identifica gli host attivi sulla rete.
2. **Scansione delle porte** – Determina quali porte sono aperte su un host.
3. **Rilevamento del sistema operativo** – Deduce quale OS è in esecuzione.
4. **Rilevamento della versione del servizio** – Identifica il software eseguito sulle porte aperte.

_**The Phases of an Nmap Scan:**_ https://nmap.org/book/nmap-phases.html

### **Concetto di Porta e Protocollo TCP**

Le porte consentono l'identificazione delle applicazioni di rete su un host.

- Un host viene identificato tramite il suo **indirizzo IP** (simile all'indirizzo di un edificio residenziale).
- Una **porta** è come un numero di appartamento all'interno di quell'edificio, permettendo di indirizzare correttamente i dati all'applicazione giusta.

Le scansioni di rete si concentrano principalmente sulle **porte TCP**, il tipo più comune di porta utilizzato su Internet. T**CP (Transmission Control Protocol)** è un insieme di regole che definisce la comunicazione tra sistemi. Una delle sue caratteristiche principali è la **stretta di mano a tre vie**, che avviene così:

1. **Client → Server**: SYN (sincronizzazione)
2. **Server → Client**: SYN/ACK (sincronizzazione e riconoscimento)
3. **Client → Server**: ACK (riconoscimento)

Una volta stabilita la connessione, i dati possono essere trasmessi in modo affidabile.

Questa regola semplifica la scansione delle porte TCP: **un servizio attivo su una porta aperta risponderà sempre a una richiesta di connessione (SYN), confermandone la disponibilità**.

### **Come Nmap Analizza le Risposte**

Nmap invia pacchetti di dati agli host e analizza le risposte per ottenere informazioni dettagliate. Per farlo, utilizza un database di **impronte digitali** che permette di confrontare le risposte ricevute e identificare sistemi e servizi.

Esempio:

- Supponiamo di voler distinguere tra due persone, **Mary** e **Molly**.
- Dici _"Hello"_ e entrambe rispondono _"Hello"_ → nessuna differenza evidente.
- Dici _"Ciao, come stai?"_ e Mary risponde _"Sto bene, e tu?"_ mentre Molly dice _"Bene, e tu?"_ → ora puoi distinguerle.

Allo stesso modo, Nmap utilizza risposte specifiche per identificare con precisione i dettagli degli host e dei servizi in esecuzione.

---

## **Tipi di scansione con Nmap**

Nella maggior parte degli scenari (quasi tutti), utilizzerai uno di questi tipi di scansione TCP:

- ### **-sT (Scansione TCP Connect)**
	
	Nota anche come **“full-open”** o **Connect scan**, questa scansione completa l'intera stretta di mano TCP prima di terminare la connessione. Il processo avviene nel seguente modo:

	1. **Client → Server**: SYN (sincronizzazione)
	2. **Server → Client**: SYN/ACK (sincronizzazione e riconoscimento)
	3. **Client → Server**: ACK (riconoscimento)
	4. **Client → Server**: ACK (riconoscimento)
	5. **Client → Server**: RST (reset per chiudere la connessione)

	![[Pasted image 20250326155152.png]]

	Questa è la scansione predefinita se si esegue Nmap senza privilegi di root, quindi il comando seguente è equivalente:

	![[Pasted image 20250326155253.png]]

- ### **-sS (Scansione SYN Stealth)**
	
	Chiamata anche **“half-open” scan**, questa tecnica interrompe la stretta di mano TCP prima del completamento, terminando la connessione con un pacchetto di reset. Il processo avviene così:
	
	1. **Client → Server**: SYN (sincronizzazione)
	2. **Server → Client**: SYN/ACK (sincronizzazione e riconoscimento)
	3. **Client → Server**: RST (reset per terminare la connessione)
	
	Il termine **“stealth”** si riferisce alla registrazione nei log delle applicazioni: **poiché la connessione non viene completata, è meno probabile che venga registrata**. Tuttavia, firewall moderni e sistemi IDS/IPS sono in grado di rilevare questo tipo di traffico sospetto.
	
	Nonostante non sia necessariamente più discreta della scansione **full-open** (-sT), la scansione SYN è più **veloce** e utilizza **meno larghezza di banda**, rendendola un'opzione preferita per l'analisi delle reti.

	![[Pasted image 20250326155729.png]]
	
	Questa è la scansione predefinita se si esegue Nmap con privilegi di root, quindi il comando seguente è equivalente:

	![[Pasted image 20250326155803.png]]


	**Nota**: Le scansioni **-sS** nella foto sopra hanno anche identificato una porta aggiuntiva. In genere, sia -sS che -sT riveleranno le stesse porte, ma **non è insolito vedere variazioni nei risultati tra le varie tecniche di scansione**.


Ecco una tabella che riassume i **pro e contro** del **TCP Connect Full Scan** e del **TCP SYN Scan (Semi-Open)** in Nmap: 

| **Caratteristica**         | **TCP Connect Full Scan**                         | **TCP SYN Scan (Semi-Open)**                         |
| -------------------------- | ------------------------------------------------- | ---------------------------------------------------- |
| **Affidabilità**           | Alta (connessione completa)                       | Meno affidabile (potenziale blocco di pacchetti SYN) |
| **Velocità**               | Lenta                                             | Veloce                                               |
| **Rilevabilità**           | Alta (facilmente rilevabile)                      | Bassa (meno rilevabile)                              |
| **Richiesta privilegi**    | Nessuna (funziona senza privilegi elevati)        | Richiede privilegi elevati (root)                    |
| **Utilizzo risorse**       | Maggiore (utilizza più risorse di sistema e rete) | Minore (utilizza meno risorse)                       |
| **Compatibilità**          | Alta (funziona su tutti i sistemi)                | Limitata (può essere bloccato dai firewall)          |
| **Visibilità per IDS/IPS** | )Alta (facile da rilevare                         | Bassa (difficile da rilevare)                        |


**Nota**: Nmap offre anche alcune opzioni di scansione più specializzate, tra cui:

- **-sA (Scansione ACK)**: utile per analizzare il comportamento dei firewall e determinare quali porte sono filtrate (https://nmap.org/book/scan-methods-ack-scan.html).

- **-sU (Scansione UDP)**: impiegata per individuare servizi in esecuzione su porte UDP, sebbene sia più lenta rispetto alla scansione TCP a causa della natura senza connessione del protocollo UDP (https://nmap.org/book/scan-methods-udp-scan.html).

Tuttavia, queste tecniche sono utilizzate meno frequentemente rispetto alle scansioni **SYN stealth (-sS)** e **full-connect (-sT)** discusse in precedenza. Per un elenco completo di tutte le modalità di scansione disponibili, consulta la documentazione ufficiale di Nmap: https://nmap.org/book/scan-methods.html

---

## **Scansione delle porte**

Nmap si è evoluto nel corso degli anni. Inizialmente è stato progettato come uno scanner di porte efficiente, e questa rimane la sua funzione principale. Il comando semplice **`nmap <target>`** esegue la scansione delle 1.000 porte TCP sull'host . A differenza di altri scanner di porte, che considerano generalmente le porte come **aperte** o **chiuse**, Nmap fornisce una panoramica molto più dettagliata, classificando le porte in sei stati: **aperta**, **chiusa**, **filtrata**, **non filtrata**, **aperta|filtrata** e **chiusa|filtrata**.

Questi stati non sono proprietà intrinseche delle porte, ma descrivono come Nmap le vede. Ad esempio, una scansione da una rete locale del target potrebbe mostrare la porta **135/tcp** come aperta, mentre una scansione dalla stessa rete ma da un'altra posizione su Internet potrebbe mostrarla come filtrata.

### **I Sei Stati delle Porte**

- **Aperta (open)**  
    Una porta aperta è una porta su cui un'applicazione sta attivamente accettando connessioni TCP, datagrammi UDP o associazioni SCTP. Trovare porte aperte è spesso l'obiettivo principale della scansione delle porte. Le porte aperte sono viste come potenziali vie di accesso per gli attacchi, quindi sono di grande interesse per i penetration tester, che vogliono sfruttarle, e per gli amministratori, che cercano di proteggerle, spesso con firewall. Le porte aperte sono anche importanti nelle scansioni non legate alla sicurezza, poiché indicano i servizi disponibili sulla rete.
    
- **Chiusa (closed)**  
    Una porta chiusa è accessibile (risponde ai pacchetti sonda inviati da Nmap), ma non c'è alcuna applicazione in ascolto su di essa. Le porte chiuse sono utili per dimostrare che un host è attivo (scoperta dell'host o scansione ping), nonché per il rilevamento del sistema operativo. Poiché le porte chiuse sono raggiungibili, potrebbe essere utile eseguire una scansione successiva nel caso in cui queste si aprano. Gli amministratori potrebbero voler considerare di bloccarle con un firewall per evitare che vengano scansionate da attaccanti.
    
- **Filtrata (filtered)**  
    Una porta filtrata è una porta che non consente a Nmap di determinare se è aperta o chiusa, poiché il traffico in entrata viene bloccato da un firewall, una regola di router o un software firewall sul dispositivo. Le porte filtrate sono frustranti per gli attaccanti perché non forniscono alcuna informazione utile. In alcuni casi, possono rispondere con messaggi di errore ICMP, come "destinazione irraggiungibile" o "comunicazione proibita amministrativamente", ma più frequentemente non rispondono affatto, causando l'eliminazione dei pacchetti sonda. Questo rende più difficile per Nmap determinare lo stato della porta e rallenta notevolmente la scansione.
    
- **Non filtrata (unfiltered)**  
    Lo stato non filtrato indica che una porta è accessibile, ma Nmap non è in grado di determinare se sia aperta o chiusa. Solo il tipo di scansione **ACK** mappa le porte in questo stato. In altre scansioni, come il **SYN scan** o **FIN scan**, Nmap cerca di determinare se una porta è aperta o chiusa, ma nel caso delle porte non filtrate, non riesce a fare una valutazione chiara.
    
- **Aperta|Filtrata (open|filtered)**  
    Questo stato si verifica quando Nmap non riesce a determinare se una porta è aperta o filtrata. Ciò accade in scansioni in cui una porta aperta non risponde ai pacchetti inviati da Nmap. La mancata risposta potrebbe significare che un filtro di pacchetti ha bloccato la sonda, ma Nmap non è sicuro di quale sia la causa. Le scansioni **UDP**, **IP protocol**, **FIN**, **NULL** e **Xmas** spesso classificano le porte in questo stato.
    
- **Chiusa|Filtrata (closed|filtered)**  
    Questo stato si verifica quando Nmap non è in grado di determinare se una porta è chiusa o filtrata. È utilizzato esclusivamente dal **IP ID idle scan**. Questo stato è meno comune e si verifica solo in scenari avanzati di scansione.

Prendendo come esempio il caso precedente, possiamo osservare una porta aperta, una porta filtrata e 998 porte chiuse (si noti che Nmap per default scansiona le prime 1000 porte più comuni).

![[Pasted image 20250326162339.png]]

Questo significa che possiamo essere abbastanza certi che ci sia un servizio in esecuzione sulla porta 22. Inoltre, possiamo ipotizzare che la porta 3389 sia bloccata da un firewall, ma non possiamo sapere se un servizio stia effettivamente funzionando su quella porta, poiché dovrebbe essere raggiungibile per poterlo determinare. Infine, possiamo essere ragionevolmente sicuri che le restanti 998 porte non abbiano alcun servizio associato – la porta era aperta, ma non c'era nessuno a rispondere.

### **Specifica della porta (Port Specification)**:

Le seguenti opzioni possono essere utilizzate per mirare a porte specifiche durante la scansione con Nmap:

- **-p** : Specifica una o più porte da scansionare. Può essere una singola porta, un intervallo        (es. `sudo nmap -p 1-1024`), un elenco separato da virgole o una combinazione di questi.

	![[Pasted image 20250326163956.png]]
    
	Ad esempio, se stai cercando server web, eseguire il comando `nmap -p 80,443,8080,8443` è una buona scelta per scansionare le porte comunemente utilizzate per il traffico HTTP e HTTPS.

	**Nota**:  `-p-` è una  scorciatoia per specificare tutte le porte ed è equivalente a  `-p 1-65535`
    
- **--top-ports** : Seleziona le prime `<numero>` porte più comuni.

	![[Pasted image 20250326164020.png]]

	Se ti trovi di fronte a una rete molto grande e scansionare le 1000 porte predefinite su ogni indirizzo IP ti sembra eccessivo o lento, puoi far sapere a Nmap di concentrarsi su una selezione di porte di tuo interesse. Esegui `nmap --top-ports 50` per scansionare le 50 porte più comuni.
    
- **-F**: Velocità (abbreviazione per "top 100 porte").

	![[Pasted image 20250326164040.png]]
	
	Se pensi che scansionare le prime 100 porte sia sufficiente per determinare se un sistema è attivo nella tua gamma di indirizzi, ma non vuoi digitare `--top-ports 100`, Nmap ha pensato a te: l'opzione `-F` ti consente di eseguire la scansione delle prime 100 porte in modo rapido.


---

## **Scoperta degli host** 

Le seguenti opzioni possono essere utilizzate per controllare il rilevamento dell'host durante una scansione con Nmap:

- **-sn**: Disabilita la scansione delle porte, eseguendo esclusivamente la scoperta degli host. Questa opzione è utile quando vuoi semplicemente **verificare se un host esiste senza scansionare le sue porte**. Perfetta per una scansione mirata a identificare gli host attivi senza entrare nei dettagli dei servizi disponibili.

	![[Pasted image 20250326164701.png]]

	L'opzione `-reason` di `nmap` viene utilizzata per mostrare il motivo per cui una determinata porta o host è stato identificato come aperto, chiuso o filtrato durante la scansione. Ad esempio, se un host è stato identificato come "aperto", `nmap` ti dirà se l'host ha risposto a un pacchetto ICMP (ping), una richiesta TCP, un'analisi di porta o un altro tipo di test.

		Es. sudo nmap -sn --reason 192.168.0.0/24

- **-Pn**: Disabilita il rilevamento dell'host, trattando tutti gli host come se fossero online. In questo caso, **Nmap salta la fase di rilevamento e procede direttamente alla scansione delle porte**, anche se non ha conferma che l'host sia effettivamente raggiungibile. Questa opzione è utile se sospetti che un target stia bloccando i pacchetti di rilevamento dell'host di Nmap (come quelli ICMP) e vuoi comunque eseguire la scansione delle porte.

	![[Pasted image 20250326164728.png]]


---

## **Rilevamento dei Sistemi Operativi e dei Servizi**

Le seguenti opzioni possono essere utilizzate per rilevare i sistemi operativi e i servizi durante una scansione Nmap:

- **-O**: Rileva il sistema operativo in esecuzione sull'host.
	
	Se il sistema target corrisponde abbastanza da vicino a una delle impronte digitali di sistema operativo nel database di Nmap, verrà identificato e riportato. Se la corrispondenza non è precisa, è possibile forzare Nmap a fare una stima più aggressiva aggiungendo l'opzione        **--osscan-guess** per cercare di indovinare il sistema operativo.

	![[Pasted image 20250326170531.png]]

- **-sV**: Rileva il servizio di rete e la versione in esecuzione sulle porte aperte di un host.

	![[Pasted image 20250326170553.png]]

	Aggiungere l'opzione `-p <numero_porta>` per rilevare il software e la versione in esecuzione sulla porta specificata.
	
		Es. sudo nmap -sV 192.168.0.20 -p 21

	Questa opzione fornisce informazioni aggiuntive sul sistema operativo dell'host, ma il suo obiettivo principale è identificare i servizi vulnerabili (per eseguire patching o sfruttarli, a seconda del tuo ruolo).


---

## **Controllo della Velocità di Scansione**

Le seguenti opzioni possono essere utilizzate per controllare la velocità della scansione con Nmap:

- **Paranoid (T0)** 
- **Sneaky (T1)**
- **Polite (T2)**
- **Normal (T3)**
- **Aggressive (T4)**
- **Insane (T5)**.

![[Pasted image 20250326170858.png]]

Il valore predefinito è **Normal (T3)**. Puoi scegliere di accelerare la scansione se sei impaziente o rallentarla per evitare di attivare filtri che potrebbero alterare i risultati.

---