## **1. Navigazione**

---
### **Informazioni utili all'avvio del terminale**

Quando apri il terminale, puoi visualizzare alcune informazioni importanti nella riga di comando:

- **User (Utente)**: è la prima parola che compare.  
    Esempio: `cybrary`

- **Host name (Nome host)**: si trova subito dopo il carattere `@` ed è il nome del computer o del sistema.  
    Esempio: `linux` oppure `ip-10-...`

- **Directory corrente**: è il percorso visualizzato dopo i due punti `:` e Indica in quale cartella ti trovi attualmente.  
    Esempio: `~/Desktop` oppure `/home/cybrary/Desktop`

---

### **Significato dei simboli**

- **`~` (tilde)**: rappresenta la **home directory** dell’utente.  
    Per l’utente `cybrary`, `~` equivale a `/home/cybrary`.

- **`$`**: indica che stai operando **come utente normale** (non root).  
    Se fossi root, vedresti invece il simbolo `#`.

---


![[Pasted image 20250409174534.png]]

Nell’esempio mostrato:

- **User**: `cybrary`
- **Host name**: `linux`
- **Directory corrente**: `~/Desktop`, che è equivalente a `/home/cybrary/Desktop`

> **Nota**: `~` è un'abbreviazione della home directory dell’utente attivo.  
> Quindi, `~/Desktop` è la stessa cosa di `/home/cybrary/Desktop` nel caso dell’utente `cybrary`.

---

### **Comandi utili**

#### **`whoami`** – Mostra il nome dell’utente attualmente connesso

Il comando `whoami` restituisce il nome dell'utente che ha effettuato l'accesso alla sessione corrente.

**Sintassi**:

```bash
whoami
```

**Esempio di output**:

```bash
cybrary
```

In questo esempio, l'utente attualmente connesso si chiama **cybrary**.

---

#### **`hostname`** – Mostra il nome della macchina

Il comando `hostname` restituisce il nome dell'host (identificativo del sistema) che è stato assegnato al computer o server. Questo nome viene usato per identificare il sistema sulla rete.

**Sintassi**:

```bash
hostname
```

**Esempio di output**:

```bash
linux
```

o

```bash
ip-10-...  # in caso di sistema su cloud
```

In questo esempio, il nome della macchina è **linux**, ma in un ambiente cloud potrebbe essere qualcosa come **ip-10-...**, che rappresenta l'indirizzo IP assegnato.

---

#### **`pwd`** – Mostra la directory corrente

Il comando `pwd` (print working directory) mostra il percorso completo della directory in cui ti trovi al momento nel filesystem.

**Sintassi**:

```bash
pwd
```

**Esempio di output**:

```bash
/home/cybrary/Desktop
```

In questo esempio, la directory corrente è **`/home/cybrary/Desktop`**.

---

#### **`id`** – Mostra l’ID dell’utente, il gruppo primario e i gruppi a cui appartiene

Il comando `id` fornisce informazioni sull'utente attualmente connesso, come l'**ID dell'utente** (UID), l'**ID del gruppo primario** (GID), e l'elenco degli **ID dei gruppi** a cui l'utente appartiene.

**Sintassi**:

```bash
id
```

**Esempio di output**:

```bash
uid=1001(cybrary) gid=1001(cybrary) groups=1001(cybrary),27(sudo)
```

In questo esempio:

- **UID**: L'ID dell'utente **cybrary** è 1001.
- **GID**: Il gruppo primario a cui appartiene è **cybrary** (GID 1001).
- **Groups**: L'utente appartiene anche al gruppo **sudo** (GID 27), che permette di eseguire comandi con privilegi di superutente.


![[Pasted image 20250409181054.png]]

---

### **Utente standard e identificativo (UID)**

In Linux, gli account utente **non di sistema** (cioè utenti normali, non root) iniziano solitamente con un **UID (User ID)** pari a **1000** o superiore.

Nel nostro caso, l’utente `cybrary` ha **UID 1001**, il che conferma che si tratta di un **utente standard**.

Inoltre, ogni utente ha un **gruppo primario** che porta lo **stesso nome dell’utente**.  
Quindi, l’utente `cybrary` appartiene automaticamente anche al gruppo `cybrary`.

---

### **Altri comandi utili per la navigazione del filesystem**

#### **`cd`** – Cambia directory

Il comando `cd` (change directory) viene utilizzato per spostarsi tra le directory nel filesystem.

##### **Varianti di `cd`**

- **`cd [directory]`** → Cambia la directory corrente a quella specificata.
   
- **`cd ../..`** → Torna indietro di due livelli nella gerarchia delle cartelle.

- **`cd ~`** → Torna direttamente alla **home directory** dell'utente.

---

#### **`ls`** – Elenco dei file nella directory corrente

Il comando `ls` (list) mostra i file e le directory presenti nella directory corrente.

##### **Varianti di `ls`**

- **`ls`** → Mostra un elenco di tutti i file e le cartelle nella directory corrente.

- **`ls -l`** → Mostra l’elenco in **dettaglio**, con informazioni come permessi, proprietario, dimensioni e data dell'ultima modifica.

- **`ls -a`** → Mostra **tutti** i file, inclusi quelli **nascosti** (quelli che iniziano con un punto `.`).

- **`ls -la`** → Combina le opzioni `-l` (dettaglio) e `-a` (mostra file nascosti), visualizzando tutti i file con dettagli.
 
- **`ls -R`** → Mostra i file e le directory in modo **ricorsivo** (mostra anche il contenuto delle sottodirectory).

---

## **2. Permessi in Linux**

---
### **Cosa sono e a chi vengono applicati?**

In Linux, i permessi di un file o di una cartella sono rappresentati da una stringa di **9 caratteri**, divisi in 3 set di 3 caratteri ciascuno. I permessi sono:

- **`r`** (read): Permesso di lettura
    
- **`w`** (write): Permesso di scrittura
    
- **`x`** (execute): Permesso di esecuzione
    
- **`-`**: Significa che il permesso non è concesso


Questi permessi vengono applicati a tre categorie di utenti:

1. **Proprietario (Owner)**: Il primo set di 3 caratteri
    
2. **Gruppo (Group)**: Il secondo set di 3 caratteri
    
3. **Altri utenti (Others)**: Il terzo set di 3 caratteri

#### **Esempio di permessi per la directory `/home/cybrary/Desktop`**

Nel caso della directory `/home/cybrary/Desktop`, i permessi per l'utente `cybrary` e gli altri gruppi e utenti potrebbero essere:

```
rwx r-x r-x
```

- **`rwx`** per il proprietario (`cybrary`):  
	L'utente `cybrary` ha il permesso di **leggere**, **scrivere** ed **eseguire** (modificare e entrare nella cartella).

- **`r-x`** per il gruppo (`cybrary`):  
    Il gruppo a cui appartiene l'utente `cybrary` ha il permesso di **leggere** ed **eseguire**, ma non può modificare (scrivere) i file nella directory.

- **`r-x`** per tutti gli altri utenti (others):  
    Gli utenti esterni al gruppo `cybrary` hanno il permesso di **leggere** ed **eseguire**, ma non possono modificare i contenuti.

---

### **Come leggere i permessi**

Supponiamo che vediamo un output di `ls -l` così:

```bash
drwxr-xr-x  2 cybrary cybrary 4096 Apr  9 12:45 Desktop
```

La stringa **`drwxr-xr-x`** rappresenta:

- **d**: Indica che si tratta di una **directory** (se fosse un file normale, sarebbe un `-` al posto della `d`).

- **rwx**: Il proprietario (utente `cybrary`) ha permessi di lettura, scrittura ed esecuzione.

- **r-x**: Il gruppo (ancora `cybrary`) ha permessi di lettura ed esecuzione, ma non scrittura.

- **r-x**: Tutti gli altri utenti hanno permessi di lettura ed esecuzione, ma non scrittura.

---

### **Sintesi**

- **`rwx`**: Lettura, scrittura ed esecuzione
    
- **`r-x`**: Lettura ed esecuzione (senza scrittura)
    
- **`---`**: Nessun permesso

---

### **Tipi di File e Directory**

- **`d`** → Directory
    
- **`-`** → File normale
    
- **`l`** → Link simbolico (soft link) 


> Un **link simbolico** (o **symlink**) è un tipo di **riferimento** a un altro file o directory nel sistema. In pratica, è come un "collegamento" che punta a un altro file o directory.

---

## **3. File Operations**

Ecco una panoramica dei principali comandi di gestione dei file in Linux, con spiegazioni e note sui comportamenti più importanti:

---
### **`mkdir`** - Creare directory

Il comando `mkdir` (make directory) viene utilizzato per creare una o più directory.

**Sintassi**:

```bash
mkdir directory_name
```

Per creare più directory in una volta, basta separarli con uno spazio:

```bash
mkdir directory1 directory2 directory3
```

---

### **`touch`** - Creare file vuoti

Il comando `touch` viene utilizzato per creare file vuoti o per aggiornare la data di accesso e modifica di un file esistente.

**Sintassi**:

```bash
touch file_name
```

Ad esempio:

```bash
touch file1.txt
```

---

### **Redirezione dell'output: `>` vs `>>`**

- **`>>` (append)**: Aggiunge (append) testo alla fine di un file esistente. Se il file non esiste, viene creato.
    
    **Esempio**:
    
    ```bash
    echo "This is file 1" >> file1.txt
    ```


- **`>` (overwrite)**: Sovrascrive il contenuto di un file esistente con nuovo testo. Se il file non esiste, viene creato.
    
    **Esempio**:
    
    ```bash
    echo "This is file 1" > file1.txt
    ```


In sintesi:

- `>>` aggiunge contenuto.
- `>` sovrascrive il contenuto.

---

### **`cat`** - Visualizzare contenuti di un file

Il comando `cat` (concatenate) viene usato per visualizzare il contenuto di un file sul terminale.

**Sintassi**:

```bash
cat file_name
```

---

### **`more` e `less`** - Visualizzare contenuti di un file con scorrimento

- **`more`**: Permette di visualizzare il contenuto di un file pagina per pagina.
    
    **Sintassi**:
    
    ```bash
    more file_name
    ```


- **`less`**: Come `more`, ma con la possibilità di scorrere indietro nel file. È generalmente più potente di `more`.
    
    **Sintassi**:
    
    ```bash
    less file_name
    ```


---

### **`file`** - Determinare il tipo di file

Il comando `file` viene utilizzato per determinare il tipo di contenuto di un file, indipendentemente dall'estensione.

**Sintassi**:

```bash
file file_name
```

Ad esempio:

```bash
file document.txt
```

> **Nota**: In Linux, non è obbligatorio aggiungere un'estensione ai file. Le estensioni sono solo una convenzione per aiutare gli utenti a comprendere il contenuto del file.

---

### **`cp`** - Copiare file o directory

Il comando `cp` (copy) viene utilizzato per copiare file o directory da una posizione a un'altra.

**Sintassi**:

```bash
cp source_file destination
```

Ad esempio:

```bash
cp file1.txt /home/cybrary/Documents/
```

Per copiare una directory, devi usare l'opzione `-r` (ricorsiva):

```bash
cp -r directory_name /path/to/destination/
```

---

### **`rm`** - Rimuovere file e directory

Il comando `rm` (remove) serve per eliminare file o directory. **Attenzione**: senza l'opzione `-i`, i file vengono eliminati immediatamente senza conferma, il che può essere rischioso perché Linux non ha un cestino come Windows.

Con l'opzione `-i`, il comando chiede conferma prima di rimuovere il file:

**Sintassi**:

```bash
rm -i file_name
```

**Esempio**:

```bash
rm -i file1.txt
```

> **Nota**: Senza l'opzione `-i`, il file verrebbe eliminato senza chiedere conferma. È sempre meglio usare `-i` per evitare eliminazioni accidentali.

---

### **`mv`** - Muovere o rinominare file e directory

Il comando `mv` (move) viene utilizzato per spostare file o directory da una posizione all'altra, o per rinominarli.

**Sintassi**:

```bash
mv source_file destination
```

Per rinominare un file:

```bash
mv old_name.txt new_name.txt
```

Per spostare un file in una directory:

```bash
mv file1.txt /home/cybrary/Documents/
```

---

### **`base64` – Codifica dati in formato leggibile**

Converte dati binari in una rappresentazione testuale leggibile, utile per garantire compatibilità e stampa.

**Esempio**:

```bash
cat file.bin | base64
```

---

### **`|` (pipe) – Collega comandi tra loro**

Usato per passare l’output di un comando come input per un altro.

**Esempio**:

```bash
cat file.txt | sort
```

---

### **`find` – Cerca file o directory nel filesystem**

Permette di cercare file o directory in base a nome, tipo, estensione, data, dimensione, ecc...

**Esempio**:

```bash
find . -name "*.txt"
```

**Con filtro errori**:

```bash
find . -name "*.txt" 2>/dev/null
```


> [!NOTE]
> Il `2>/dev/null` **reindirizza gli errori (descrittore 2)** verso `/dev/null` (una sorta di “cestino” del sistema), così non vengono mostrati a schermo.

---

### **`grep` – Cerca testo all’interno di file o output**

Il comando `grep` (**Global Regular Expression Print**) serve per **cercare righe che contengono una determinata parola o espressione** all’interno di un file o di un output.

```bash
grep parola file.txt
```

Questo comando cerca la parola indicata (es. `parola`) all’interno del file `file.txt` e **mostra solo le righe che la contengono**.

**Opzioni utili**:

- **`-i`** → ignora le maiuscole/minuscole
- **`-n`** → mostra anche il numero di riga`
- **`-r`** o **`-R`** → cerca ricorsivamente nelle sottocartelle


**Esempio**:

```bash 
grep r "testo" 
```

In questo esempio il comando `grep` cerca **tutte le occorrenze della parola "testo"** **all’interno dei file** della **directory corrente** e **in tutte le sottocartelle**, in modo **ricorsivo**.

---

### **`sort` – Ordina righe di testo**

Ordina le righe di un file (o di un output) in ordine alfabetico o numerico.

**Esempio**:

```bash
cat file.txt | sort
```

---

### **`uniq` – Rimuove righe duplicate**

Filtra le righe duplicate (richiede che l’input sia ordinato per funzionare correttamente).

**Esempio**:

```bash
cat file.txt | sort | uniq
```

---

### **`wc` – Conta righe, parole o caratteri**

Conta righe, parole o caratteri in un file o output.

**Esempi**:

- Tutto (righe, parole, byte):
    
    ```bash
    cat file.txt | wc
    ```
    
- Solo parole:
    
    ```bash
    cat file.txt | wc -w
    ```
    
- Righe uniche:
    
    ```bash
    cat file.txt | sort | uniq | wc -l
    ```
    

---

