## **Cos'è IPv6:**

Successore di IPv4, progettato per risolvere il problema dell’esaurimento degli indirizzi. Fornisce **uno spazio praticamente illimitato** di indirizzi e semplifica la configurazione delle reti.

---

## **Formato degli indirizzi IPv6:**

- **Lunghezza**: 128 bit (contro i 32 di IPv4)
    
- **Notazione esadecimale**, divisa in 8 blocchi da 16 bit:
    
    `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
    
- **Regole di abbreviazione**:
    
    - Si possono omettere zeri iniziali in ogni blocco: `0db8` → `db8`
        
    - Si può comprimere **una sola sequenza consecutiva di blocchi a zero** con `::`:
        
        `2001:db8:85a3::8a2e:370:7334`

---

## **Tipi di indirizzi IPv6:**

|Tipo|Prefisso|Scopo|
|---|---|---|
|**Unicast globale**|`2000::/3`|Instradabile pubblicamente su Internet|
|**Link-local**|`fe80::/10`|Comunicazione locale punto-punto (obbligatorio su ogni interfaccia)|
|**Unique local**|`fc00::/7`|Indirizzi privati, non instradabili su Internet|
|**Multicast**|`ff00::/8`|Invio a gruppi di dispositivi (usato anche da ICMPv6, NDP)|

> In IPv6 **non esiste il broadcast** → tutto è gestito tramite **multicast**.

---

## **Formato del Datagramma IPv6**

Il datagramma IPv6 ha una struttura composta da vari campi, come segue:

![[Pasted image 20250511150806.png]]

|Campo|Lunghezza|Descrizione|
|---|---|---|
|**Versione**|4 bit|Indica la versione del protocollo. Per IPv6 è sempre `0110`.|
|**Traffic Class**|8 bit|Usato per il controllo della qualità del servizio (QoS).|
|**Flow Label**|20 bit|Usato per identificare flussi di pacchetti con requisiti di trattamento simili.|
|**Payload Length**|16 bit|Lunghezza del corpo del pacchetto (escluso l'header).|
|**Next Header**|8 bit|Identifica il protocollo del livello superiore (es. TCP, UDP, ICMPv6).|
|**Hop Limit**|8 bit|Similarmente al Time To Live (TTL) di IPv4, limita il numero di hop.|
|**Indirizzo sorgente**|128 bit|Indirizzo IPv6 del nodo di origine.|
|**Indirizzo destinazione**|128 bit|Indirizzo IPv6 del nodo di destinazione.|

### Quali campi sono stati rimossi rispetto a IPv4?

- checksum
- fragmentation/reassembly
- options

---

## **Tunneling IPv6 su IPv4**

Il **tunneling** consente il **trasporto di pacchetti IPv6 all’interno di una rete IPv4**, utile in reti **non ancora compatibili nativamente con IPv6**.

Serve per:

- Garantire **interoperabilità** durante la transizione IPv4 → IPv6
- Collegare due nodi IPv6 tramite una rete IPv4 intermedia

### Encapsulation

Eccome come un pacchetto IPv6 viene incorporato in un pacchetto IPv4 come un payload.

![[Pasted image 20250511153013.png]]


### Schema di tunneling

![[Pasted image 20250511153219.png]]


### Perché il tunneling non è una soluzione permanente?

- Aggiunge **latenza** e **complessità**.
    
- Dipende da IPv4, mentre IPv6 dovrebbe **eliminare** tale dipendenza.
    
- Molti meccanismi (es. Teredo) sono **bloccati da firewall/NAT**.

> [!NOTE]
>  Oggi si preferiscono connessioni **dual-stack** (IPv4 + IPv6 nativo), o reti full-IPv6.

---


