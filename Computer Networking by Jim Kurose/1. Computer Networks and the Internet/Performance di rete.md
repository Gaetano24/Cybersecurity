
### **Perdita e ritardi dei pacchetti**

Prima della trasmissione sul canale di comunicazione, i pacchetti in ingresso vengono accodati nel buffer del router. La lunghezza della coda nel buffer aumenta all'arrivo di ciascun pacchetto. L'inoltro dei pacchetti avviene secondo una politica di scheduling FIFO (First-In, First-Out), per cui ogni pacchetto deve attendere che vengano trasmessi quelli arrivati in precedenza. In condizioni di congestione, il buffer può raggiungere la sua capacità massima; in tal caso, i pacchetti in arrivo non possono essere memorizzati e vengono scartati, comportando una perdita di pacchetti (**packet loss**).

![[Pasted image 20250416090414.png]]

**Schema generale sui ritardi**:

![[Pasted image 20250416090550.png]]

![[Pasted image 20250416090751.png]]

![[Pasted image 20250416090817.png]]

---

### **Traceroute**

**Traceroute** è uno strumento diagnostico di rete utilizzato per tracciare il percorso che un pacchetto IP compie da un host sorgente a un host di destinazione, mostrando tutti i router intermedi (hop) attraversati lungo il cammino.

#### Come funziona?

**Traceroute** sfrutta il campo **Time To Live (TTL)** presente nell’intestazione dei pacchetti IP per determinare il percorso seguito dai pacchetti verso una destinazione. A ogni passo, invia pacchetti con un valore TTL incrementale a partire da 1. Ogni router lungo il percorso decrementa il TTL di 1; quando il TTL raggiunge zero, il router scarta il pacchetto e invia un messaggio di errore ICMP "Time Exceeded" al mittente. Analizzando questi messaggi ICMP, traceroute identifica l’indirizzo IP (e spesso il nome DNS) di ogni router attraversato.

Per ogni hop, traceroute invia tipicamente tre pacchetti e misura il tempo di risposta (RTT - Round Trip Time) per ciascuno, fornendo una stima della latenza verso ogni nodo intermedio.

![[Pasted image 20250416091323.png]]

![[Pasted image 20250416091514.png]]

---

### **Throughput**

Il **throughput** è la quantità di dati trasmessi attraverso un canale di comunicazione in un determinato intervallo di tempo. Viene generalmente espresso in **bit per secondo (bps)** o in suoi multipli (**Kbps**, **Mbps**, **Gbps**).

Distinguiamo:

- **Throughput istantaneo**: misura la **velocità di trasferimento dei dati in un intervallo di tempo molto breve** (quasi "in tempo reale"). Varia rapidamente nel tempo ed è utile per analizzare fluttuazioni o picchi di traffico.

- **Throughput medio**: calcola la **media della velocità di trasferimento su un intervallo di tempo più ampio**, offrendo una visione complessiva e più stabile delle prestazioni della rete.

![[Pasted image 20250416092552.png]]

Di seguito due possibili scenari:

![[Pasted image 20250416092635.png]]


#### Scenario di rete

![[Pasted image 20250416092812.png]]