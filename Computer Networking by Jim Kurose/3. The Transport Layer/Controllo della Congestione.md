## **Concetti Fondamentali**

### **Cos'è la Congestione**

La congestione in una rete si verifica quando la quantità di dati offerta al sistema supera le capacità disponibili di trasmissione e buffering. Questo porta a:

- Aumento del **ritardo di accodamento** nei router
- **Perdita di pacchetti** per overflow dei buffer
- **Riduzione del throughput** globale, paradossalmente anche con maggiore carico

### **Congestione vs Controllo di Flusso**

- **Controllo di flusso**: Meccanismo punto-a-punto tra mittente e ricevente per evitare che quest’ultimo venga sovraccaricato.
    
- **Controllo della congestione**: Regola il **carico globale** sulla rete, tenendo conto delle risorse condivise.

---

## **Cause e Impatti della Congestione**

### **Scenario 1: Buffer infiniti nei router**

- In teoria, i pacchetti non vengono persi.
    
- Ma i ritardi aumentano rapidamente con il traffico → throughput effettivo si stabilizza a **R/2** (R = capacità del link condiviso).
    
- La rete resta operativa ma **con ritardi inaccettabili**.


### **Scenario 2: Buffer finiti**

- Quando i buffer si riempiono → **perdita di pacchetti**.
    
- Le ritrasmissioni:
    
    - Consumano banda
    - Possono generare **duplicati** per timeout prematuri
    
- Si spreca la capacità a monte: pacchetti persi viaggiano inutilmente fino al punto di congestione.

### **Scenario 3: Reti multi-hop**

- La congestione in un router può rallentare o bloccare flussi anche a diversi salti di distanza.
    
- **Effetto domino**: rallentamenti a valle si riflettono a monte, causando ulteriore inefficienza.


---

## **Approcci al Controllo della Congestione**

### **Controllo End-to-End**

**Caratteristica principale**: Il mittente regola la velocità senza feedback diretto dalla rete.

- Rileva congestione da:
    
    - **Perdita di pacchetti** (assenza di ACK, timeout)
    - **Aumento del Round-Trip Time (RTT)**
    
- Implementazioni:
    
    - **AIMD (Additive Increase Multiplicative Decrease)**
    - **Slow Start**
    - **Fast Retransmit** e **Fast Recovery**


### **Controllo Assistito dalla Rete**

**Caratteristica principale**: Router o dispositivi intermedi forniscono indicazioni esplicite sullo stato della rete.

- **ECN (Explicit Congestion Notification)**:
    
    - Router marcano pacchetti quando congestionati, senza scartarli
    - Il ricevitore notifica il mittente tramite gli ACK
    
- **DECbit** (DECnet):
    
    - Usa un singolo bit nei pacchetti per indicare carico eccessivo
    - Basato sulla media del buffer occupato nel router
    
- **ATM**:
    
    - Meccanismo a circuito virtuale
    - La rete stessa controlla e assegna rate di trasmissione


---

## **Meccanismi TCP**

### **AIMD (Additive increase - Multiplicative decrease)**

- Aumenta la **cwnd (congestion window)** di 1 MSS per RTT (fase di probing)
    
- Dimezza cwnd in caso di perdita (indicatore di congestione)
    
- Comportamento: **oscillazione a dente di sega**, stabile ma con lente convergenze

![[Pasted image 20250507233656.png]]


### **Slow Start**

- **Obiettivo**: evitare di sovraccaricare la rete all’inizio della connessione.
	
- `cwnd` parte da 1 MSS.
    
- Dopo ogni ACK ricevuto, `cwnd` **raddoppia** (crescita esponenziale).
    
- Prosegue fino a:
    
    - Raggiungimento di **ssthresh** → transizione a Congestion Avoidance.
    - Rilevamento di **perdita** → Fast Retransmit/Fast Recovery o reset in Slow Start.

![[Pasted image 20250507233248.png]]


### **Congestion Avoidance**

- **Obiettivo**: crescita più prudente della finestra per evitare congestione.
    
- Quando `cwnd ≥ ssthresh`, la crescita diventa **lineare**:
    
    - Ogni RTT: `cwnd += 1 MSS`
    
- Se rileva perdita:
    
    - `ssthresh = cwnd / 2`
    - Se 3 ACK duplicati → Fast Retransmit + Fast Recovery.
    - Se timeout → ritorno a Slow Start.


### **Fast Retransmit**

- **Obiettivo:**  Ritrasmettere un pacchetto perso **senza attendere il timeout**.
	
- **Meccanismo:**

	- Se il mittente riceve **3 ACK duplicati** per lo stesso numero di sequenza, presuppone che un pacchetto è andato perso ma i successivi sono stati ricevuti.
		
	- Il pacchetto mancante viene **ritrasmesso immediatamente**, senza aspettare il timeout del timer associato.


### **Fast Recovery**

**Obiettivo:**  Evitare di tornare a Slow Start dopo una perdita, mantenendo parzialmente la velocità di trasmissione.

**Funzionamento con TCP Reno:**

1. Dopo Fast Retransmit, si entra in Fast Recovery.
    
2. Il valore di **ssthresh** viene impostato a metà dell'attuale **cwnd**.
    
    `ssthresh = cwnd / 2`
    
3. **cwnd viene ridotto a ssthresh**, ma **non azzerato**.
	
	`cwnd = ssthresh + 3*MSS`
	
	(3*MSS perché ha già ricevuto 3 duplicati → 3 segmenti presumibilmente ricevuti)
	
4. Durante Fast Recovery:
    
    - Ogni ACK duplicato ricevuto → `cwnd += 1 MSS`
      Ogni ACK duplicato successivo indica che **altri pacchetti sono arrivati correttamente** al ricevitore, **ma non ancora quello perso**.
      
    - Quando arriva un ACK **nuovo**, si esce da Fast Recovery e si entra in **Congestion Avoidance**.
      Questo è **l’ACK che conferma il pacchetto ritrasmesso**, quello che mancava.


### **ECN (Explicit Congestion Notification)**

ECN è un meccanismo di controllo della congestione **assistito dalla rete**. Permette ai router di **segnalare la congestione** ai terminali **senza scartare pacchetti**.

**Funzionamento**:

1. Router che rileva congestione **non scarta** il pacchetto → lo **marca** con un bit nel campo IP (ECN Capable).
    
2. Il ricevitore riceve il pacchetto marcato e **avvisa il mittente** con un bit nei suoi ACK (campo `ECE` di TCP).
    
3. Il mittente **interpreta il segnale come un’avvisaglia di congestione** e **riduce la `cwnd`**, **senza aspettare perdite**.

![[Pasted image 20250507233734.png]]

---

## **Tecniche Avanzate**

### **TCP CUBIC**

TCP CUBIC è il **congestion control predefinito in Linux** da anni. È pensato per **link ad alta capacità** (es. 10 Gbps o più) e connessioni **a lunga distanza (high BDP)**.

**Principio base**: La crescita della `cwnd` segue una funzione **cubica** rispetto al tempo trascorso dall’ultima congestione.

**Formula**:

```
cwnd(t) = C * (t - K)^3 + W_max
```

- `W_max`:  valore massimo di cwnd prima della perdita
- `K` : punto in cui cwnd ritorna a W_max
- `C` : costante di aggressività


### **TCP BBR – Bottleneck Bandwidth and RTT**

BBR (sviluppato da Google) è un meccanismo **basato sul modello della rete**, non sulle perdite. Si concentra su **massimo throughput** con **minima latenza**.

- Non si basa sulle perdite per rilevare congestione
    
- Stima direttamente:
    
    - **Bandwidth disponibile**
    - **RTT minimo osservato**
    
- L’obiettivo è **riempire il "tubo" della rete senza sovraccaricarlo**

---