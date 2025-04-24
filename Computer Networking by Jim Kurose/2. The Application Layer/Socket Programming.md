
## 🧠 **Programmazione Socket**

Una **socket** è un punto finale di una comunicazione bidirezionale tra due macchine su una rete. Viene utilizzata per creare connessioni client-server.

Le socket possono usare due principali protocolli di trasporto:

- **TCP (Transmission Control Protocol)**
    
- **UDP (User Datagram Protocol)**


![[Pasted image 20250424123356.png]]

---

## 🔍 **Differenza tra TCP e UDP**

|Caratteristica|TCP|UDP|
|---|---|---|
|Tipo di connessione|Orientato alla connessione|Senza connessione|
|Affidabilità|Alta (garantisce l’ordine e la consegna)|Bassa (nessuna garanzia)|
|Velocità|Più lento|Più veloce|
|Uso tipico|Web, email, file transfer|Streaming, DNS, giochi online|

---

## 📦 **Socket TCP in Python**


![[Pasted image 20250424123533.png]]

### ✅ Server TCP

```python
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('localhost', 12345))
server.listen(1)
print("Server in attesa di connessioni...")

while True:
    conn, addr = server.accept()
    print(f"Connesso da {addr}")
    data = conn.recv(1024).decode()
    if not data:
        break
    print(f"Ricevuto: {data}")
    conn.send("Messaggio ricevuto!".encode())
    conn.close()
```

### ✅ Client TCP

```python
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(('localhost', 12345))
client.send("Ciao server!".encode())
response = client.recv(1024).decode()
print(f"Risposta dal server: {response}")
client.close()
```

---

## **📦 Socket UDP in Python**


![[Pasted image 20250424123455.png]]

### ✅ Server UDP

```python
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server.bind(('localhost', 12345))
print("Server UDP in ascolto...")

while True:
    data, addr = server.recvfrom(1024)
    print(f"Ricevuto '{data.decode()}' da {addr}")
    server.sendto("Risposta ricevuta!".encode(), addr)

```

### ✅ Client UDP

```python
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
client.sendto("Messaggio UDP!".encode(), ('localhost', 12345))
data, addr = client.recvfrom(1024)
print(f"Risposta: {data.decode()}")
```

---

## 🧩 **Quando usare TCP vs UDP**

- **Usa TCP**: quando è importante che i dati arrivino integri e ordinati (es. login, pagamenti).
    
- **Usa UDP**: quando serve velocità e una perdita occasionale è accettabile (es. videochiamate, giochi).


---
