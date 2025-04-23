
## 📧 **Email – Componenti e Funzionamento**

### 🧩 Componenti principali

1. **User Agent (UA)**
    
    - È il programma usato dall’utente per **scrivere, inviare e leggere** email.
    
    - Esempi: Outlook, Apple Mail, Thunderbird, Gmail (web client).
    
    - Funzioni:
        
        - Composizione del messaggio
        - Gestione cartelle (Posta inviata, Bozza, etc.)
        - Invio messaggi al mail server

---

2. **Mail Server**
    
    - Ogni utente ha un mail server associato (es. `smtp.gmail.com`, `mail.università.it`)
        
    - Funzioni:
        
        - **Invio** e **ricezione** di messaggi
        - Salvataggio dei messaggi in arrivo (casella di posta)
        - Comunicazione con altri mail server

---

3. **SMTP (Simple Mail Transfer Protocol)**
    
    - Protocollo usato per **inviare** email tra server e verso il server del destinatario.
        
    - Usa **TCP**, porta **25** (o 587 con autenticazione).
        
    - **Solo per l’invio** (non per la ricezione o lettura).
        
    - Comunicazione tipo: `client → server` e `server → server`


---

## 🔁 **Funzionamento base dell’invio email**

1. L’utente scrive l’email nel suo **user agent (UA)**.
    
2. Il UA invia l’email al proprio **mail server** usando **SMTP**.
    
3. Il **mail server mittente** contatta il **mail server del destinatario**, sempre via SMTP.
    
4. Il **server del destinatario** salva il messaggio nella **casella di posta** del destinatario.
    
5. Quando il destinatario apre il proprio UA:
    
    - Recupera l’email dal server usando protocolli di lettura (es. **IMAP**).


![[Pasted image 20250420160419.png]]

---

## 🧪 **Protocolli a confronto**

|Protocollo|Funzione|Porta|
|---|---|---|
|**SMTP**|Invio email|25 / 587|
|**POP3**|Scarica e rimuove dal server|110|
|**IMAP**|Consulta email lasciandole sul server|143 / 993|

> 🔸 IMAP è più moderno e adatto a più dispositivi (sincronizzazione).  
> 🔹 POP3 scarica e rimuove: meno adatto per accessi da più dispositivi.

---

## 📄 **RFC 5321 – Simple Mail Transfer Protocol (SMTP)**

### ✉️ Scopo

Definisce il protocollo base per il trasporto affidabile ed efficiente delle email su Internet. SMTP è indipendente dal sistema di trasmissione sottostante e richiede solo un canale di dati affidabile e ordinato. ​

### 🧱 Struttura del protocollo

- **Comandi e risposte**: SMTP opera tramite una serie di comandi inviati dal client e risposte dal server.
    
- **Sessione**: Una sessione SMTP inizia con il comando `HELO` o `EHLO` e termina con `QUIT`.
    
- **Trasferimento dei messaggi**: I messaggi vengono trasmessi utilizzando il comando `DATA`, preceduto da `MAIL FROM` e `RCPT TO` per specificare il mittente e i destinatari.


![[Pasted image 20250420160818.png]]

---

## ✉️ **Struttura di un messaggio email (RFC 5322)**

Un messaggio email è composto da due sezioni principali:​

1. **Header (Intestazione)**  
    Contiene informazioni di controllo e metadati del messaggio. Alcuni campi comuni includono:
    
    - `From`: mittente del messaggio
    - `To`: destinatario
    - `Subject`: oggetto del messaggio
    - `Date`: data e ora di invio
    - `Message-ID`: identificatore univoco del messaggio
    
	I campi dell'intestazione seguono la sintassi `Campo: valore` e sono separati dal corpo del messaggio da una linea vuota.
    
2. **Body (Corpo)** 
    Contiene il contenuto effettivo del messaggio, che può essere in formato testo semplice o includere contenuti multimediali e allegati. Per supportare contenuti complessi, si utilizzano le specifiche MIME (Multipurpose Internet Mail Extensions).

![[Pasted image 20250420161236.png]]

