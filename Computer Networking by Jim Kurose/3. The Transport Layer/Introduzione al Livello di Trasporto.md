
### **Servizi e Protocolli di Trasporto**

- Forniscono **comunicazione logica** tra processi applicativi su host diversi.
    
- Due protocolli principali:
    
    - **UDP**: non affidabile, consegna disordinata, nessuna garanzia su ritardi o banda.
        
    - **TCP**: affidabile, consegna in ordine, controllo di congestione e di flusso, richiede setup di connessione.

![[Pasted image 20250505145121.png]]

---

### **Ruolo nei Sistemi Terminali**

- **Mittente**:
    
    - Riceve messaggi dall’applicazione
    - Li suddivide in segmenti
    - Crea intestazioni (header) e passa al livello di rete
    
- **Destinatario**:
    
    - Riceve segmenti dal livello di rete (IP)
    - Verifica intestazioni
    - Ricompone messaggi
    - Passa all’applicazione tramite socket

---

### **Livello di Trasporto vs. Livello di Rete**

- **Livello di rete**: comunicazione logica tra **host**
    
- **Livello di trasporto**: comunicazione logica tra **processi**
    
- Il trasporto si basa sui servizi del livello di rete e li arricchisce

---
