## **Cosa rappresenta la colonna "Time" ?**

La colonna **Time** è fondamentale durante le analisi di rete e le indagini forensi.  
Per impostazione predefinita, questa colonna mostra un timer che parte dall'inizio della cattura, indicando per ogni pacchetto quanto tempo è trascorso rispetto all'avvio.

**Nota:** Se si stanno analizzando eventuali ritardi, è utile osservare questa colonna per individuare salti temporali significativi tra un pacchetto e l'altro.

Tuttavia, cosa succede se si verifica un problema alle 10:00 del mattino e si vuole sapere esattamente quando è accaduto?  
In questo caso, il formato predefinito della colonna **Time** potrebbe non essere sufficiente.

> [!NOTE] Come modificare il formato della colonna Time  
> **View > Time Display Format** 
> 
> Per scegliere un formato che mostri data e ora assolute, in modo da identificare con precisione il momento esatto di un evento. Usare le configurazioni UTC per evitare problemi di fuso orario.


> [!NOTE] Avviare un cronometro su uno specifico pacchetto
> 
> Ogni volta che desideri avviare un cronometro a partire da un determinato pacchetto per misurare il tempo trascorso fino a un altro pacchetto, puoi farlo facilmente cliccando con il tasto destro sul pacchetto da cui vuoi iniziare il conteggio e selezionare **`Set/Unset Time Reference`**.  In questo modo, la colonna **Time** verrà azzerata su quel pacchetto e i pacchetti successivi mostreranno il tempo trascorso rispetto a quel punto di riferimento.

---

## **Conversazioni simultanee**

Un altro aspetto molto importante da tenere in considerazione è la presenza di più conversazioni TCP simultanee.  
In questi casi, la colonna **Delta Time** (che mostra il tempo trascorso dall'ultimo pacchetto) può diventare fuorviante, perché i valori riportati potrebbero riferirsi a pacchetti appartenenti a conversazioni diverse.

Per risolvere questo problema:

![[Pasted image 20250408115401.png]]


> [!NOTE]
> 
> Transmission Control Protocol > Timestamps > Time since previous frame in this TCP Stream > Apply as Column


![[Pasted image 20250408121109.png]]

In questa nuova colonna troveremo i valori delta calcolati tra pacchetti della stessa conversazione.

---
