## **Cos'è il Port Forwarding?**

Il **port forwarding** è una tecnica usata per **rendere accessibili dall’esterno** (Internet) dei servizi ospitati **su dispositivi all’interno di una rete privata** (LAN), nonostante ci sia di mezzo un **router con NAT**.

**Port forwarding** = Inoltro delle porte

Permette di:

- **Aprire una porta** del router (che ha l'**IP pubblico**)
    
- **Inoltrare il traffico** ricevuto su quella porta verso un **dispositivo interno alla rete** (con IP privato)

---

## **Esempio pratico**

Hai un **server web** sulla tua rete interna:

- IP del server: `192.168.1.100`
    
- Il server ascolta sulla porta `80` (HTTP)
    
- Il router ha IP pubblico: `203.0.113.5`


### Senza port forwarding:

Il traffico proveniente da Internet verso `203.0.113.5:80` **non sa dove andare** nella LAN → bloccato.

### Con port forwarding configurato:

Il router sa che:

```
Tutto ciò che arriva su 203.0.113.5:80 → gira a 192.168.1.100:80
```

---

## **Come funziona tecnicamente?**

1. Il pacchetto arriva al router NAT dall'esterno (es. `203.0.113.5:80`)
    
2. Il router controlla la **tabella di port forwarding**
    
3. Reindirizza il pacchetto al dispositivo locale corretto
    
4. Il dispositivo risponde → il router inverte il processo per inviare la risposta

---

## **Tipi di port forwarding**

|Tipo|Descrizione|
|---|---|
|**Statico (Manuale)**|Configurato dall’utente (es. `porta 22 → host SSH`)|
|**Dinamico (UPnP)**|Apertura automatica delle porte da parte delle app|
|**Range forwarding**|Inoltro di un intervallo di porte (es. per giochi)|
|**Port triggering**|Attiva l’inoltro **solo quando** un'app lo richiede|

---

## **Quando si usa il port forwarding?**

- Hostare un **server HTTP/HTTPS** su una rete domestica
    
- Connettersi a un **server FTP, SSH o RDP**
    
- Giochi online che richiedono porte specifiche
    
- Accesso a videocamere IP o sistemi di domotica da remoto
    
- Applicazioni P2P (torrent, VoIP, ecc.)

---

## **Come configurarlo**

1. Accedi all'interfaccia del router (di solito `192.168.1.1`)
    
2. Cerca la sezione **"Port Forwarding", "Virtual Server"** o simile
    
3. Inserisci:
    
    - Porta esterna
    - IP interno
    - Porta interna
    - Protocollo (TCP/UDP o entrambi)
    
4. Salva e riavvia se richiesto

---
