## **Cos'è il NAT?**

**NAT** è un meccanismo che permette a più dispositivi all’interno di una rete privata di accedere a Internet **utilizzando un solo indirizzo IP pubblico**.

![[Pasted image 20250511131936.png]]

## **Tipi di NAT**

### 1. **SNAT** – _Source NAT_

- Traduce solo l'**indirizzo IP sorgente**.
- Usato per traffico **in uscita** da una LAN verso Internet.
- Di solito con un **IP statico pubblico**.

Esempio:

`Interno: 192.168.1.10 → Router NAT → Internet: 203.0.113.5`

---

### 2. **DNAT** – _Destination NAT_

- Traduce solo l'**indirizzo IP di destinazione**.
- Usato per rendere **servizi interni accessibili dall'esterno** (es. web server).
- Tipico del **port forwarding**.

Esempio:

`Internet: 203.0.113.5:80 → Router DNAT → Interno: 192.168.1.100:80`

---

### 3. **PAT** – _Port Address Translation_ (aka NAT Overload)

- Traduce **IP + Porta**: consente a **più dispositivi** interni di usare lo **stesso IP pubblico**, differenziati dalle **porte sorgenti**.
- È il tipo più comune nei **router domestici**.

Esempio:

|Dispositivo interno|Porta interna|IP Pubblico:Porta esterna|
|---|---|---|
|192.168.1.10|51500|203.0.113.5:40001|
|192.168.1.11|51501|203.0.113.5:40002|

---

### **Riepilogo**

| Tipo                               | Funzione                                               | Esempio                               |
| ---------------------------------- | ------------------------------------------------------ | ------------------------------------- |
| **SNAT** (Source NAT)              | Traduce l’IP sorgente (tipico in uscita da LAN)        | 192.168.1.5 → 203.0.113.10            |
| **DNAT** (Destination NAT)         | Traduce l’IP di destinazione (usato per inoltro porte) | 203.0.113.10:80 → 192.168.1.100:80    |
| **PAT** (Port Address Translation) | Mappa IP e porta su base dinamica (NAT overload)       | 192.168.1.5:5050 → 203.0.113.10:40001 |

---

## **Come funziona il NAT?**

1. Il dispositivo interno invia un pacchetto verso Internet.
    
2. Il router NAT **sostituisce l’IP sorgente** con l’IP pubblico e registra la porta.
    
3. Quando la risposta torna, il router NAT **usa la tabella NAT** per inoltrare il pacchetto al dispositivo corretto.


![[Pasted image 20250511132931.png]]

---

## **Perché esiste il NAT?**

- IPv4 ha **solo ~4,3 miliardi di indirizzi**.
    
- Permette a **centinaia di dispositivi** privati di accedere a Internet tramite **1 solo IP pubblico**.
    
- **Sicurezza**: nasconde la rete interna.
    
- Supporta la **condivisione di connessione Internet** (es. router domestici).

---

## **Limitazioni del NAT**

- **Complica applicazioni peer-to-peer** (es. VoIP, gaming).
    
- Richiede tecniche come **UPnP**, **STUN**, **ALG**, **port forwarding**.
    
- Non è scalabile per servizi che devono essere **raggiungibili da fuori** (es. server web casalinghi).

---

