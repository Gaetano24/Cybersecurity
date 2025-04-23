
La sezione **Statistics** di Wireshark è fondamentale per ottenere una visione sintetica, dettagliata e spesso immediata di quanto catturato durante un’analisi. In particolare, la modalità **Conversations** mi permette di visualizzare le comunicazioni presenti nel file di cattura per livello di indirizzo .

---
## **Ethernet**

![[Pasted image 20250408141339.png]]

**Commento**: A livello 2 ho solo una conversazione tra due indirizzi MAC.

---

## **IPv4**

![[Pasted image 20250408141757.png]]

**Commento**: prestiamo particolare attenzione alle colonne **Rel Start** e **Duration**:	

- **Rel Start**: indica il momento in cui ha avuto inizio la conversazione, misurato rispetto all’inizio della cattura.    
- **Duration**: rappresenta la durata complessiva della conversazione.

Dall’analisi iniziale si può osservare che un singolo host (10.0.2.15) sta tentando di esplorare diversi indirizzi IP all’interno della sottorete 192.168.0.0. Approfondiremo questo comportamento nella sezione dedicata al protocollo **TCP**.


#### **Come individuare un trasferimento lento o un grande scambio di dati**

Nel caso volessimo tracciare un trasferimento di file lento o il passaggio di un volume elevato di dati, possiamo ordinare le conversazioni in base alla colonna **Bytes**, in ordine crescente o decrescente.

Facendo tasto destro su una specifica conversazione, possiamo eseguire:

> [!NOTE]
> 	Apply as Filter > Selected > A <-> B

![[Pasted image 20250408190939.png]]

In questo modo **Wireshark** mostrerà esclusivamente il traffico bidirezionale tra i due endpoint selezionati, facilitando l’analisi dettagliata dello scambio dati.	

![[Pasted image 20250408190848.png]]

---

## **TCP**

![[Pasted image 20250408141606.png]]

**Commento**: Dalla panoramica emerge un dato significativo: sono presenti ben **17.476 conversazioni**, un numero decisamente elevato. Inoltre, si osserva che ciascuna conversazione contiene **solamente da 1 a 3 pacchetti**.

Questa caratteristica suggerisce chiaramente un comportamento riconducibile a un **port scanning**. In particolare, lo scanning sembra indirizzarsi prima verso una specifica porta (nell’esempio mostrato, la porta 1), per poi passare a un’altra (ad esempio la porta 3), ripetendo il processo su tutti gli indirizzi IP della sottorete.

È interessante notare che le **porte non vengono scansionate in modo sequenziale**: dalla porta 1 si salta direttamente alla porta 3, saltando quindi la 2. Questo comportamento può essere interpretato come un tentativo da parte dell’attaccante di **eludere eventuali sistemi di rilevamento**, utilizzando una scansione più discreta e meno prevedibile.

---

## **Approfondimento**

### **1. Sommario della Cattura ("Summary")**

- **Cos'è:** È una finestra di riepilogo che si apre subito dopo la cattura o che può essere consultata in seguito.
    
- **Cosa mostra:**

    - Tempo totale della cattura        
    - Numero di pacchetti registrati
    - Velocità di trasmissione media
    - Informazioni sui protocolli utilizzati
    - Dimensione complessiva dei dati catturati

- **Perché è utile:** Fornisce un primo quadro della sessione di monitoraggio, evidenziando ad esempio se ci sono picchi di traffico o anomalie nel flusso di dati.    

---

### **2. Gerarchia dei Protocolli ("Protocol Hierarchy")**

- **Cos'è:** Una rappresentazione ad albero che suddivide il traffico in base ai protocolli.
    
- **Cosa mostra:**
    
    - La percentuale di pacchetti e byte relativi ad ogni protocollo (ad esempio Ethernet, IP, TCP, UDP, etc.)    
    - Sottolivelli, permettendo di vedere le dipendenze tra protocolli (come HTTP sopra TCP sopra IP)

- **Utilizzo pratico:**
    
    - Comprendere il mix dei protocolli in rete
	- Identificare protocolli anomali o inaspettati in un contesto specifico

---

### **3. Conversazioni ("Conversations")**

- **Cos'è:** Un report che raggruppa i pacchetti in "conversazioni" o flussi di comunicazione tra due endpoint.
    
- **Cosa mostra:**
    
    - Indirizzi IP e porte delle entità coinvolte
    - Numero di pacchetti scambiati, byte trasferiti e durata della comunicazione        
    - Eventuali errori o problemi di trasmissione

- **Applicazioni pratiche:**
    
    - Analizzare la comunicazione tra due dispositivi
    - Identificare eventuali colli di bottiglia o anomalie nella comunicazione bidirezionale

---

### **4. Endpoint**

- **Cos'è:** Un report che elenca tutti gli endpoint (IP, MAC o altri identificatori) presenti nella cattura.
    
- **Cosa mostra:**
    
    - Numero di pacchetti inviati e ricevuti da ciascun endpoint
    - Quantità di dati trasferiti
    - Eventuali malfunzionamenti o comportamenti sospetti

- **Utilizzo pratico:**
    
    - Identificare dispositivi che generano traffico anomalo        
    - Analizzare il comportamento di specifici host in rete


---

### **5. Grafici I/O ("I/O Graphs")**

- **Cos'è:** Una funzionalità grafica che permette di visualizzare il traffico nel tempo.
    
- **Cosa mostra:**
    
    - Andamento dei pacchetti e dei byte durante la cattura in forma di grafico
    - Possibilità di confrontare traffico di diversi protocolli o flussi simultanei

- **Applicazioni:**
    
    - Rilevare picchi di traffico e correlare eventi di rete     
    - Monitorare, in tempo reale o in post-analisi, le performance della rete

---

### **6. Grafici di Flusso ("Flow Graph")**

- **Cos'è:** Rappresenta graficamente le sequenze di scambi tra i vari dispositivi partecipanti alla comunicazione.
    
- **Cosa mostra:**
    
    - Sequenza cronologica delle comunicazioni
    - Relazione tra richieste e risposte, mostrando come si sviluppa una sessione di comunicazione

- **Utilità pratica:**
    
    - Debug di protocolli e identificazione di ritardi o interruzioni nel flusso di dati        
    - Visualizzazione chiara e immediata di interazioni complesse

---

### **7. Altri Strumenti Statistici**

Wireshark offre anche altre funzionalità statistiche e filtri che possono essere personalizzati per approfondire l'analisi in funzione di specifici scenari:

- **Endpoint Specifici e filtri personalizzati:** Permettono di isolare il traffico verso/dal dispositivo di interesse e analizzarlo in dettaglio.

- **Statistiche sui pacchetti:** Permettono di aggregare dati sui tipi di pacchetti e sugli errori riscontrati, facilitando la diagnosi di problemi specifici. 

---
