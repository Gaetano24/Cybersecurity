## **Caratteristiche Fondamentali**

UDP è un protocollo di trasporto **senza connessione** e **non affidabile** che opera a livello 4 del modello OSI. 

A differenza di TCP, non fornisce:

- Controllo di flusso
- Controllo di congestione
- Ritrasmissione di pacchetti persi
- Riordinamento dei pacchetti
- Conferme di ricezione (ACK)

---

## **Header UDP (8 byte)**

![[Pasted image 20250507212838.png]]

---

## **Meccanismo del Checksum**

Il checksum UDP è calcolato su:
1. Pseudo-header (informazioni di IP)
2. Header UDP (porte, lunghezza)
3. Dati

**Calcolo**:
1. Divide i dati in parole da 16 bit
2. Somma tutte le parole (addizione in complemento a 1)
3. Aggiunge gli eventuali riporti al risultato
4. Calcola il complemento a 1 della somma


> [!NOTE]
>  Il checksum UDP è utile per errori casuali minori, ma non è adatto per applicazioni che richiedono affidabilità elevata o sicurezza. Le applicazioni critiche devono implementare meccanismi aggiuntivi (es. controlli a livello applicativo, ritrasmissioni selettive).


---

## **Vantaggi di UDP**

1. **Bassa latenza**: Nessun handshake iniziale (RTT=0)
2. **Overhead minimo**: Header di soli 8 byte
3. **Nessuna congestione**: Ideale per streaming live
4. **Broadcast/Multicast**: Supporto nativo
5. **Controllo applicativo**: Lo sviluppatore gestisce affidabilità se necessaria

---

## **Casi d'Uso Tipici**

| Applicazione | Porta | Perché UDP? |
|-------------|-------|-------------|
| DNS | 53 | Query/response singoli pacchetti |
| DHCP | 67/68 | Broadcast necessario |
| VoIP | 5060 | Tolleranza alla perdita |
| Videoconferenza | - | Bassa latenza critica |
| Giochi online | - | Stato continuo aggiornato |
| SNMP | 161 | Semplicità di implementazione |
| NTP | 123 | Temporizzazione precisa |

---

## **Estensioni e Protocolli su UDP**

1. **QUIC (HTTP/3)**: 
   - Aggiunge affidabilità a livello applicativo
   - Crittografia integrata
   - Multiplexing senza HOL blocking

2. **DTLS (TLS su UDP)**:
   - Fornisce sicurezza mantenendo i vantaggi di UDP
   - Usato in WebRTC

3. **Protocolli real-time**:
   - RTP (Real-time Transport Protocol)
   - RTCP (RTP Control Protocol)

---