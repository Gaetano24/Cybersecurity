
In questa lezione non parleremo di dove posizionare l'analizzatore (questo verrà trattato successivamente) ma parleremo specificamente delle interfacce visualizzabili quando si va a catturare il traffico con Wireshark, cosa significano e come usarle sulla riga di comando.

Affinché Wireshark catturi il traffico, deve usare un driver di pacchetti.

> [!NOTE] Per visualizzare il driver in uso:
> 
> Su Mac OS:
> Wireshark > About Wireshark
> 
> Su Linux/Windows:
> Help > About Wireshark

Il driver mi consente di portare quei pacchetti nel mio analizzatore e catturarli.

---

### **Configurazione interfacce di cattura**

Cliccando su **Capture Options**, è possibile visualizzare l'elenco delle interfacce di rete e configurare alcuni parametri di acquisizione:

![[Pasted image 20250403114708.png]]

---

#### **Input**

- **Snaplen**: definisce la quantità di dati catturati per ciascun frame. Se non è necessario acquisire l'intero payload, è possibile impostare un valore inferiore per ottimizzare le risorse. Tuttavia, è importante assicurarsi di non troncare informazioni essenziali.

- **Buffer**: indica la dimensione del buffer del kernel riservato alla cattura. Nel caso mostrato, il valore è impostato a 2 MB, una scelta generalmente adeguata. Tuttavia, in ambienti con traffico di rete molto elevato, potrebbe essere necessario aumentarlo.

- **Enable promiscuous mode**: permette a Wireshark di intercettare non solo il traffico destinato o generato dalla macchina locale, ma anche i pacchetti unicast tra altri dispositivi sulla rete.

---

#### **Output**

Questa finestra consente di configurare la destinazione in cui Wireshark salverà le catture e di impostare diversi parametri che possono migliorare la leggibilità del traffico acquisito.

![[Pasted image 20250403121729.png]]

- **File**: consente di specificare il percorso in cui salvare i file di traccia della cattura.

- **Deadline**: permette di definire criteri per l'interruzione automatica della cattura, in base a tempo trascorso, numero di pacchetti o dimensione del file. Ad esempio, è possibile impostare un limite massimo di 500 MB per ogni file di traccia.

- **Ring buffer**: abilita la scrittura ciclica su più file, eliminando i più vecchi quando si raggiunge il numero massimo specificato. Questa funzione è utile per catture prolungate senza esaurire lo spazio su disco.

---