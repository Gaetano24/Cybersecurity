## **Configurazione Profili**

**Profilo**: è un insieme di configurazioni e impostazioni. In base al tipo di problema/protocollo (es. Problemi TCP) con cui ho a che fare potrei volere un certo set di colonne e regole di colorazioni, e filtri solo per quello specifico protocollo.

![[Pasted image 20250402172213.png]]

Tasto destro e clicchiamo su **_new_** per creare un nuovo profilo che andremo a personalizzare.

---

### **Configurazione layout**

**Come faccio a modificare il layout della mia interfaccia Wireshark?**

> [!NOTE]
> ```
> Edit > Preferences > Layout 
> 
> Posso selezionare uno dei layout presenti.
  
**Diagramma del pacchetto**: mostra il layout del frame e il layout del pacchetto. 
Per visualizzare i valori di ciascun campo fare tasto destro sul campo e cliccare su
**_show fields value**.

---

### **Aggiungere la colonna Delta Time**

Un'altra modifica utile da apportare è quella di inserire la colonna **Delta**:

> [!NOTE]
> Edit > Preferences > Columns
> 
>Delta (Title) - Delta time displayed (Type)

Nella colonna **delta** verrà visualizzato il tempo che intercorre tra un pacchetto e il pacchetto precedente (molto utile nelle operazioni di troubleshooting).


Il valore mostrato nella colonna **time** può essere configurato nel seguente modo:

> [!NOTE] 
> View > Time Display Format
> 
> Possiamo impostare cosa visualizzare nella colonna del tempo, ad esempio
> - I secondi passati dall'inizio della cattura
> - Time of Day: l'ora del giorno viene presa dall'orologio del mio sistema
> - UTC Time of Day

---

### **Regole di colorazione**

Ecco come impostare una nuova regola di colorazione:

> [!NOTE] Nuova regola di colorazione
> View > Coloring Rules > [+]
> 
> Dal tasto **background** è possibile selezionare il colore  


> [!NOTE] Esempio
> Name: TCP SYN
> Filter: tcp.flags.syn==1
> 
> Il flag **SYN** è usato nella **fase di handshake a tre vie** di TCP
> **Nota**: le regole vengono processate in ordine

---

### **Salvare un filtro di visualizzazione come pulsante** 

Wireshark permette di filtrare i pacchetti in tempo reale usando i **Display Filters**. Se usi spesso un filtro specifico (ad esempio `arp.opcode == 1`), puoi salvarlo come **pulsante personalizzato** per applicarlo rapidamente senza doverlo riscrivere ogni volta.

- Inserisci il filtro nella barra dei filtri (es. `arp.opcode == 1`).
- Clicca sull'**icona "+"** accanto alla barra del filtro.
- Dai un **nome** al pulsante.
- Clicca **OK** e il pulsante apparirà nella barra sopra la lista dei pacchetti.


![[Pasted image 20250402184649.png]]

---

### **Aggiungere e rimuovere colonne**

Un metodo veloce per inserire colonne nella nostra interfaccia è quello di selezionare un campo all'interno del pacchetto, come ad esempio **TCP Segment Len**, fare tasto destro e cliccare su **Apply as Column**:

![[Pasted image 20250402185252.png]]

Al contrario, per rimuovere una colonna basta fare tasto destro sulla colonna che vogliamo rimuovere e cliccare su **Remove this Column**.

---

