## **Introduzione a TCP**

TCP (Transmission Control Protocol) è un **protocollo di trasporto connection-oriented** che fornisce una comunicazione affidabile, ordinata e full-duplex tra due sistemi. Viene utilizzato in una vasta gamma di applicazioni, come il trasferimento di file (FTP), la navigazione web (HTTP) e le comunicazioni via email (SMTP), grazie alla sua capacità di garantire la consegna dei dati in modo sicuro ed efficiente.

TCP si basa su una serie di meccanismi fondamentali per gestire **l'affidabilità** e il **controllo del flusso e della congestione**, consentendo una trasmissione dei dati che rispetta i requisiti di performance anche in ambienti di rete non ideali.

---

## **Caratteristiche fondamentali di TCP**

### **Affidabilità**

TCP garantisce la **consegna affidabile e ordinata dei dati**, che significa che i pacchetti arrivano correttamente, nel giusto ordine e senza duplicazioni. Le caratteristiche che assicurano questo comportamento sono:

- **Numeri di sequenza e ACK cumulativi**: Ogni byte trasmesso ha un numero di sequenza unico che consente al destinatario di ordinare correttamente i pacchetti. Il destinatario invia anche un ACK cumulativo, indicando l'ultimo byte correttamente ricevuto.

- **Ritrasmissione dei segmenti persi**: Se il mittente non riceve un ACK per un pacchetto entro un certo periodo (timeout), ritrasmette il pacchetto. In questo modo, TCP gestisce la perdita di pacchetti.

- **Rilevazione e eliminazione dei duplicati**: TCP riconosce e scarta i pacchetti duplicati grazie all'uso dei numeri di sequenza, evitando che dati identici vengano elaborati più di una volta.


### **Controllo del flusso**

TCP implementa meccanismi per **regolare la velocità di trasmissione** in modo da evitare che il ricevitore venga sopraffatto dai dati che arrivano troppo velocemente:

- **Finestra scorrevole (sliding window)**: Ogni lato della connessione TCP mantiene una finestra di dimensione variabile che determina quanti byte possono essere inviati prima che venga ricevuta una conferma (ACK). La finestra scorrevole aiuta a mantenere il flusso di dati ottimale senza sovraccaricare il ricevitore.

- **Meccanismo di advertisement (rwnd)**: Il ricevitore comunica al mittente la quantità di spazio disponibile nel suo buffer, usando il campo "rwnd" nell'header TCP. Questo permette al mittente di sapere quanta capacità ha il ricevitore prima di inviare ulteriori dati.


### **Controllo della congestione**

TCP gestisce la **congestione della rete**, evitando che la trasmissione di troppi pacchetti contemporaneamente causi rallentamenti o perdite di pacchetti:

- **Algoritmi AIMD (Additive Increase Multiplicative Decrease)**: TCP aumenta la finestra di congestionamento in modo additivo quando la rete non è congestionata, ma la riduce in modo moltiplicativo in caso di congestione (per esempio, quando vengono rilevati pacchetti persi).

- **Slow start**: All'inizio della connessione, TCP aumenta rapidamente la dimensione della finestra di congestionamento, ma solo fino a un certo punto, per evitare un eccessivo carico sulla rete.

- **Fast retransmit/recovery**: Se il mittente riceve tre duplicati di un ACK, capisce che un pacchetto è stato perso e lo ritrasmette senza attendere il timeout. Questo riduce significativamente i ritardi nelle situazioni di congestione.

---

## **Struttura del segmento TCP**

Un **segmento TCP** è il dato che viene effettivamente trasmesso tra i due host e include una serie di campi nell'header che definiscono informazioni cruciali per la gestione della connessione. Di seguito viene descritta la struttura dell'header di un segmento TCP:

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Acknowledgment Number                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Data |           |U|A|P|R|S|F|                               |
| Offset| Reserved  |R|C|S|S|Y|I|            Window             |
|       |           |G|K|H|T|N|N|                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |         Urgent Pointer        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             Data                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

**Descrizione dei campi principali**:

- **Source Port e Destination Port**: Specificano i numeri di porta sorgente e di destinazione, che identificano i processi in esecuzione sui due host.
    
- **Sequence Number**: Indica il numero di sequenza del primo byte del segmento. È utile per l'ordinamento dei dati e la gestione dei pacchetti.
    
- **Acknowledgment Number**: Indica il prossimo byte che il ricevitore si aspetta di ricevere, confermando così l'ordinato arrivo dei dati.
    
- **Data Offset**: Indica la lunghezza dell'header TCP (in unità di 32 bit).
    
- **Flags (U, A, P, R, S, F, R, C, S, S, Y, I)**: Ogni bit di flag ha una funzione specifica, come l'inizio di una connessione (SYN), la chiusura (FIN) o il controllo del flusso.
    
- **Window**: Mostra la dimensione della finestra di ricezione disponibile, cioè lo spazio nel buffer del ricevitore.
    
- **Checksum**: Utilizzato per verificare l'integrità del segmento.
    
- **Urgent Pointer**: Indica se il segmento contiene dati urgenti.
    
- **Options e Padding**: I campi opzionali che forniscono funzionalità aggiuntive, con eventuale padding per allineare l'header.


![[Pasted image 20250507222111.png]]

---

## **Numeri di sequenza e ACK**

- **Sequence Number**: Ogni byte trasmesso da TCP è contrassegnato da un numero di sequenza. Questo numero è cruciale per mantenere l'ordine corretto dei pacchetti e per gestire eventuali pacchetti persi.

- **ACK Number**: L'ACK (Acknowledge) è un numero che rappresenta il byte successivo che il ricevitore si aspetta di ricevere. In altre parole, se il ricevitore invia un ACK con un numero 1000, significa che ha ricevuto tutti i byte fino al byte 999 e si aspetta il byte 1000 come prossimo.


![[Pasted image 20250507222145.png]]

---

## **Gestione della connessione**

TCP gestisce la connessione attraverso un processo chiamato **Three-Way Handshake**, che serve a stabilire una connessione tra il client e il server. Il processo si svolge in tre fasi:

1. **SYN** (Client → Server): Il client invia un segmento con il flag SYN attivo per iniziare una connessione.
    
2. **SYN-ACK** (Server → Client): Il server risponde con un segmento che ha sia il flag SYN che ACK attivi, confermando la ricezione del primo pacchetto.
    
3. **ACK** (Client → Server): Il client invia un pacchetto con il flag ACK attivo per confermare l'avvenuta ricezione del segmento del server.

![[Pasted image 20250507222757.png]]

La chiusura di una connessione TCP avviene in modo molto simile all’handshake di apertura, con l’uso del flag **FIN** al posto di **SYN**. In pratica si ha quindi l’invio di un **FIN** da parte dell’host che vuole chiudere la connessione, seguito in risposta da un **FIN+ACK** e poi di nuovo **ACK**. Esiste anche la possibilità di chiudere la connessione in modo più brusco semplicemente smettendo di inviare e ricevere dati e inviando un segmento con il flag **RST** (reset).

![[Pasted image 20250507223031.png]]

---
