## **Generalized Forwarding: Match + Action**

È un modello **astratto e flessibile** per l’inoltro dei pacchetti che si basa su:

- **Match**: identificazione di pacchetti tramite campi specifici dei loro header.
    
- **Action**: operazioni da eseguire su quei pacchetti.

Rispetto al tradizionale modello IP (basato solo su destinazione IP → next hop), generalized forwarding consente decisioni basate su **più campi**, o perfino su metadati.

### **Esempio di Match Fields**

- Ethernet (MAC src/dst, Ethertype)
- VLAN ID
- IP src/dst
- Protocollo IP (TCP, UDP, ICMP)
- TCP/UDP port src/dst
- MPLS label
- Metadata assegnati dal controller

### **Tipi di Azioni (Action)**

- **Forward** a una o più porte.
- **Drop** (blocca il pacchetto).
- **Modify**: cambia campi dell’header (es. riscrivi IP di origine).
- **Encapsula/Decapsula** (es. MPLS, tunneling).
- **Invia al controller** per decisioni centralizzate.


![[Pasted image 20250511160226.png]]

### **Applicazioni tipiche**

- SDN (es. OpenFlow)
- Middlebox programmabili (firewall, NAT, load balancer)
- Service chaining (catene di servizi su più dispositivi)

---

## **OpenFlow**

Un dispositivo OpenFlow (es. switch) contiene una o più **flow tables**, ciascuna con **flow entries** che specificano come gestire i pacchetti.

### **Struttura di una Flow Entry**

|Campo|Descrizione|
|---|---|
|**Match Fields**|Specificano i criteri di corrispondenza (sui campi dell’intestazione)|
|**Priority**|Numero intero: più alto = ha precedenza in caso di più match|
|**Counters**|Statistiche su pacchetti/byte corrispondenti (monitoraggio, billing, etc.)|
|**Instructions**|Azioni da eseguire se il pacchetto corrisponde|
|**Timeouts**|Rimozione automatica della entry (idle/hard timeout)|
|**Cookie**|ID opzionale associato alla voce (utile per controllo e gestione remota)|

![[Pasted image 20250511160521.png]]

### **Comportamento del pacchetto**

1. **Arrivo pacchetto** allo switch.
    
2. Cerca la **prima entry** (con priorità maggiore) che fa match con il pacchetto.
    
3. Se trovata:
    
    - Aggiorna i counters.
    - Esegue le azioni specificate.
      
4. Se non trovata:
    
    - Scatena una **table miss** → default: invia il pacchetto al **controller**.

#### Esempi

![[Pasted image 20250511160930.png]]

### **OpenFlow Abstraction**

"**match+action**" è un'astrazione che unisce diversi tipi di dispositivi.

![[Pasted image 20250511160806.png]]

#### Esempio

![[Pasted image 20250511160859.png]]

---

