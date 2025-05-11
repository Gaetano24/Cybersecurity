## **Livello di Rete: Panoramica Generale**

Il **livello di rete** è responsabile dell'instradamento dei pacchetti da un host sorgente a uno di destinazione attraverso una o più reti.  

Funzioni principali:

- **Instradamento (Routing):** Determina il percorso migliore da sorgente a destinazione.
    
- **Forwarding:** Sposta i pacchetti dal collegamento input del router al collegamento output corretto.
    
- **Addressing:** Usa indirizzi IP per identificare univocamente host e reti.

Protocollo principale: **IP (Internet Protocol)**  
Altri protocolli: ICMP, OSPF, BGP, ARP (a cavallo tra livelli)


![[Pasted image 20250509195055.png]]

---

## **Control Plane vs Data Plane**

### **Data Plane (Piano dati)**

Si occupa dell'effettiva **trasmissione dei pacchetti**. Opera in modo locale su ogni router.

- Esegue il **forwarding** dei pacchetti in base alla tabella di instradamento.    
- Esempio: il **router inoltra** un pacchetto verso la porta output scelta.

![[Pasted image 20250509195127.png]]


### **Control Plane (Piano di controllo)**  

Si occupa del **calcolo e della gestione dei percorsi**.

- Utilizza **protocolli di routing** (come OSPF, BGP) per costruire le tabelle di instradamento.
- È responsabile della **logica di decisione** sui percorsi.

Si distinguono due approcci: 

- **Algoritmi router tradizionali**: implementati nei router
- **Software-defined Networking (SDN)**: implementato in server remoti

---

## **Per-router Control Plane vs SDN (Software-Defined Networking)**

### **Per-router control plane:**

Un algoritmo di routing distribuito viene eseguito in tutti i router di rete. In particolare, la funzione dell'algoritmo di routing in un router comunica con le funzioni dell'algoritmo di routing in altri router per calcolare i valori in queste tabelle di inoltro.

Caratteristiche:

- Architettura **distribuita**, più resistente a guasti.    
- Complessa da gestire su larga scala.    

![[Pasted image 20250509195309.png]]


### **SDN (Software Defined Networking):**

Un processo software di un controller remoto calcola e distribuisce la tabelle di routing utilizzate da ciascun router. I controller remoti sono in genere implementati in un data center remoto o in un set di server che hanno che hanno elevata affidabilità e ridondanza.

Caratteristiche:

- **Separazione netta** tra control plane e data plane.       
- Il control plane è **centralizzato** in un controller SDN.
- I router (switch) diventano dispositivi che seguono le istruzioni del controller.
- Vantaggi: flessibilità, programmabilità, visione globale della rete.

![[Pasted image 20250509195423.png]]


---

## **Network Service Model: Best Effort**

Internet adotta un modello di servizio detto **Best Effort**:

- Nessuna garanzia di consegna, ordine, o ritardo.
- La rete **fa del suo meglio** per consegnare i pacchetti.
- Non c'è controllo integrato di **affidabilità o qualità del servizio (QoS)**.

Conseguenze:

- I pacchetti possono essere **persi, duplicati o ritardati**.
- Sono necessari meccanismi **a livello superiore** (es. TCP) per garantire affidabilità.

---
