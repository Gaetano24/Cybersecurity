---

---
## **Filtri di cattura (Capture Filters)**

Questi filtri vengono applicati **prima** che il traffico venga registrato: servono a **limitare** i pacchetti che Wireshark effettivamente cattura.  

Si impostano **prima** di iniziare la cattura, nel campo "Capture Filter".

### Esempi comuni

|Filtro|Descrizione|
|---|---|
|`host 192.168.1.1`|Cattura solo i pacchetti da/verso l’host 192.168.1.1|
|`net 192.168.0.0/24`|Cattura il traffico per la rete 192.168.0.0/24|
|`port 80`|Solo traffico HTTP (porta 80)|
|`tcp`|Solo pacchetti TCP|
|`udp`|Solo pacchetti UDP|
|`tcp port 443`|Solo traffico HTTPS|
|`src host 10.0.0.5`|Solo pacchetti inviati **da** 10.0.0.5|
|`dst port 53`|Solo pacchetti **verso** la porta 53 (DNS)|

**Nota:** I filtri di cattura usano la sintassi di **libpcap**, più limitata rispetto ai filtri di visualizzazione.

---

## **Filtri di visualizzazione (Display Filters)**

Questi filtri vengono applicati **dopo** la cattura, per **filtrare e analizzare** solo i pacchetti che ti interessano.  

Si inseriscono nella barra in alto, anche mentre la cattura è in corso o dopo che è finita.

### Esempi comuni

| Filtro                                        | Descrizione                                                                           |
| --------------------------------------------- | ------------------------------------------------------------------------------------- |
| `ip.addr == 192.168.1.1`                      | Mostra pacchetti da/verso l’indirizzo IP                                              |
| `tcp.port == 443`                             | Mostra pacchetti TCP con porta 443 (HTTPS)                                            |
| `tcp.port in {80, 443, 8080}`                 | Mostra tutti i pacchetti TCP in cui la porta sorgente o destinazione è 80, 443 o 8080 |
| `http`                                        | Mostra solo pacchetti HTTP                                                            |
| `dns`                                         | Mostra solo pacchetti DNS                                                             |
| `tcp.flags.syn == 1`                          | Solo pacchetti TCP con flag SYN (inizio connessione)                                  |
| `frame contains "password"`                   | Cerca pacchetti che contengono la stringa "password" (controllo case-sensitive)       |
| `frame matches Google`                        | Cerca pacchetti che contengono la stringa "Google" (controllo non case-sensitive)     |
| `ip.src == 10.0.0.2 && ip.dst == 192.168.1.5` | Solo traffico da 10.0.0.2 a 192.168.1.5                                               |

---

## **Differenza chiave**

- **Filtri di cattura**: riducono i dati **registrati** al momento della cattura
- **Filtri di visualizzazione**: filtrano i dati **già catturati**

**Nota**: usare filtri di cattura specifici potrebbe farci perdere informazioni importanti.

---

