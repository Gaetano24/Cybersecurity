
Per prima cosa, è necessario scaricare i database GeoIP forniti da MaxMind al seguente link:   [MaxMind – GeoLite2 Free Geolocation Data](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data/?lang=en)

I database da scaricare sono tre: 
- **ASN**
- **Country** 
- **City**.

---

## **Configurazione database**

Una volta scaricati i database, apri Wireshark e segui questi passaggi per configurarli:

1. Vai su **Edit** > **Preferences**
2. Nel menu a sinistra, seleziona **Name Resolution**    
3. Clicca su **MaxMind database directories** e poi su **Edit**
4. Inserisci il percorso in cui hai salvato i tre database

Dopo aver completato la configurazione, puoi tornare all’elenco dei pacchetti catturati.

---

## **Come utilizzare le funzionalità di GeoIP**

1. Seleziona un pacchetto dall’elenco
2. Nella finestra dei dettagli del pacchetto, espandi la sezione **Internet Protocol Version (IP)**    
3. Qui troverai il campo **Source GeoIP**, che ti mostrerà la posizione geografica dell'indirizzo IP sorgente e diverse informazioni come latitudine e longitudine

---

### **Mappa degli indirizzi IP**

Wireshark offre una funzionalità molto utile per visualizzare graficamente la posizione geografica degli endpoint (indirizzi IP sorgente e destinazione) attraverso una **mappa interattiva**. 

#### Come accedere alla mappa:

1. Vai su **Statistics** > **Endpoints**
2. Nella finestra che si apre, seleziona la tab **IPv4** o **IPv6**, in base al tipo di traffico
3. In basso, clicca su **Map** (o sull’icona a forma di mappamondo)

#### Cosa puoi fare nella mappa:

- Visualizzare gli **endpoint IP geolocalizzati**
- Esplorare la **distribuzione geografica** dei dispositivi coinvolti nella comunicazione
- Capire a colpo d’occhio da dove proviene (o dove va) il traffico analizzato
- Fare **click sugli endpoint** per ottenere informazioni più dettagliate (IP, numero di pacchetti, etc.)

---

### **Filtrare i pacchetti per posizione geografica**

Per filtrare i pacchetti usando una specifica posizione geografica seguire i seguenti passaggi:

1. Seleziona un pacchetto dall’elenco
2. Nella finestra dei dettagli del pacchetto, espandi la sezione **Internet Protocol Version (IP)**    
3. Qui troverai il campo **Source GeoIP**, che ti mostrerà la posizione geografica dell'indirizzo IP sorgente e diverse informazioni come latitudine e longitudine
4. Click destro e selezionare l'opzione **Prepare as Filter** 

Esempio:  `ip.geoip.src_city == "Moscow"`

---


