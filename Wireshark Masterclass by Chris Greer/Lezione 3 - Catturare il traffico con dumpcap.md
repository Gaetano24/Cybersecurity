
In questa lezione vedremo come catturare il traffico da linea di comando tramite uno strumento chiamato **dumpcap**.

Per visualizzare alcune delle opzioni che abbiamo a disposizione:

```
dumpcap -h
```

Per visualizzare la lista delle interfacce disponibili:

```
dumpcap -D
```

Questo comando mi restituirà l'elenco delle interfacce, ognuna associata ad uno specifico indice.

Per selezionare una specifica interfaccia per la cattura:

```
dumpcap -i <indice_interfaccia>
```

Questo comando mi restituirà la posizione del file di output ed il numero di pacchetti catturati in modo interattivo.

**Nota**: Per terminare la cattura premere CTRL+C

Per specificare la posizione in cui salvare l'output:

```
dumpcap -i <indice_interfaccia> -w <path>
```

dove *-w* sta per "write".

Come scrivere il traffico su un buffer ad anello (ring buffer):

```
dumpcap -i <indice_interfaccia> -w <path> -b filesize:500000 -b files:10
```

In questo caso abbiamo impostato:

- 500000: dimensione in kilobyte di ciascun file di cattura
- 10: dimensione del ring buffer





