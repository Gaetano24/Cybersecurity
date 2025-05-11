## **IP Datagram Format**

Il **datagramma IP** è l'unità base di trasporto dei dati a livello rete (livello 3 del modello OSI). La sua struttura è definita dal protocollo IP (IPv4 o IPv6). Qui vediamo IPv4:

### Struttura del Datagramma IPv4:

![[Pasted image 20250510202245.png]]

| Campo                                   | Descrizione                                                                        |
| --------------------------------------- | ---------------------------------------------------------------------------------- |
| **Version (4 bit)**                     | Indica la versione del protocollo IP (4 per IPv4, 6 per IPv6).                     |
| **IHL (Internet Header Length, 4 bit)** | Lunghezza dell'intestazione IP in parole da 32 bit.                                |
| **Type of Service (ToS, 8 bit)**        | Indica la priorità e il tipo di servizio (QoS).<br>- diffserv (0:5)<br>- ECN (6:7) |
| **Total Length (16 bit)**               | Lunghezza totale del datagramma (header + dati).                                   |
| **Identification (16 bit)**             | Identifica univocamente ogni datagramma.                                           |
| **Flags (3 bit)**                       | Controlla la frammentazione.                                                       |
| **Fragment Offset (13 bit)**            | Indica la posizione del frammento nel datagramma originale.                        |
| **Time to Live (TTL, 8 bit)**           | Numero massimo di router attraversabili.                                           |
| **Upper Layer Protocol (8 bit)**        | Indica il protocollo del livello superiore (es. TCP=6, UDP=17).                    |
| **Header Checksum (16 bit)**            | Verifica d’integrità dell’header.                                                  |
| **Source IP Address (32 bit)**          | Indirizzo IP del mittente.                                                         |
| **Destination IP Address (32 bit)**     | Indirizzo IP del destinatario.                                                     |
| **Options (opzionale)**                 | Usato per funzioni speciali, non comune. (es. timestamp)                           |
| **Data (variabile)**                    | Il payload, ovvero i dati da trasportare.                                          |

---

## **IP Addressing: IP Address and Interfaces**

Ogni dispositivo connesso a una rete IP possiede un **indirizzo IP** che lo identifica univocamente nella rete.

### Interfacce:

Un **host** può avere più **interfacce di rete** (es. Wi-Fi, Ethernet), ciascuna con il proprio indirizzo IP. L’indirizzo IP è quindi assegnato a un’interfaccia, non al dispositivo in sé.

### Formato Indirizzo IPv4:

- 32 bit → 4 byte → es. `192.168.1.1`
    
- Diviso in due parti:
    
    - **Network ID**: identifica la rete.
    - **Host ID**: identifica l’host nella rete.


![[Pasted image 20250510202847.png]]

---

## **Subnets (Sottoreti)**

Una **subnet** (sottorete) è una divisione logica di una rete IP. In termini più pratici, una subnet è un insieme di interfacce che possono raggiungersi fisicamente senza passare da un router.

- Permette di suddividere una rete grande in più reti piccole.
    
- Ogni subnet ha:
    
    - Un **indirizzo di rete** (tutti gli host in quella subnet condividono questa parte).
    - Un **range di host validi**.
    - Un **indirizzo broadcast**.

### Subnet Mask:

- Determina quali bit dell'indirizzo IP rappresentano la rete.
    
- Esempio: `255.255.255.0` → primi 24 bit = rete, ultimi 8 = host


![[Pasted image 20250510203517.png]]

---

## **CIDR (Classless Inter-Domain Routing)**

**CIDR** è un metodo flessibile per rappresentare subnet.

- Notazione: `IP_address/prefix_length` (es. `192.168.1.0/24`)
    
- Il **prefix length** indica quanti bit rappresentano la parte di rete.
    
- Sostituisce il vecchio sistema a classi (Class A, B, C).
    
- Permette una migliore assegnazione degli IP e meno sprechi.

![[Pasted image 20250510203754.png]]

---

## **DHCP (Dynamic Host Configuration Protocol)**

**DHCP** è un protocollo che assegna dinamicamente indirizzi IP ai dispositivi su una rete.

![[Pasted image 20250510204014.png]]

### Processo DHCP:

1. **DHCP Discover** (broadcast): il client cerca un server DHCP.
2. **DHCP Offer**: il server propone un indirizzo.
3. **DHCP Request**: il client accetta la proposta.
4. **DHCP Acknowledgement**: il server conferma.

![[Pasted image 20250510204047.png]]

Il DHCP può anche assegnare:

- Gateway predefinito
- DNS server
- Subnet mask
- Lease time (durata temporale dell’indirizzo assegnato)



---

## **DHCP Handshake – 4 Fasi (DORA)**

### 1. **DHCP Discover**

- **Chi**: Client → Broadcast
    
- **Cosa**: "C'è un server DHCP disponibile?"
    
- **Dettagli**:
    
    - Il client non ha ancora un IP, quindi invia da `0.0.0.0` verso `255.255.255.255`
    - Porta sorgente: **UDP 68**
    - Porta destinazione: **UDP 67**
    - Include: MAC address del client, richieste opzionali (DNS, gateway…)

```
Client (0.0.0.0:68) → Broadcast (255.255.255.255:67)
[DHCP Discover]
```


### 2. **DHCP Offer**

- **Chi**: Server → Client (in broadcast se client non ha ancora IP)
    
- **Cosa**: "Ti propongo l’IP 192.168.1.100 per 24 ore"
    
- **Dettagli**:
    
    - Porta sorgente: **UDP 67**
    - Porta destinazione: **UDP 68**
    - Include: IP offerto, lease time, subnet mask, router, DNS…

```
Server (192.168.1.1:67) → Broadcast/Client MAC (UDP 68)
[DHCP Offer: IP 192.168.1.100]
```


### 3. **DHCP Request**

- **Chi**: Client → Broadcast
    
- **Cosa**: "Accetto l’IP che mi hai offerto"
    
- **Dettagli**:
    
    - Include: l’IP desiderato, l’identificatore del server che ha fatto l’offerta.
    - Questo passaggio permette al server di riservare l’IP per il client.

```
Client (0.0.0.0:68) → Broadcast (255.255.255.255:67)
[DHCP Request for IP 192.168.1.100]
```


### 4. **DHCP Acknowledgment (ACK)**

- **Chi**: Server → Client
    
- **Cosa**: "Confermo: l’IP 192.168.1.100 è tuo per 24 ore"
    
- **Dettagli**:
    
    - Il client può ora usare l’IP assegnato.
    - Potrebbe includere altre opzioni di configurazione di rete.

```
Server (192.168.1.1:67) → Client (192.168.1.100:68)
[DHCP ACK]
```

---

## **ICANN e l'allocazione degli indirizzi IP**

**ICANN** (Internet Corporation for Assigned Names and Numbers) è l'organismo responsabile della gestione degli indirizzi IP a livello globale.

1. **ICANN/IANA (Internet Assigned Numbers Authority)**  
    ↳ Gestisce lo **spazio degli indirizzi IP globali**.  
    ↳ Suddivide blocchi di grandi dimensioni (es. interi prefissi /8) ai registri regionali.

2. **RIR (Regional Internet Registries)**  
    ICANN assegna i blocchi ai **5 RIR**, ciascuno responsabile per una regione del mondo:

|RIR|Regione|
|---|---|
|ARIN|Nord America|
|RIPE NCC|Europa, Medio Oriente|
|APNIC|Asia-Pacifico|
|AFRINIC|Africa|
|LACNIC|America Latina, Caraibi|

3. **ISP (Internet Service Providers)**  
    i RIR assegnano blocchi più piccoli agli ISP e alle grandi aziende, che poi li assegnano agli utenti finali.

4. **Utenti finali / Aziende / Dispositivi**  
    L’IP viene assegnato all'interfaccia di rete tramite:
    
    - Configurazione manuale (statico)
    - DHCP
    - PPPoE (es. per connessioni DSL)
    - SLAAC (in IPv6)


![[Pasted image 20250511124357.png]]

---

## **Ripartizione e Formati dei Blocchi IP**

### IPv4 Address Space

IPv4 ha un totale di circa **4,3 miliardi di indirizzi** (2³²).

- Alcuni blocchi sono **riservati** e **non assegnabili** pubblicamente:
    
    - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16` → reti private
        
    - `127.0.0.0/8` → loopback
        
    - `169.254.0.0/16` → APIPA (link-local)
        
    - `224.0.0.0/4` → multicast
        
    - `240.0.0.0/4` → riservato (futuro/ricerca)

|Range IP|Nome|Scopo|Instradabile?|Note|
|---|---|---|---|---|
|`10.0.0.0/8`|Privata|LAN aziendali/grandi reti|❌|Usata con NAT|
|`172.16.0.0/12`|Privata|LAN medie|❌||
|`192.168.0.0/16`|Privata|LAN domestiche|❌||
|`127.0.0.0/8`|Loopback|Comunicazione interna|❌|Test locale|
|`169.254.0.0/16`|Link-local|Auto-IP se DHCP non risponde|❌|Solo nella LAN|
|`224.0.0.0/4`|Multicast|Invio a gruppi selezionati|✅ (solo LAN/WAN)||
|`240.0.0.0/4`|Riservato|Futuro uso/ricerca|❌|Attualmente inutilizzabile|

### IPv6 Address Space

IPv6 ha **2¹²⁸ indirizzi possibili**, distribuiti in base a **prefissi globali**. Alcuni esempi:

|Prefisso|Uso|
|---|---|
|`2000::/3`|Global unicast (pubblici)|
|`fc00::/7`|Unique local addresses (privati)|
|`fe80::/10`|Link-local|
|`::1/128`|Loopback|
|`ff00::/8`|Multicast|

---

## **Hierarchical Addressing**

La **struttura gerarchica** degli indirizzi IP migliora l'efficienza del routing:

### Esempio di Gerarchia (IPv4):

Un IP come `192.0.2.33/24` potrebbe essere interpretato così:

- **/8 (es. 192.0.0.0/8)** → Assegnato a un RIR (es. RIPE)
    
- **/16 (es. 192.0.0.0/16)** → Assegnato a un ISP
    
- **/24 (es. 192.0.2.0/24)** → Assegnato a un cliente aziendale
    
- **/32 (es. 192.0.2.33)** → Indirizzo host specifico


### Vantaggi della gerarchia:

- **Aggregazione delle rotte (route summarization)** → meno voci nelle tabelle di routing.
    
- **Controllo amministrativo più semplice**.
    
- **Scalabilità** → le grandi reti possono essere gestite come insiemi di subnet.

---