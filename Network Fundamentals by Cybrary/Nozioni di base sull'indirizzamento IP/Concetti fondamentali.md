## **Il modello di rete TCP/IP**

TCP/IP è una suite di protocolli di rete che regolano il modo in cui i dati vengono trasmessi, instradati e ricevuti tra i dispositivi su una rete. TCP/IP è organizzato in quattro aree distinte, ognuna con funzioni specifiche:

![[Pasted image 20250321102205.png]]

Insieme, i protocolli TCP/IP consentono di suddividere i dati in pacchetti, instradarli attraverso le reti e garantirne la consegna affidabile e Il ri-assemblaggio corretto. La flessibilità e la scalabilità di questa suite hanno contribuito alla sua ampia diffusione, rendendola la spina dorsale dell'Internet moderno.


## **Transmission Control Protocol (TCP)**

Il Transmission Control Protocol (TCP) fornisce una comunicazione affidabile e orientata alla connessione. Stabilisce un canale di comunicazione tra due dispositivi, consentendo il trasferimento dei dati e garantendo che vengano inviati e ricevuti correttamente, senza errori. TCP utilizza i numeri di porta per distinguere i servizi in esecuzione sullo stesso dispositivo. Ad esempio, la porta 80 è generalmente associata al traffico HTTP (web), mentre la porta 25 è utilizzata per il traffico SMTP (email).

Di seguito è riportato un elenco delle porte TCP più comuni:

![[Pasted image 20250321102618.png]]

**Nota**: UDP sta per User Datagram Protocol. Offre una comunicazione più veloce e senza connessione, ma non garantisce lo stesso livello di affidabilità e correzione degli errori di TCP.


## **Internet Protocol**

Il **protocollo Internet (IP)** è responsabile dell’**instradamento dei pacchetti** di dati dalla sorgente alla destinazione attraverso le reti che utilizzano router. Un **router** è un dispositivo specializzato che **inoltra i pacchetti tra reti diverse** utilizzando gli indirizzi IP.

Attualmente, esistono due versioni principali degli indirizzi IP. L’Internet Protocol **versione 4 (IPv4)** è il più diffuso e utilizza un **indirizzo a 32 bit**, suddiviso in quattro **ottetti**, accompagnato da una **maschera di sottorete**. Il più recente Internet Protocol **versione 6 (IPv6)** utilizza invece **indirizzi a 128 bit**, progettati per supportare l’espansione del numero di dispositivi connessi a Internet.

In questo laboratorio, ci concentreremo sugli indirizzi IPv4. Come accennato, un indirizzo IPv4 è composto da quattro ottetti, ciascuno con un valore compreso tra 0 e 255.

La **maschera di sottorete** ha il compito di **distinguere quali parti dell’indirizzo identificano la rete e quali identificano l’host**. Esaminiamo un esempio per comprenderlo meglio:

![[Pasted image 20250321103411.png]]

Nell'esempio sopra, 192.168.10.100 è l'indirizzo IP e 255.255.255.0 è la maschera di sottorete. Un 255 nella maschera di sottorete indica che l'ottetto fa parte della rete, mentre uno 0 (zero) indica che l'ottetto rappresenta l'host. I primi tre ottetti (192.168.10) sono la rete e il quarto ottetto (.100) è l'host. Quindi questo esempio mostra l'host 100 sulla rete 192.168.10.0.

Gli **host sulla stessa rete possono parlarsi direttamente utilizzando ARP** (vedi sotto), mentre gli **host su un'altra rete devono ricevere messaggi inoltrati utilizzando un router**. Nell'esempio seguente, il primo e il secondo host mostrati condividono la stessa rete (192.168.10) e quindi possono raggiungersi senza router. Tuttavia, il terzo host non utilizza la stessa rete (192.168.11) e richiederà un router per comunicare con i primi due.

![[Pasted image 20250321104138.png]]

**Nota**: È comune vedere 255.255.255.0 scritto come /24. Ciò significa che **192.168.10.100/24 è lo stesso di 192.168.10.100 255.255.255.0**.


## **Instradamento e sottoreti**

Per questo laboratorio, è sufficiente comprendere che un indirizzo IP è composto da due parti: la rete e l'host. Solo gli host appartenenti alla stessa rete possono comunicare direttamente tra loro senza bisogno di un router.

Nell’esempio seguente, l’indirizzo **192.168.10.10** può comunicare direttamente con **192.168.10.20**, poiché entrambi si trovano sulla stessa rete. Tuttavia, per comunicare con **192.168.11.10** o **192.168.11.20**, avrà bisogno di un router situato all’indirizzo **192.168.10.1** (chiamato **gateway**).

È importante notare che il router possiede due indirizzi IP, uno per ciascuna rete a cui è collegato. Inoltre, i router non devono necessariamente far parte di una rete specifica per poter instradare il traffico. Possono utilizzare il proprio gateway per inoltrare pacchetti al di fuori delle reti locali, ad esempio verso Internet.

![[Pasted image 20250321104437.png]]


## **Media Access Control (MAC) e Address Resolution Protocol (ARP)**

Quando un dispositivo all'interno di un segmento di rete locale desidera comunicare con un altro dispositivo nello stesso segmento, deve conoscere il **MAC address** (_Media Access Control_) del destinatario. L'**indirizzo MAC** è un **identificativo univoco a 12 cifre esadecimali assegnato a ogni scheda di rete all'interno di una rete locale**.

Per associare un indirizzo IP a un indirizzo MAC, si utilizza il **protocollo ARP** (_Address Resolution Protocol_), che funziona nel seguente modo:

1. Un host trasmette una **richiesta ARP** (in broadcast) sulla rete locale per scoprire l'indirizzo MAC corrispondente a un determinato indirizzo IP.
2. Il dispositivo con l’indirizzo IP richiesto riconosce la richiesta e invia una **risposta ARP** contenente il proprio indirizzo MAC.
3. Dopo aver ricevuto la risposta, l’host memorizza la corrispondenza tra **indirizzo IP e MAC** nella sua **cache ARP** per evitare richieste ripetute.
 
 **Nota**: 
 La **cache ARP** aiuta a ridurre il traffico di rete evitando richieste ARP ripetitive per lo stesso IP. Tuttavia, le voci nella cache hanno un **time-out** e, una volta scadute, devono essere aggiornate. Ora che l’indirizzo MAC del destinatario è noto, il dispositivo mittente può **incapsulare** i pacchetti IP all'interno di **frame Ethernet** e inviarli al destinatario utilizzando il suo indirizzo MAC.