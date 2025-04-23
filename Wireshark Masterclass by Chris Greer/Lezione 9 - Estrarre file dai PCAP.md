## **Ricostruzione dei segmenti TCP** 

TCP è un protocollo orientato al flusso e **può spezzettare un messaggio** (come una richiesta HTTP o un pacchetto TLS) su più segmenti. L'opzione **"Allow subdissector to reassemble TCP streams"** permette a Wireshark di **ricostruire il messaggio completo** a partire da questi frammenti TCP.

> [!NOTE] Attivare l'opzione:
> 
> Transmission Control Protocol > Protocol Preferences > Allow subdissector to reassemble TCP streams
> 
> Alternativa:
> 
> Edit > Preferences > Protocols > TCP > Allow subdissector to reassemble TCP streams

In figura viene riportata la prima alternativa menzionata:

![[Pasted image 20250408195645.png]]

---

## **Estrarre file trasferiti via HTTP**

La funzione **Export Objects** permette di:

- Vedere **tutti i file o risorse** trasferite via HTTP nel traffico catturato
- **Salvare quei file** sul proprio computer (immagini, PDF, eseguibili, script, ecc.)

> [!NOTE] Dove si trova?
> 
> **File > Export Objects > HTTP**
> 
> Si aprirà una finestra con una lista di oggetti HTTP identificati nel traffico
> 

![[Pasted image 20250408194939.png]]

---

### **Cosa trovi nella finestra?**

| Campo            | Cosa mostra                                                           |
| ---------------- | --------------------------------------------------------------------- |
| **No.**          | Numero del pacchetto in cui inizia l’oggetto                          |
| **Hostname**     | L’host da cui proviene il file (es. `example.com`)                    |
| **Content Type** | Il tipo MIME del contenuto (es. `image/jpeg`, `text/html`)            |
| **Size**         | Dimensione del file                                                   |
| **Filename**     | Il nome del file, se presente nell’header `Content-Disposition` o URL |
| **Info**         | Qualche dettaglio extra (come l’URL richiesto)                        |

---

### **Quando funziona bene?**

- Quando il file è stato **trasferito via HTTP in chiaro** (porta 80, no HTTPS!)
- Quando l’intero contenuto del file è **presente nel pcap** (non troncato)
- Quando l’opzione **“Allow subdissector to reassemble TCP streams”** è **abilitata** (altrimenti i file potrebbero non essere completi!)

---

### **Pro tip**

Se stai facendo penetration testing o analisi malware, puoi usarlo per:

- Scaricare payload sospetti
- Salvare immagini, script JS, o file PHP
- Raccogliere prove di esfiltrazione dati

---

## **Follow TCP Stream**

La funzione **Follow TCP Stream** in **Wireshark** è uno degli strumenti più utili e intuitivi per **ricostruire conversazioni TCP** complete, come richieste e risposte HTTP, chat in chiaro, login, comandi FTP, e molto altro.

---

### **Cosa permette di fare**:

La funzione **Follow TCP Stream** permette di:

- Ricostruire **tutto il contenuto** di una conversazione TCP punto-a-punto (es. client-server)    
- Vederlo in formato leggibile (testo, ASCII, raw)
- Distinguere tra dati inviati e ricevuti
- Esportare facilmente il contenuto della sessione


> [!NOTE] Come si usa?
> 1. Trova un pacchetto TCP (es. uno con `http`, `ftp`, `smtp`, ecc.)
> 2. **Clic destro** sul pacchetto
> 3. Vai su **"Follow" > "TCP Stream"**
 

![[Pasted image 20250408195722.png]]

---

###  **Cosa vedo nella finestra che si apre?**

- Il contenuto della sessione in formato **testuale**

- Dati separati per **direzione**:
    - 🔴 Inviato dal client al server (di solito in **rosso**)        
    - 🔵 Inviato dal server al client (di solito in **blu**)
 
- Un menù a tendina per cambiare il formato di visualizzazione:  
    `ASCII`, `Hex Dump`, `C Arrays`, `Raw`, ecc.

- Pulsanti per:
    - **Salvare** il contenuto        
    - **Cambiare stream** (se ci sono più conversazioni TCP nel file)

---

### **Perché è utile questa funzione?**

- **Per analizzare protocolli in chiaro**:
	- HTTP → vedi richieste GET/POST e risposte HTML
	- FTP → vedi login, comandi e trasferimenti
	- Telnet / SMTP → vedi cosa ha scritto un utente
	- IRC / Chat → ricostruisci le conversazioni

- **Per cercare dati sensibili (in ambienti di test!)**
	- Username e password in chiaro
	- Cookie HTTP
	- Token di sessione
	- E-mail, messaggi, dati inviati in form

- **Per esportare file o payload**

	Puoi salvare l’intero flusso come `.txt`, `.bin`, ecc. per ulteriori analisi (o con strumenti come `foremost`, `binwalk`, ecc.)

---

### **Pro Tip**

E' possibile filtrare per stream TCP specifico scrivendo:

`tcp.stream == N`

(dove `N` è il numero dello stream visto nella finestra)

---
