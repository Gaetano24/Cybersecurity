
### **Multiplexing / Demultiplexing**

Il **multiplexing** consente di inviare più flussi di dati su un singolo canale, mentre il **demultiplexing** assicura che ciascun flusso di dati venga indirizzato correttamente alla sua destinazione. Questo è possibile grazie agli header TCP aggiunti durante la fase di multiplexing.

![[Pasted image 20250505145640.png]]

---

### **Come funziona il demultiplexing**

L'host riceve i datagrammi IP. Ogni datagramma contiene l'indirizzo IP di origine e di destinazione. Ogni datagramma trasporta un segmento del livello di trasporto. Ogni segmento include i numeri di porta di origine e di destinazione.

L'host utilizza gli indirizzi IP e i numeri di porta per indirizzare correttamente il segmento al socket appropriato.

![[Pasted image 20250505150143.png]]

---

### **Sintesi**

**Multiplexing e Demultiplexing**: basati sui valori dei campi nell'intestazione del segmento e del datagramma

- **UDP**: Il demultiplexing avviene utilizzando **soltanto il numero di porta di destinazione**. Questo significa che il sistema indirizza i dati a un socket specifico in base al numero di porta di destinazione del datagramma UDP ricevuto.

- **TCP**: Il demultiplexing avviene utilizzando una **tupla a 4 elementi**: gli **indirizzi IP di origine e di destinazione** e i **numeri di porta di origine e di destinazione**. Questo permette di distinguere tra connessioni diverse anche se provengono dallo stesso indirizzo IP o dalla stessa porta, indirizzando correttamente i segmenti TCP al socket giusto.


**Multiplexing e Demultiplexing avvengono a tutti i livelli** del modello OSI, non solo al livello di trasporto. Ogni livello svolge un ruolo nella gestione dei flussi di dati attraverso la rete, usando le informazioni contenute nei relativi header per gestire correttamente il traffico.

---

