## **Introduzione e contesto**

Il trasferimento affidabile dei dati è una sfida fondamentale nelle reti di computer. In un mondo ideale, i pacchetti viaggerebbero sempre intatti dal mittente al destinatario, ma nella realtà devono affrontare:

- Errori di trasmissione (bit flip)
- Perdite di pacchetti
- Duplicazioni
- Ritardi variabili

Per garantire affidabilità, i protocolli RDT (Reliable Data Transfer) utilizzano meccanismi complessi come:

- Macchine a stati finiti (FSM) per modellare il comportamento del mittente e del ricevitore
- Meccanismi di conferma (ACK) e negazione (NAK)
- Temporizzatori per gestire le perdite
- Numeri di sequenza per evitare duplicati

---

## **Evoluzione dei protocolli RDT**

### **RDT 1.0 – Canale perfetto**

Il protocollo RDT 1.0 è il modello più semplice e si assume che il canale sia perfetto, senza errori o perdite. Non sono previsti controlli sul flusso dei dati, né meccanismi di gestione degli errori.

**Comportamento**:

- Il mittente invia un pacchetto senza alcuna conferma dal ricevitore.
- Nessun controllo di errore o ritrasmissione.
- Il ricevitore non invia alcun feedback.

**Limiti**:

- Completamente inadeguato per reti reali, dove errori e perdite sono inevitabili.
- Serve solo come punto di partenza teorico, non applicabile a situazioni pratiche.


### **RDT 2.0 – Introduzione del controllo errori**

Il protocollo RDT 2.0 migliora il precedente introducendo meccanismi di rilevamento degli errori e feedback esplicito tramite ACK (Acknowledge) e NAK (Negative Acknowledge). Viene utilizzato un **checksum** per verificare l'integrità dei pacchetti.

**Comportamento**:

- Il mittente invia il pacchetto e aspetta una conferma dal ricevitore (ACK) o una negazione (NAK).
- Se il pacchetto è errato, il ricevitore invia un NAK e il mittente ritrasmette il pacchetto.
- Se l'ACK o il NAK stesso è corrotto, il mittente rimane in un stato di incertezza.

**Problemi**:

- La corruzione di ACK o NAK può portare a incertezze nel comportamento del mittente, rischiando duplicazioni di pacchetti.


### **RDT 2.1 – Gestione delle ambiguità**

RDT 2.1 affronta il problema delle ambiguità causate dalla corruzione di ACK e NAK introducendo numeri di sequenza. Il mittente e il ricevitore utilizzano numeri di sequenza per ogni pacchetto, permettendo di distinguere tra pacchetti duplicati e pacchetti nuovi.

**Comportamento**:

- Vengono usati numeri di sequenza (0 e 1) per identificare univocamente i pacchetti.
- Il ricevitore può rilevare i pacchetti duplicati e ignorarli, riducendo il rischio di duplicazioni.
- Migliorata la robustezza contro la corruzione di ACK o NAK

**Vantaggi**:

- Introduzione dei numeri di sequenza rende possibile il trattamento delle duplicazioni.
- Permette al mittente di avere maggiore certezza sullo stato della trasmissione.


### **RDT 2.2 – Ottimizzazione del protocollo**

RDT 2.2 è un'ulteriore evoluzione che ottimizza il protocollo, eliminando il NAK e semplificando la logica del protocollo. Utilizza solo gli ACK per la gestione degli errori.

**Comportamento**:

- Eliminazione del NAK: se un pacchetto viene corrotto, il ricevitore invia un ACK per il pacchetto precedente, il che permette al mittente di ritrasmettere solo il pacchetto corrotto.
- Uso degli ACK duplicati per migliorare l'affidabilità del trasferimento.

**Vantaggi**:

- Riduzione della complessità del protocollo.
- Semplificazione della gestione degli errori, riducendo il numero di messaggi necessari.


### **RDT 3.0 – Gestione delle perdite**

RDT 3.0 affronta il problema delle perdite di pacchetti e introduce il **timeout** come meccanismo per la ritrasmissione automatica in caso di mancata ricezione di un ACK. Questo protocollo è completo e risolve le principali problematiche di affidabilità in una rete imperfetta.

**Comportamento**:

- Il mittente invia un pacchetto e attende un ACK. Se non arriva entro un certo tempo (timeout), il pacchetto viene ritrasmesso.
- Gestione delle perdite di pacchetti tramite ritrasmissione.
- Introduzione del timer, che consente di rilevare e reagire alle perdite.

**Vantaggi**:

- Gestione completa di errori, duplicati e perdite.
- È in grado di operare anche su canali non perfetti, come quelli delle reti reali.

---

## **Tecniche avanzate: Pipelining**

### **Go-Back-N (GBN)**

Il Go-Back-N è una tecnica di **pipelining** che permette di inviare più pacchetti prima di ricevere un ACK, migliorando l'efficienza del trasferimento. Tuttavia, se un pacchetto viene perso o corrotto, l'intero blocco di pacchetti successivi deve essere ritrasmesso.

**Comportamento**:

- Finestra di **N pacchetti** in transito.
- Il ricevitore invia un ACK cumulativo per il pacchetto più recente ricevuto correttamente.
- In caso di errore, tutti i pacchetti successivi devono essere ritrasmessi (approccio di ritrasmissione massiva).

**Vantaggi**:

- Semplice da implementare.
- Basso overhead quando gli errori sono rari.

**Svantaggi**:

- Inefficiente in ambienti con errori frequenti o alta latenza, poiché l’intera finestra deve essere ritrasmessa anche per un solo errore.


![[Pasted image 20250507220802.png]]


### **Selective Repeat (SR)**

Selective Repeat è una variante più sofisticata del Go-Back-N, in cui solo i pacchetti che sono stati effettivamente persi o corrotti vengono ritrasmessi. Questa tecnica è più efficiente, soprattutto in reti con errori frequenti.

**Comportamento**:

- Finestra di **N pacchetti** in transito.
- Ogni pacchetto ha un suo ACK individuale.
- Solo i pacchetti persi o corrotti vengono ritrasmessi.

**Vantaggi**:

- Massima efficienza, poiché solo i pacchetti errati vengono ritrasmessi.
- Riduzione dello spreco di banda rispetto al Go-Back-N.

**Svantaggi**:

- Maggiore complessità implementativa.
- Necessità di buffer più grandi e gestione complessa della finestra.


![[Pasted image 20250507220624.png]]

---
