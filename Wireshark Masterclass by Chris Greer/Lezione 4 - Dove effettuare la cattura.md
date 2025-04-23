
Prima di avviare una cattura con Wireshark, è fondamentale capire il problema che si vuole analizzare e individuare il punto migliore della rete in cui intercettare il traffico.
Ad esempio, se stiamo cercando di risolvere un problema di connettività di un singolo client verso un server, il punto di cattura sarà diverso rispetto a un'indagine su un incidente di sicurezza che coinvolge un'intera rete.

![[Pasted image 20250403141736.png]]

In questo esempio, un buon punto per catturare il traffico può essere:

- **Lato client**, ad esempio sull’access point, per monitorare gli utenti connessi.
- **Lato server**, posizionando Wireshark fuori dallo switch, se possibile.
- **Lungo il percorso di rete**, ad esempio prima dell’ingresso nel provider, per ottenere una visione più ampia del traffico.

---

### **Casi ideali vs casi reali**

L’ideale sarebbe poter inserire più punti di cattura lungo la rete utilizzando dei **network tap** (rubinetti), dispositivi fisici che duplicano il traffico senza interrompere la connessione. Tuttavia, nella pratica, non sempre si ha accesso fisico alla rete.

Se non è possibile installare un network tap, possiamo usare altre tecniche come:

- **SPAN port (Switched Port Analyzer)**: configura uno switch per duplicare il traffico di una porta su un'altra, dove è collegato Wireshark.
- **Monitor port**: funziona in modo simile allo SPAN, permettendo di analizzare il traffico senza interferire con la rete.

Se non possiamo usare un **network tap** e non abbiamo accesso alla rete per inviare il traffico a un analizzatore, possiamo comunque raccogliere dati utili installando **Wireshark direttamente sul client**. Questo ci permetterà di osservare cosa sta succedendo nella comunicazione tra client e server.

Dal lato server, sarebbe ideale ottenere una **cattura simultanea** sia lato client che lato server per avere una visione completa del traffico.  
Prima di procedere, dobbiamo considerare alcuni aspetti:

- **Dove si trova il server?**
- **Che tipo di accesso ho a esso?**
- **Dovrei usare un V-TAP o un VSPAN?** (per la cattura in ambienti virtualizzati)

> **⚠️ Sconsigliato:** Installare Wireshark direttamente sul server non è una buona pratica, poiché potrebbe sovraccaricare il sistema, che è già impegnato a gestire altre operazioni.

---

### **Differenza tra TAP e SPAN**

Sia i **TAP (Test Access Point)** che le **SPAN port (Switched Port Analyzer)** vengono utilizzati per intercettare e analizzare il traffico di rete, ma funzionano in modi diversi e hanno pro e contro distinti.

- Un **TAP** è un dispositivo hardware che si installa fisicamente tra due dispositivi di rete per copiare tutto il traffico senza interrompere la comunicazione. Richiede accesso fisico alla rete per essere installato.

- La **SPAN port** è una funzione degli switch di rete che copia il traffico da una o più porte su una porta dedicata, dove può essere analizzato con strumenti come Wireshark. 

---

### **Conclusioni finali**

Per concludere, la scelta del punto di cattura dipende sempre dal problema da analizzare. Idealmente, vogliamo:

- Posizionarci **il più vicino possibile** ai due endpoint (client e server).
- Ottenere una **cattura simultanea** se possibile.
- **Evitare di installarlo direttamente sugli endpoint**, preferendo un **tap di rete o uno span** se abbiamo il controllo sulla rete.

Questa strategia ci permetterà di raccogliere dati utili senza impattare negativamente sulle prestazioni dei dispositivi coinvolti.

---

