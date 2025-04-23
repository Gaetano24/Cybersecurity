## **Problema di risoluzione dei nomi**

L'utente su Linux-A (rete 192.168.1.0/24) non riesce a installare un client Samba a causa di un errore di rete temporaneo. L'indagine ha rivelato che il problema era legato alla risoluzione dei nomi DNS, impedendo l'accesso ai repository online.

**Metodologia di Risoluzione:**

1. **Verifica della configurazione di rete:**

    - Controllo dell'indirizzo IP e del gateway con `ip a` e `netstat -r`.        
    - Test di connettività al gateway (`ping 192.168.1.1`) e a Internet (`ping 8.8.8.8`), risultati positivi.

2. **Diagnosi del problema DNS:**
    
    - Il test di risoluzione DNS (`ping google.com`) fallisce.        
    - Controllo delle configurazioni DNS (`cat /etc/network/interfaces` e `cat /etc/resolv.conf`), che risultano errate o mancanti.
    
3. **Soluzione:**
    
    - Configurazione manuale del server DNS interno (`echo "nameserver 192.168.1.5" > /etc/resolv.conf`).    
    - Verifica della modifica con `cat /etc/resolv.conf`.
    - Test di risoluzione DNS riuscito (`ping google.com`).
    
4. **Installazione del client Samba:**
    
    - Comando `apk add samba-client` per installare il client.
    - Verifica dell'installazione con `smbclient --version`.    

---

## **Problema di assegnazione dell' indirizzo IP da parte del server DHCP**

**Problema:**  
L'utente su Linux-B (rete 10.10.10.0/24) non riesce a connettersi a Internet dopo un recente passaggio a DHCP. L'host non ottiene un indirizzo IP dal server DHCP.

**Metodologia di Risoluzione:**

1. **Verifica dell'assegnazione IP:**
    
    - Tentativo di ottenere un IP tramite `udhcpc`, senza successo.
    - Discussione con l'amministratore di sistema: il firewall locale dovrebbe fungere da server DHCP.

2. **Controllo della configurazione del firewall (pfSense):**
    
    - Accesso alla GUI web di pfSense tramite un browser su Host Browser-B.
    - Controllo della configurazione DHCP: il servizio risulta disabilitato.
    
3. **Abilitazione del server DHCP su pfSense:**
    
    - Attivazione del servizio DHCP con i seguenti parametri:    
        - **Intervallo IP:** 10.10.10.100 - 10.10.10.110
        - **Server DNS:** 10.10.10.1 (IP del firewall)
        - **Gateway:** 10.10.10.1
        
    - Salvataggio della configurazione e attesa della propagazione.
    
4. **Verifica del DNS Resolver:**
    
    - Controllo che il servizio DNS Resolver sia attivo su pfSense per la risoluzione dei nomi.
    
5. **Test della connessione su Linux-B:**
    
    - Riprova dell'assegnazione DHCP con `udhcpc`: questa volta riceve un indirizzo IP.
    - Controllo IP, gateway e DNS con `ip a`, `netstat -r` e `cat /etc/resolv.conf`.
    - Test della connettività con `ping google.com`, che conferma il successo.

---


## **Problema di Risoluzione DNS per Host Locale**

**Problema:**  
Dopo l'installazione del client Samba, l'utente su Linux-A (rete 192.168.1.0/24) non riesce a connettersi a FILESERVER (presente nella stessa rete) tramite SMB. Il comando `smbclient -L FILESERVER -U cybrary` fallisce e il ping a FILESERVER non ha successo.

**Metodologia di Risoluzione:**

1. **Verifica della risoluzione DNS:**
    
    - Il server DNS locale (192.168.1.5) dovrebbe risolvere FILESERVER, ma il ping fallisce. 
    - Accesso alla GUI web del server DNS tramite Browser-A.

2. **Controllo e aggiornamento del file di zona DNS:**    

    - Apertura della configurazione delle zone DNS (clab.local).        
    - Il file di zona contiene solo record NS e SOA, senza un record A per FILESERVER.
        
    - Aggiunta di un record A con i seguenti dettagli:
        
        - **Nome:** FILESERVER
        - **Indirizzo IPv4:** 192.168.1.20
        - **Record inverso (PTR):** Abilitato
        - **Zona inversa per PTR:** Abilitata
        
3. **Verifica della risoluzione DNS:**
    
    - Test del ping con `ping -c 4 FILESERVER.clab.local`, ora funzionante.
    
4. **Configurazione del dominio di ricerca su Linux-A:**
    
    - Per evitare di digitare il nome completo (FILESERVER.clab.local), si aggiunge `search clab.local` a `/etc/resolv.conf`:
    
        ```sh
        echo "search clab.local" >> /etc/resolv.conf
        ```
    
    - Verifica della modifica con `cat /etc/resolv.conf`.        
    - Test del ping a `FILESERVER`, ora risolto correttamente.
        
5. **Connessione SMB riuscita:**
    
    - Esecuzione di `smbclient -L FILESERVER -U cybrary`, con autenticazione tramite password `cybrary`.
    - Il server Samba risponde con l'elenco delle condivisioni disponibili.

**Conclusione:**  
Il problema era dovuto all'assenza di un record DNS per FILESERVER. Dopo aver aggiornato il DNS e configurato il dominio di ricerca su Linux-A, la connessione SMB è stata ristabilita con successo.

---

## **Problema di Connettività VPN tra host remoti**

**Problema:**  
L'utente su Linux-B (rete 10.10.10.0/24) non riesce a raggiungere FILESERVER (192.168.1.20) nella rete 192.168.1.0/24. La VPN IPsec che collega le due reti potrebbe essere la causa del problema.

**Metodologia di Risoluzione:**

1. **Verifica della risoluzione DNS:**
    
    - Il ping a FILESERVER fallisce con un errore di indirizzo errato.
    - Per evitare traffico DNS eccessivo sulla VPN, si aggiunge manualmente l'IP di FILESERVER al file `/etc/hosts` su Linux-B:
        
        ```sh
        echo "192.168.1.20 FILESERVER" >> /etc/hosts
        ```

	- Verifica della modifica con `cat /etc/hosts`.
	- Il ping a FILESERVER ora risolve correttamente il nome, ma la connessione è ancora bloccata.

> [!NOTE]  
> - Aggiungendo manualmente l'IP (192.168.1.20) e il nome dell'host (`FILESERVER`) nel file `/etc/hosts`, stai dicendo al sistema che quando cerca `FILESERVER`, deve usare l'indirizzo IP specificato (192.168.1.20) senza dover fare una richiesta a un server DNS. In pratica, `/etc/hosts` è una lista locale di nomi di host e indirizzi IP, che consente la risoluzione diretta e immediata dei nomi degli host senza coinvolgere un server DNS.
> 


2. **Controllo dello stato della VPN IPsec:**
    
    - Accesso alla GUI web di pfSense tramite Browser-B.
    - Navigazione su **Stato > IPsec** per controllare la connessione VPN.
    - Stato IPsec risulta **disconnesso**.

3. **Riconnessione della VPN:**
    
    - Premuto il pulsante **"Connetti P1 e P2"** per ristabilire il tunnel VPN.        
    - Dopo pochi secondi, la connessione VPN viene ripristinata con successo.

4. **Verifica della connettività:**
    
    - Nuovo test con `ping FILESERVER` da Linux-B, che ora risponde correttamente.

**Conclusione:**  
Il problema era dovuto alla disconnessione del tunnel VPN IPsec tra le due reti. Dopo aver aggiornato manualmente la risoluzione DNS su Linux-B e riattivato la VPN su pfSense, Linux-B è riuscito a connettersi correttamente a FILESERVER.

---
