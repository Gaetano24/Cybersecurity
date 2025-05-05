### **Operatori standard**

- `==` : uguaglianza
    
- `&&` : AND logico
    
- `!` : NOT logico
    
- `>` / `<` : maggiore / minore


---

### **Operatore `in`**

Utilizzato per specificare elenchi o intervalli di valori in un campo.

**Esempi**:

- Porte TCP:  
    `tcp.port in {80, 443, 8000..8009}`
    
- Metodi HTTP:  
    `http.request.method in {GET, POST}`
    

---

### **Operatore `contains`**

Ricerca stringhe all’interno di un campo o dell’intero pacchetto.  
Case-sensitive (fa distinzione tra maiuscole e minuscole).

**Esempi**:

- In tutto il pacchetto:  
    `frame contains "hack"`
    
- In un campo specifico:  
    `dns.qry.name contains "login"`
    

---

### **Operatore `matches`**

Consente l’uso di espressioni regolari compatibili con Perl.  
Utile per ricerche complesse e case-insensitive (specificando `(?i)` nella regex).

**Esempi**:

- Ricerca semplice insensibile al caso:  
    `frame matches "hack"`
    
- Ricerca di estensioni file:  
    `frame matches "(?i)\.(php|txt|exe)"`
    
- Versione case-sensitive:  
    `frame matches "\.(php|txt|exe)"`
    

---

### **Note utili**

- `contains` è più semplice ma distingue tra maiuscole e minuscole.
    
- `matches` è più flessibile grazie all’uso delle espressioni regolari.
    
- Utili per trovare nomi utente, password, percorsi, estensioni di file o altri dati rilevanti nei pacchetti.

---
