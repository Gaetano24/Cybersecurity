## **Cos'è Wireshark?**

**Wireshark è un potente strumento di analisi del traffico di rete**, noto anche come analizzatore di pacchetti o protocollo. Consente di intercettare e ispezionare i dati di rete per estrarre informazioni sulle comunicazioni tra dispositivi e analizzare il funzionamento dei protocolli di rete.

Per fare un'analogia, Wireshark è come una macchina a raggi X per le reti di computer: permette di vedere il traffico in transito e comprendere cosa accade a ogni livello del protocollo.

### **Comprendere i protocolli di rete**

I protocolli di rete sono le "lingue" della comunicazione tra dispositivi. Così come i linguaggi di programmazione (C, Java, Python) servono a scrivere software, i protocolli di rete (HTTP, IPv4, TCP) stabiliscono le regole per la trasmissione dei dati. Poiché la comunicazione in rete deve essere precisa e priva di ambiguità, i protocolli seguono regole ben definite e prevedibili.

### **Applicazioni pratiche di Wireshark**

Wireshark è utilizzato in diversi ambiti, tra cui:

- **Gestione di rete**: Diagnosi e risoluzione di problemi di prestazioni.
- **Sicurezza informatica**: Analisi di intrusioni e verifica delle misure di sicurezza.
- **Analisi forense**: Indagine su violazioni della sicurezza e infezioni da malware.
- **Penetration testing**: Ricerca di informazioni sensibili che potrebbero rappresentare vulnerabilità.

---

## **Interfaccia di Wireshark**

All'avvio, Wireshark mostra un elenco delle interfacce di rete disponibili per la cattura del traffico. Sono incluse interfacce Ethernet, Wi-Fi, Bluetooth e USB.

### **Filtri di acquisizione e visualizzazione**

Wireshark offre due tipi di filtri:

- **Filtro di acquisizione**: Registra solo i pacchetti che soddisfano determinati criteri.
- **Filtro di visualizzazione**: Mostra selettivamente pacchetti già catturati in base a specifiche condizioni.

Esempi di filtri utili:

- `http` - Mostrami tutto il traffico HTTP
- `ip.src == 192.168.0.1` - Mostrami i pacchetti inviati dall'indirizzo IP 192.168.0.1
- `ip.dst == 192.168.0.1` - Mostrami i pacchetti inviati all'indirizzo IP 192.168.0.1
- `ether.addr == 00:01:02:03:04:05` - Mostrami i pacchetti inviati all'indirizzo MAC 00:01:02:03:04:05
- `tcp.port == 22` - Mostrami i pacchetti inviati da o verso la porta TCP 22 (SSH)

Possiamo anche combinare questi filtri usando vari operatori logici:

- `http or dns` - Mostrami tutto il traffico che è HTTP o DNS
- `!(arp or icmp or dns)` - Escludere tutti i pacchetti che sono ARP, ICMP o DNS

Wireshark fornisce anche filtri stenografici per combinazioni comuni:

- `ip.addr == 192.168.0.1` - mostrami i pacchetti inviati al 192.168.0.1 o dal 192.168. Equivalente a ip.src == 192.168.0.1 or ip.dst == 192.168.0.1


![[Pasted image 20250325184652.png]]

### **La finestra principale di Wireshark**

Dopo l'avvio della cattura, Wireshark presenta tre riquadri principali:

1. **Elenco dei pacchetti**: Visualizza i pacchetti catturati in ordine cronologico, con dettagli come tipo di protocollo e indirizzi di origine e destinazione.
2. **Dettagli del pacchetto**: Fornisce una vista gerarchica del pacchetto selezionato, mostrando i protocolli incapsulati.
3. **Byte del pacchetto**: Mostra i dati grezzi del pacchetto in formato esadecimale e ASCII, utile per individuare informazioni sensibili nei dati in chiaro.    

![[Pasted image 20250325185700.png]]

Le informazioni evidenziate in un riquadro si sincronizzano automaticamente con gli altri per facilitare l'analisi.


---

