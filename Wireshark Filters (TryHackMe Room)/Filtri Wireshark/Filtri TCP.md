### **Filtrare per porte TCP**

- **Singola porta**:  
    `tcp.port == 80`  
    (traffico su porta 80)
    
- **Porta sorgente o destinazione**:  
    `tcp.srcport == 80`  
    `tcp.dstport == 80`
    
- **Più porte**:  
    `tcp.port in {80 443}`
    
- **Intervallo di porte**:  
    `tcp.port in {8000..8004}`
    

---

### **Filtrare per flag TCP**

- **SYN (inizio connessione)**:  
    `tcp.flags.syn == 1`
    
- **FIN (fine connessione)**:  
    `tcp.flags.fin == 1`
    
- **RESET (connessione terminata anormalmente)**:  
    `tcp.flags.reset == 1`
    

---

###  **TCP Conversazioni (4-tuple)**

- IP sorgente, porta sorgente, IP destinazione, porta destinazione
    
- In Wireshark: tasto destro su un pacchetto → **Filtro di conversazione > TCP**


![[Pasted image 20250505141142.png]]

---

### **Analisi problemi TCP**

- Per filtrare:
    
    - **Ritrasmissioni**
        
    - **Pacchetti fuori ordine**
        
    - **Doppi ACK**
        
    
    Usa:  
    `tcp.analysis.flags`
    

---
