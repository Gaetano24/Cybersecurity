
## 🧱 **Stack di rete

La comunicazione in rete è organizzata in **livelli (layers)** per semplificare la progettazione e l’interoperabilità tra dispositivi e protocolli. I due modelli più comuni sono:

### 1. **Modello ISO/OSI (Open Systems Interconnection)** – 7 livelli

| Livello | Nome                  | Funzione principale                                        |
| ------: | --------------------- | ---------------------------------------------------------- |
|       7 | **Applicazione**      | Interfaccia per le applicazioni (es. HTTP, FTP, SMTP)      |
|       6 | **Presentazione**     | Formattazione, cifratura, compressione                     |
|       5 | **Sessione**          | Gestione dialogo tra host (es. apertura/chiusura sessioni) |
|       4 | **Trasporto**         | Trasferimento affidabile (TCP) o non (UDP) dei dati        |
|       3 | **Rete**              | Indirizzamento e instradamento (IP)                        |
|       2 | **Collegamento dati** | Comunicazione su rete locale (es. Ethernet, MAC)           |
|       1 | **Fisico**            | Trasmissione bit su mezzo fisico (cavi, onde radio, ecc.)  |

---

### 2. **Modello TCP/IP** – 4 livelli (più usato nella pratica)

| Livello TCP/IP   | Corrispondenza OSI | Esempi di protocolli      |
| ---------------- | ------------------ | ------------------------- |
| **Applicazione** | 5-6-7              | HTTP, FTP, SMTP, DNS, SSH |
| **Trasporto**    | 4                  | TCP, UDP                  |
| **Internet**     | 3                  | IP, ICMP, ARP             |
| **Accesso Rete** | 1-2                | Ethernet, Wi-Fi, MAC      |

> 🔗 Ogni livello interagisce solo con quello **immediatamente superiore o inferiore**.


![[Pasted image 20250417200434.png]]

---

## 📦 **Incapsulazione**

L’ **incapsulazione** è il processo attraverso il quale ogni livello dello stack aggiunge le **proprie informazioni di controllo (intestazioni o header)** ai dati ricevuti dal livello superiore.

### 🔁 Processo:

1. L’applicazione genera i **dati** (es. richiesta HTTP).
2. Il livello Trasporto aggiunge il suo **header** (es. porta TCP).
3. Il livello Rete aggiunge il suo **header IP**.
4. Il livello Dati aggiunge **header e trailer** (es. indirizzo MAC, controllo errori).
5. Il livello Fisico converte tutto in **bit** e li trasmette.


![[Pasted image 20250417200234.png]]

---