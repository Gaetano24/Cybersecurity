
I filtri più semplici da ricordare sono i **filtri di protocollo**. Per la maggior parte, sono gli stessi del loro nome.

- `dns` → per vedere solo traffico DNS
- `tcp` → per tutto il traffico TCP
- `arp` → per il traffico ARP

Per escludere uno specifico protocollo si usa `!` oppure `not` :

- `!arp` → mostra tutto **tranne** il traffico ARP
- `not lldp` → esclude il protocollo LLDP

Per filtrare campi specifici di un protocollo utilizziamo il formato `protocollo.campo`:

- `ip.src` → indirizzo IP sorgente
- `ip.dst` → indirizzo IP di destinazione
- `tcp.flags.syn` → filtra pacchetti TCP con flag SYN attivo


> [!NOTE] Suggerimenti utili
> Guarda **in basso a destra** in Wireshark per il numero di pacchetti che corrispondono al filtro.
