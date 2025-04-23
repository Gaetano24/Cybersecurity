
### `/` – **Directory Root (principale)**

La **directory radice** è il punto di partenza di tutta la gerarchia del file system. Ogni altra cartella (inclusi dispositivi montati) esiste come sottodirectory di questa. Non contiene file veri e propri, ma funge da contenitore per tutte le altre cartelle necessarie al funzionamento del sistema.

---

### `/bin` – **Comandi base del sistema**

Contiene i **comandi eseguibili essenziali** accessibili sia dagli utenti normali che dall’amministratore (root). Sono strumenti di base come `cp`, `mv`, `rm`, `cat`, `grep`, `bash`, che servono per l’uso quotidiano e la manutenzione del sistema, anche in modalità di recupero.

> **Importante**: deve essere disponibile anche quando altri volumi non sono montati (es. `/usr`).

---

### `/boot` – **File di avvio del sistema operativo**

Ospita tutti i file necessari all’**inizializzazione del sistema**, come:

- Il kernel Linux (`vmlinuz`)
    
- Il file initrd/initramfs (immagine del disco RAM temporaneo usata all’avvio)
    
- File di configurazione del bootloader (`grub.cfg`)
    
- La directory `grub/` con i file necessari a GRUB (bootloader)
    

> Talvolta `/boot` risiede su una **partizione separata**, specialmente su sistemi dual-boot o con cifratura completa.

---

### `/dev` – **File dei dispositivi hardware**

Qui si trovano i cosiddetti **device files**, che rappresentano dispositivi fisici come:

- Dischi (`/dev/sda`, `/dev/nvme0n1`)
    
- Partizioni (`/dev/sda1`)
    
- Terminali (`/dev/tty`, `/dev/pts/`)
    
- File speciali (`/dev/null`, `/dev/random`)
    

I file in `/dev` sono gestiti dal **device manager** del sistema (`udev`) e permettono al kernel e agli utenti di comunicare con l'hardware.

---

### `/etc` – **Configurazioni di sistema e dei servizi**

Contiene **tutti i file di configurazione** globali del sistema, leggibili e modificabili manualmente (formato di testo).

Esempi:

- `/etc/passwd`: informazioni sugli utenti

- `/etc/fstab`: tabella dei file system da montare

- `/etc/hostname`: nome della macchina

- `/etc/ssh/`: configurazioni del server SSH

- `/etc/network/`: configurazioni di rete

- `/etc/netplan` :  contiene informazioni di rete sui moderni sistemi Linux

- `/etc/hosts` : è un file di testo semplice che consente al sistema di associare nomi di host ad indirizzi IP, senza consultare un server DNS.
  

> **Non contiene eseguibili**: solo configurazioni.

---

### `/home` – **Dati e configurazioni personali degli utenti**

Ogni utente normale (non root) ha la sua directory personale in `/home`, ad esempio:

- `/home/giovanni`
    
- `/home/lisa`
    

Contiene:

- File personali (documenti, immagini, ecc.)
    
- Configurazioni utente (in file e cartelle nascoste come `.bashrc`, `.config/`)
    

> L’utente **root** ha invece la sua home separata in `/root`.

---

### `/lib` – **Librerie condivise per i programmi base**

Ospita le **librerie (.so)** essenziali necessarie per l’esecuzione dei programmi in `/bin` e `/sbin`.  
Esempi:

- `/lib/x86_64-linux-gnu/` su sistemi 64 bit
    
- `/lib/modules/` contiene i moduli caricabili del kernel
    

---

### `/media` – **Montaggio automatico di dispositivi rimovibili**

Quando colleghi una chiavetta USB, un disco esterno o un CD/DVD, viene **montato automaticamente** in questa cartella, in una sottodirectory con il nome del dispositivo.

> Es: `/media/utente/NOME_CHIAVETTA`

---

### `/mnt` – **Montaggi manuali temporanei**

Utilizzata **manualmente dagli amministratori** di sistema per montare partizioni o dischi in modo temporaneo.

> Esempio: `mount /dev/sdb1 /mnt/usb`

---

### `/opt` – **Software di terze parti o pacchetti opzionali**

Questa cartella è pensata per contenere **applicazioni non standard**, come software commerciali, closed source o installati manualmente.  
Esempio: `/opt/google/chrome/`

---

### `/proc` – **Informazioni in tempo reale sul sistema**

Un file system virtuale che contiene **file dinamici** che rappresentano lo stato corrente del kernel, dei processi e dell’hardware. Ogni directory numerata rappresenta un processo attivo.

Esempi:

- `/proc/cpuinfo`: info sulla CPU
    
- `/proc/meminfo`: info sulla RAM
    
- `/proc/[PID]/`: directory per ogni processo attivo
    

> Nessun file qui occupa realmente spazio su disco.

---

### `/root` – **Home directory dell’utente root**

È la directory personale del **superutente (amministratore)**. Separata da `/home` per motivi di sicurezza e accesso.

> Accessibile solo da root o con permessi elevati.

---

### `/run` – **Dati temporanei del sistema in esecuzione**

Contiene informazioni volatili create **durante l’esecuzione del sistema**: socket, PID, mount temporanei.

> È una **tmpfs**: risiede in RAM e viene svuotata al riavvio.

---

### `/sbin` – **Comandi di amministrazione del sistema**

Contiene comandi simili a `/bin`, ma destinati a **task di sistema e manutenzione**, utilizzati soprattutto da root.

Esempi:

- `fsck`: controllo del file system
    
- `reboot`: riavvio del sistema
    
- `mount`: montaggio di dispositivi
    

---

### `/srv` – **Dati serviti da servizi di rete**

Contiene dati **esposti da server** come:

- `/srv/ftp/`: contenuti FTP
    
- `/srv/www/`: siti web ospitati localmente
    

> Non sempre utilizzata da default, ma utile su server.

---

### `/sys` – **Interfaccia virtuale al kernel (hardware e moduli)**

Un altro file system virtuale, che espone informazioni **hardware e moduli kernel** in una struttura ad albero.

> Usato da `udev`, `systemd`, strumenti di diagnostica e controllo del kernel.

---

### `/tmp` – **File temporanei delle applicazioni**

Spazio per file temporanei, spesso accessibile a tutti gli utenti.  
Molti sistemi lo **svuotano ad ogni riavvio** per liberare spazio.

---

### `/usr` – **Software utente, documentazione, librerie**

Contiene tutto ciò che è **non essenziale all’avvio**, ma fondamentale per il normale utilizzo del sistema.

Sottodirectory principali:

- `/usr/bin`: comandi e programmi standard (es. `nano`, `python`)
    
- `/usr/sbin`: comandi amministrativi non critici
    
- `/usr/lib`: librerie condivise
    
- `/usr/share`: documentazione, icone, localizzazione
    
- `/usr/include`: header file per sviluppo software

---

### `/var` – **Dati variabili (log, spool, cache)**

Directory per file **che cambiano frequentemente**, come:

- `/var/log/`: file di log di sistema e servizi
    
    - **`/var/log/dmesg`**  
	    Contiene i **messaggi del kernel** generati durante l'avvio e l'esecuzione.  
	    Utile per rilevare problemi hardware, driver o inizializzazione dei moduli.
    
	- **`/var/log/syslog`** (o `/var/log/messages` su alcune distro)
	    File di **log generale del sistema**: registra messaggi di sistema, servizi e demoni.  
	
	- **`/var/log/auth.log`**  
	    Tiene traccia degli **eventi legati all'autenticazione**, come login, sudo, SSH, fallimenti di accesso.  
	
	- **`/var/log/lastlog`**  
	    Registro binario che mostra **l’ultima connessione di ogni utente**.  Utilizzato dal comando `lastlog`.
	
	- **`/var/log/wtmp`**  
	    File binario che conserva uno **storico degli accessi e disconnessioni** degli utenti.  
	    Consultabile con il comando `last`.
	
- `/var/cache/`: cache dei pacchetti e browser
    
- `/var/spool/`: code di stampa o email
    
- `/var/tmp/`: file temporanei più persistenti rispetto a `/tmp`

---
