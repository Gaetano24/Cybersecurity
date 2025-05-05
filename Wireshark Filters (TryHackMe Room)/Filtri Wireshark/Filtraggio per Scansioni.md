
### **TCP Completezza (tcp.completeness)**

Il campo `tcp.completeness` indica il **livello di completamento di una conversazione TCP**, combinando valori numerici assegnati ai vari flag/contenuti.

---

### **Valori associati ai tipi di pacchetto**

|Componente|Valore|
|---|---|
|SYN|1|
|SYN/ACK|2|
|ACK|4|
|Dati|8|
|FIN|16|
|RESET (RST)|32|

![[Pasted image 20250505142711.png]]

---

### **Esempi di filtro**

- **Handshake completo (SYN + SYN/ACK + ACK)**  
    `tcp.completeness == 7`  
    _(1 + 2 + 4)_
    
- **Connessione stabilita + dati + chiusura corretta (completa)**  
    `tcp.completeness == 31`  
    _(1 + 2 + 4 + 8 + 16)_
    
- **Scansione stealth (Nmap SYN scan + RST)**  
    `tcp.completeness == 35`  
    _(1 + 2 + 32)_
    
- **Tentativo filtrato (solo SYN)**  
    `tcp.completeness == 1`
    
- **Porta chiusa (SYN + RST/ACK)**  
    `tcp.completeness == 37`  
    _(1 + 32 + 4)_
    

---

### **Utilizzo**

- Utile per identificare rapidamente:
    
    - Connessioni complete
    - Scansioni
    - Tentativi di accesso falliti o respinti
    
- Ottimo per analizzare traffico sospetto in grandi PCAP

---
