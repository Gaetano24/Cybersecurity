
Il concetto di **Name Resolution** in Wireshark riguarda la conversione di valori numerici (come indirizzi IP, porte e indirizzi MAC) in nomi più leggibili e comprensibili, facilitando così l'analisi del traffico di rete.

> [!NOTE] 
> Edit > Preferences > Name Resolution

---

## **Risoluzione degli indirizzi**

Wireshark può risolvere i nomi a vari livelli:

- Ethernet (MAC)
- IP (Livello Rete)
- TCP/UDP (Livello Trasporto)

Di default è attivata solamente la risoluzione degli indirizzi MAC

![[Pasted image 20250407192901.png]]

Cosa succede se attiviamo la risoluzione degli indirizzi IP?

![[Pasted image 20250407193538.png]]

Con queste impostazioni:

- Wireshark **prova prima a risolvere tramite i pacchetti DNS catturati**
- Se non trova risposte lì, **interroga i DNS configurati nel sistema operativo**
- Se anche quello fallisce **mostrerà l'indirizzo IP così com'è**, senza risoluzione.

**Nota**: Wireshark permette di utilizzare una lista personalizzata di server DNS per effettuare la risoluzione degli indirizzi (in questo caso è disabilitata).

> [!Per visualizzare l'elenco degli host risolti:] 
> Statistics > Resolved Addresses : hosts

![[Pasted image 20250407194545.png]]

---

## **Configurazione manuale dei nomi**

Attraverso il comando `Edit Resolved Name` (fare tasto destro su un indirizzo IP) è possibile configurare manualmente la risoluzione di uno specifico host:

![[Pasted image 20250407195023.png]]

Per salvare le modifiche effettuare (es. configurazioni manuali di host name):

> [!NOTE] 
> View > Reload as File Format/Capture

In questo modo tutte le configurazioni inserite manualmente saranno automaticamente memorizzare nel file di cattura.

---
