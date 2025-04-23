## **Introduzione ai modelli di rete**
 
I **modelli di riferimento OSI e TCP/IP** sono schemi concettuali che **descrivono il funzionamento delle reti**, rappresentando in modo astratto il flusso dei dati attraverso diversi livelli. Ogni modello è suddiviso in una **serie di strati sovrapposti**, chiamata "**stack**", in cui ogni livello si basa su quello sottostante per svolgere le proprie funzioni. Lo stack segue una direzione ben precisa: **si scende verso i livelli inferiori durante l'invio dei dati e si risale durante la ricezione**.

Alla base dello stack troviamo i segnali elettrici, i bit e i simboli – gli elementi fondamentali dell'elettronica moderna. In cima, invece, ci sono le interfacce utente, come le immagini e il testo visualizzati nei browser e nei client di posta elettronica.

Quando i dati vengono inviati, attraversano lo stack subendo un processo chiamato **incapsulamento**: ogni livello aggiunge informazioni sotto forma di intestazioni o trailer (dettagli inseriti rispettivamente all'inizio o alla fine dei dati), che verranno poi interpretate dal destinatario. Una volta ricevuti, i dati risalgono lo stack attraverso la fase di **decapsulamento**, in cui ogni livello rimuove le informazioni aggiuntive fino a restituire il contenuto originale.

Il modello OSI è composto da 7 livelli, mentre il modello TCP/IP ne ha 4. Tuttavia, comprendendone uno, risulta più facile assimilare anche l'altro, poiché condividono principi simili. Non si tratta di un semplice esercizio di memorizzazione, ma di un sistema logico e strutturato che, una volta compreso, rende il mondo delle reti molto più chiaro e accessibile.

---

## **Il Modello OSI

Il **modello OSI**, sviluppato dall'ISO negli anni '70, è stato creato per standardizzare i protocolli di rete, favorire l'interoperabilità tra sistemi di diversi fornitori e fornire una visione comune delle reti. Inizialmente, le reti erano dominate da standard proprietari, limitando la compatibilità tra dispositivi.

Il modello OSI è suddiviso in **7 livelli**:

- **I 4 livelli inferiori** ("media") gestiscono indirizzamento, trasporto e consegna dei dati.
- **I 3 livelli superiori** ("host") si basano su questa infrastruttura per garantire la comunicazione tra applicazioni.

L'OSI fornisce così una struttura universale per descrivere le interazioni tra i protocolli di rete.


![[Pasted image 20250319192337.png]]

Riepilogo dei 7 livelli:

- **Livello Fisico (1)** – Gestisce la trasmissione dei dati attraverso il mezzo fisico (cavi, segnali elettrici, onde radio).
- **Livello Data Link (2)** – Si occupa della comunicazione tra dispositivi all'interno di una rete locale, utilizzando indirizzi MAC e switch per inoltrare i frame.
- **Livello Rete (3)** – Gestisce l'instradamento dei dati tra reti diverse tramite indirizzi IP e router.
- **Livello Trasporto (4)** – Garantisce la consegna dei dati tra host, utilizzando protocolli come TCP (affidabile, ma più lento) e UDP (veloce, ma senza controllo degli errori).
- **Livello Sessione (5)** – Controlla l'avvio, la gestione e la chiusura delle sessioni di comunicazione tra dispositivi, gestendo autenticazione e autorizzazione.
- **Livello Presentazione (6)** – Si occupa della formattazione dei dati (compressione, crittografia, codifica) per renderli comprensibili al livello superiore.
- **Livello Applicazione (7)** – Interfaccia tra utente e rete, gestisce servizi come browser web, client di posta e altre applicazioni.

![[Pasted image 20250319193422.png]]


**Osservazioni su alcuni dispositivi di rete**:

- **Switch di livello 2 e 3**: tradizionalmente, gli switch operano a **livello 2** (collegando dispositivi in una rete locale tramite indirizzi MAC). Tuttavia, con l'introduzione di VLAN e funzionalità di routing, alcuni switch operano anche a **livello 3**, gestendo pacchetti IP e funzioni tipiche dei router.

- **Evoluzione dei firewall**:

	Inizialmente, i firewall operavano a **livello 3** del modello OSI, filtrando il traffico in base agli indirizzi IP. Questi firewall, detti **stateless**, esaminavano i pacchetti in transito senza tenere traccia dello stato delle connessioni, rendendoli vulnerabili a diversi tipi di attacchi.

	Con l'aumento delle minacce informatiche, sono stati introdotti i **firewall di livello 4**, capaci di monitorare le connessioni TCP. Questi firewall, definiti **stateful**, analizzano informazioni come porte di origine e destinazione, mantenendo lo stato delle sessioni attive. Questo miglioramento ha permesso una protezione più efficace contro attacchi come il **TCP SYN flooding** e una gestione più sicura del traffico di rete.
	
	Oggi, i **firewall di nuova generazione (NGFW)** operano fino a **livello 7**, offrendo un'analisi approfondita del traffico applicativo. Integrano tecnologie avanzate come **l'ispezione del contenuto, il rilevamento e la prevenzione delle intrusioni**, consentendo di identificare e bloccare minacce sofisticate come **malware e ransomware**. Inoltre, supportano la **segmentazione del traffico** e offrono un monitoraggio dettagliato in tempo reale.

---
## **Il Modello TCP-IP**

Il **modello TCP/IP** semplifica la struttura del **modello OSI** combinando diversi livelli e rispecchiando più fedelmente il funzionamento delle reti moderne.

A differenza dell'OSI, che risulta più teorico, il modello **TCP/IP** è stato adottato nella pratica e costituisce la base della **Internet Protocol Suite**, ovvero l'insieme di protocolli su cui si basa Internet. Il protocollo IP (corrispondente al livello 3 dell'OSI) è un pilastro fondamentale della comunicazione tra reti diverse, rendendo TCP/IP il modello dominante nelle reti attuali.

### **Struttura del modello TCP/IP rispetto all'OSI**

TCP/IP riduce il numero di livelli OSI combinandoli in quattro strati principali:

- **Livello 1: Accesso alla rete** (equivale ai livelli OSI **Fisico + Data Link**) – Gestisce la trasmissione dei dati su reti locali.
- **Livello 2: Internet** (equivale al livello OSI **Rete**) – Si occupa dell'instradamento dei pacchetti tra reti diverse, utilizzando IP.
- **Livello 3: Trasporto** (equivale al livello OSI **Trasporto**) – Regola la trasmissione dei dati tra host con protocolli come **TCP** (affidabile) e **UDP** (veloce).
- **Livello 4: Applicazione** (equivale ai livelli OSI **Sessione + Presentazione + Applicazione**) – Include i protocolli utilizzati dalle applicazioni, come **HTTP, FTP, SMTP**.


![[Pasted image 20250319200903.png]]

In pratica, il modello TCP / IP fornisce quanto segue:
- Costituisce la base di Internet e di altre reti su larga scala
- Fornisce un approccio semplificato e più pratico alle comunicazioni di rete, rispetto al modello OSI
- Serve come standard universale per la comunicazione di rete, data la sua ampia adozione e implementazione da parte di un'ampia varietà di dispositivi e applicazioni.


Ecco come appare nel modello TCP-IP il processo di aggiunta (**incapsulamento**) e rimozione (**decapsulamento**) dei dati:

![[Pasted image 20250319201104.png]]