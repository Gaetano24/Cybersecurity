Fonte: https://www.youtube.com/watch?v=15amNny_kKI

**IPSec** è un **gruppo di protocolli** che funzionano insieme. Il loro scopo è quello di creare tunnel di rete sicuri attraverso reti non sicure. Ad esempio, collegando due reti sicure, o più specificamente i loro router, chiamati anche **peer**, attraverso la rete Internet pubblica. 

- IPSec fornisce l'**autenticazione** in modo che solo i peer che si conoscono tra loro e che possono autenticarsi reciprocamente possano connettersi. 
- Tutto il traffico trasportato dai protocolli IPSec è **crittografato**.

## **Architettura**

Componenti fondamentali sono:

- **Rete insicura**: Una rete che non offre garanzie di sicurezza per la trasmissione dei dati, come Internet o una rete aziendale non protetta. In IPsec, la rete insicura è il mezzo attraverso il quale viaggiano i pacchetti crittografati tra due endpoint sicuri.
    
- **Tunnel VPN IPsec**: Una connessione criptata creata utilizzando il protocollo IPsec per proteggere il traffico tra due dispositivi o reti. Il tunnel incapsula e cifra i pacchetti IP, garantendo riservatezza, integrità e autenticazione tra le parti coinvolte.
    
- **Traffico interessante**: Il traffico di rete che soddisfa criteri predefiniti (ad esempio, specifici indirizzi IP, protocolli o porte) e deve essere protetto da IPsec. 

Nonostante i tunnel utilizzino la rete Internet pubblica, i dati che transitano attraverso questo tunnel sono crittografati, quindi mentre transitano su questa rete non sicura sono protetti.

![[Pasted image 20250330193756.png]]

---

## **Funzionamento**

IPsec si basa su due fasi principali:

- **IKE (Internet Key Exchange) Phase 1**: è la fase iniziale del processo, caratterizzata da operazioni più complesse e dispendiose in termini di tempo e risorse. Durante questa fase si stabiliscono i parametri di sicurezza tra le due parti.
    
    - **Autenticazione**: i dispositivi coinvolti si autenticano reciprocamente utilizzando chiavi precondivise (PSK) o certificati digitali.
        
    - **Crittografia asimmetrica**: viene impiegata per negoziare e generare in modo sicuro una chiave simmetrica, che sarà utilizzata nella seconda fase per cifrare il traffico dati.
        
    - **IKE Security Association (IKE SA)**: al termine della fase 1, viene stabilita un'Associazione di Sicurezza (SA), creando un "tunnel di fase 1" attraverso cui avverranno ulteriori negoziazioni per la protezione del traffico dati.


- **IKE (Internet Key Exchange) Phase 2**: è la fase più veloce ed efficiente del processo, poiché si basa sui parametri di sicurezza già negoziati nella fase 1.
    
    - **Uso delle chiavi della fase 1**: le chiavi generate durante la fase 1 vengono utilizzate per proteggere la comunicazione della fase 2.
        
    - **Accordo sui metodi di crittografia**: le due parti concordano sugli algoritmi di crittografia e autenticazione per proteggere il traffico dati. La chiave simmetrica generata viene utilizzata per cifrare i dati trasferiti in blocco.
        
    - **Creazione dell'IPsec Security Association (IPsec SA)**: al termine della fase 2, viene stabilita un'Associazione di Sicurezza IPsec (IPsec SA), che definisce un "tunnel di fase 2" attraverso il quale transiterà il traffico protetto.

La suddivisione in due fasi è necessaria perché consente di mantenere attivo il tunnel della fase 1 anche quando il tunnel della fase 2 viene chiuso per inattività. In questo modo, se successivamente si verifica nuovo traffico interessante, la creazione di un nuovo tunnel di fase 2 sarà molto più rapida ed efficiente, evitando di ripetere l'intero processo di negoziazione della fase 1.

### **IKE Phase 1**

![[Pasted image 20250330193651.png]]

1. **Autenticazione**: le due parti si autenticano reciprocamente utilizzando certificati digitali o una chiave precondivisa (PSK).
2. **Generazione della chiave privata DH**: ciascuna parte crea una chiave privata utilizzando l'algoritmo Diffie-Hellman (DH).    
3. **Derivazione della chiave pubblica DH**: ogni parte calcola la propria chiave pubblica a partire dalla chiave privata generata.
4. **Scambio delle chiavi pubbliche**: le due parti si inviano reciprocamente le chiavi pubbliche attraverso la rete pubblica.
5. **Generazione della chiave condivisa DH**: ciascuna parte combina la propria chiave privata con la chiave pubblica ricevuta dall'altra, generando così la stessa chiave Diffie-Hellman condivisa.
6. **Negoziazione dei parametri di sicurezza**: la chiave Diffie-Hellman condivisa viene utilizzata per proteggere lo scambio del materiale crittografico e degli algoritmi da usare (ad esempio, algoritmi di crittografia e autenticazione).
7. **Derivazione della chiave simmetrica**: entrambe le parti utilizzano la chiave Diffie-Hellman e il materiale negoziato per calcolare una chiave simmetrica condivisa.
8. **Protezione del tunnel IKE Phase 1**: questa chiave simmetrica viene impiegata per crittografare tutto il traffico che passa attraverso il tunnel di fase 1, noto come **IKE Security Association (IKE SA)**.

### **IKE Phase 2**

![[Pasted image 20250330193557.png]]

Ecco una versione migliorata e più chiara del testo:

1. La **chiave simmetrica condivisa** viene utilizzata per cifrare e decifrare le informazioni scambiate tra i peer, comprese le negoziazioni sui parametri di sicurezza. Uno dei peer comunica all’altro l’elenco delle **suite crittografiche supportate**, ovvero i metodi di crittografia e integrità che può eseguire.
2. L’altro peer seleziona i metodi migliori tra quelli proposti, li comunica e li conferma. Da quel momento, gli algoritmi concordati verranno utilizzati per proteggere la comunicazione.
3. La chiave Diffie-Hellman (DH) e il materiale negoziato vengono utilizzati da entrambe le parti per generare una **chiave simmetrica dedicata alla protezione dei dati (IPsec Key)**, progettata per il trasferimento sicuro su larga scala.
4. L’**IPsec Key** viene quindi utilizzata per cifrare e decifrare il **traffico interessante** all’interno del tunnel VPN IPsec.

In ogni **tunnel di fase 1**, vengono stabilite **due associazioni di sicurezza (Security Associations - SA), una per ciascuna direzione di comunicazione**. Queste SA garantiscono la protezione dei dati trasferiti tra le reti collegate dalla VPN.

---

## **Policy-Based & Route-Based VPNs**

- **Policy-Based VPN**:  
    
    Con le VPN basate su policy, il traffico viene instradato nel tunnel in base a regole di sicurezza predefinite. Ogni policy specifica quale traffico deve essere crittografato e instradato attraverso il tunnel, creando una **coppia di Security Associations (SA)** per ogni direzione del traffico. Questo consente di applicare regole diverse per tipi di traffico differenti, offrendo maggiore controllo ma richiedendo una configurazione più complessa.
    
- **Route-Based VPN**:  

    Le VPN basate su routing utilizzano **prefissi di rete** per determinare quale traffico deve essere inviato attraverso il tunnel. Ad esempio, si può configurare una rotta per inviare tutto il traffico destinato alla rete **192.168.0.0/24** attraverso la VPN. Questo approccio utilizza **una singola coppia di Security Associations (SA) per ogni prefisso di rete**, semplificando la configurazione e la gestione. Sebbene offra meno granularità nel controllo del traffico, è una soluzione più flessibile e adatta a scenari complessi, specialmente quando si utilizza il routing dinamico.


	![[Pasted image 20250330195959.png]]
