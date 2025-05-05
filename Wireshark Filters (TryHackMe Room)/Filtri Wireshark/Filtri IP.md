### **Filtrare per indirizzi IP**

I **filtri dell'indirizzo IP**, o dell'intervallo di indirizzi, sono due dei filtri più comuni che utilizzerai. 

In Wireshark, possiamo filtrare per:

- Un indirizzo specifico
- Una sottorete
- Una conversazione
- Un intervallo di indirizzi


> [!NOTE]
> Wireshark ti aiuta a creare questi filtri mentre li costruisci. È possibile iniziare inserendo  `ip` (senza virgolette) nella barra del filtro del display e osservando le possibili opzioni.


![[Pasted image 20250503130937.png]]

---

### **Tipi di filtri IP più comuni**

1. **Indirizzo IP specifico**:
    
    - **Sorgente**: `ip.src == 10.10.10.1`
    - **Destinazione**: `ip.dst == 10.10.10.1`
    - **Qualsiasi direzione**: `ip.addr == 10.10.10.1`
    
2. **Sottorete**:
    
    - `ip.addr == 10.10.10.0/24`

---

### **Filtri di conversazione (tra 2 IP)**

﻿Un altro tipo comune di filtro IP è un filtro di conversazione in cui entrambi gli endpoint sono specificati nel filtro. Questo è quando entrambi gli endpoint sono specificati nel filtro.    


> [!NOTE] Generazione automatica
> Tasto destro su un pacchetto → `Filtro di conversazione` → `IP`


![[Pasted image 20250503131448.png]]

Questo creerà e applicherà automaticamente un filtro per i due endpoint nel pacchetto selezionato. Il filtro utilizzerà `ip.addr` per visualizzare il traffico in entrambe le direzioni per ciascun endpoint e l'operatore `and` per garantire che entrambe le condizioni del filtro siano soddisfatte (entrambi gli IP sono nello stesso pacchetto).

---
### **Operatori logici**

| Italiano | Simbolo | Inglese |
| -------- | ------- | ------- |
| e        | `&&`    | `and`   |
| o        | `       |         |
| non      | `!`     | `not`   |
| uguale   | `==`    | `eq`    |

> [!NOTE]
> Gli operatori possono essere usati in modo intercambiabile
> 
> Es. `==` è equivalente a `eq`

---

