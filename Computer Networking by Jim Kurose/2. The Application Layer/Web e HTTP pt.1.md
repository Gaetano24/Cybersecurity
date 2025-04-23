
## 🌐 **HTTP – HyperText Transfer Protocol**

### 📄 Pagine Web e Oggetti

Una **pagina web** non è solo un file HTML:

- Contiene **oggetti**: immagini, CSS, JS, video 
- Ogni oggetto è scaricato con **una richiesta HTTP separata**.

> Esempio: caricando una pagina con 1 HTML, 3 immagini e 1 CSS = **5 richieste HTTP**

---

## 📡 **Il protocollo HTTP**

### ⚙️ Caratteristiche

- Protocollo **di livello applicazione**
    
- Usa **TCP** come protocollo di trasporto (porta predefinita: **80**)
    
- È un protocollo **senza stato (stateless)**:
    
    - Ogni richiesta è **indipendente**
    - Il server **non conserva informazioni** sulle richieste precedenti
    

![[Pasted image 20250420153510.png]]

---

## 🔁 **HTTP Persistente vs Non Persistente**

### 🧱 HTTP Non Persistente

#### 🔍 Cos’è

- Per **ogni oggetto** richiesto, viene aperta **una nuova connessione TCP**.
- Dopo la risposta, la connessione viene **chiusa** subito.

#### 🧨 Conseguenze

- Ogni connessione richiede:
    
    - **3-way handshake TCP** (più lento)
    - Overhead di apertura/chiusura
    
- Maggiore **latenza totale**

---

### ⚡ HTTP **Persistente** (detto anche "keep-alive")

#### 🔍 Cos’è

- Una **sola connessione TCP** viene mantenuta **aperta** per trasferire **più oggetti**.
- Introdotto come **opzionale in HTTP/1.0**, ma **default in HTTP/1.1**

#### ✅ Vantaggi

- Meno overhead di handshake
- **Migliori prestazioni**
- Riduce il carico su client e server

---

## **📤 Request & 📥 Response**

### 🔸 Richiesta HTTP (Request)

Formato:

```
Metodo URI Versione
Header
(Linea vuota)
Corpo (opzionale)
```

> Esempio:

```
GET /index.html HTTP/1.1
Host: www.example.com
```

- **Metodi comuni**: `GET`, `POST`, `PUT`, `DELETE`, `HEAD`

---

### 🔹 Risposta HTTP (Response)

Formato:

```
Versione Codice Stato Messaggio
Header
(Linea vuota)
Corpo (contenuto richiesto)
```

> Esempio:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 456
```

---

## 🧾 **Status Code (Codici di Stato)**

|Codice|Categoria|Significato|
|---|---|---|
|1xx|Informativo|Ricevuta la richiesta, in elaborazione|
|2xx|Successo|✅ OK (200), Created (201)|
|3xx|Redirezione|Moved Permanently (301), Found (302)|
|4xx|Errore del client|❌ Not Found (404), Bad Request (400)|
|5xx|Errore del server|⚠️ Internal Server Error (500), Unavailable (503)|

---

## 🍪 **Cookie**

I **cookie** sono piccoli file di testo che i siti web inviano e memorizzano nel browser dell’utente. Contengono informazioni che permettono al sito di **riconoscere l’utente** nelle visite successive e di **mantenere uno stato** tra le varie richieste HTTP, che altrimenti sarebbero indipendenti l’una dall’altra.

---

### ⚙️ Come funzionano i cookie?

1. **Il server invia un cookie**: quando un utente visita un sito, il server può inviare un cookie attraverso l’header `Set-Cookie` nella risposta HTTP.

2. **Il browser memorizza il cookie**: il browser salva il cookie localmente, associandolo al dominio del sito.

3. **Il browser restituisce il cookie**: nelle richieste successive al medesimo dominio, il browser include automaticamente il cookie nell’header `Cookie` della richiesta HTTP.

4. **Il server legge il cookie**: il server riceve il cookie e può utilizzarne le informazioni per personalizzare la risposta o mantenere lo stato della sessione.


![[Pasted image 20250420154646.png]]

---

### 🧠 Perché i cookie sono utili?

I cookie permettono di:

- **Mantenere la sessione di login**: evitando di dover inserire le credenziali ad ogni pagina.
    
- **Salvare le preferenze dell’utente**: come la lingua o il tema scelto.
    
- **Gestire carrelli della spesa**: in siti e-commerce, mantenendo i prodotti selezionati.
    
- **Personalizzare l’esperienza di navigazione**: offrendo contenuti rilevanti basati sulle interazioni precedenti.

---

### 🧾 Esempio di header HTTP con cookie

**Risposta del server:**

```
HTTP/1.1 200 OK 
Set-Cookie: sessionId=abc123; Path=/; HttpOnly
```

**Richiesta successiva del browser:**

```
GET /dashboard HTTP/1.1 
Host: www.example.com 
Cookie: sessionId=abc123`
```

---

### 🔐 Tipi di cookie

- **Cookie di sessione**: temporanei, vengono eliminati alla chiusura del browser.
    
- **Cookie persistenti**: rimangono memorizzati per un periodo definito, anche dopo la chiusura del browser.
    
- **Cookie di terze parti**: impostati da domini diversi da quello visitato, spesso utilizzati per tracciamento e pubblicità.

---

