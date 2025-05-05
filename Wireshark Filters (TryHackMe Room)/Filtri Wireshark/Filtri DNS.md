### **Richieste e risposte DNS**

- **Tutte le query DNS (richieste)**:  
    `dns.flags.response == 0`
    
- **Tutte le risposte DNS**:  
    `dns.flags.response == 1`


![[Pasted image 20250505141731.png]]


- **Nome richiesto (es. dominio richiesto)**:  
    `dns.qry.name == "www.tryhackme.com"`  
    (oppure trascina il nome dal campo nella barra filtro)
    
- **Aggiungere `dns.qry.name` come colonna**:  
    Clic destro sul campo → **"Applica come colonna"**


![[Pasted image 20250505141756.png]]

---

### **Filtrare per contenuto nel nome**

- **Contiene stringa (case-sensitive)**:  
    `dns.qry.name contains hack`
    
- **Regex case-insensitive**:  
    `dns.qry.name matches hack`  
    (usa espressioni regolari Perl-like)
    

---

### **Tipi di record DNS comuni**

|Tipo|ID|Descrizione|
|---|---|---|
|A|1|IPv4 address|
|AAAA|28|IPv6 address|
|CNAME|5|Nome canonico / alias|
|PTR|12|Reverse lookup (IP → nome)|
|SOA|6|Inizio autorità (authoritative server)|
|AXFR|252|Trasferimento di zona|

**Filtro per tipo di query**:   `dns.qry.type == <ID>`  

Esempio per record A (IPv4):   `dns.qry.type == 1`

---

