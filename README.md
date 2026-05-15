# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.py

## PROGRAM - ARP
## Server.py
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Waiting for client...")
c, addr = s.accept()
print("Connected to", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    print("IP received:", ip)
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()
```
## Client.py
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```
## OUTPUT - ARP
## Server side
<img width="885" height="204" alt="Screenshot 2026-05-15 135923" src="https://github.com/user-attachments/assets/2a28283e-c4cc-4702-90c7-7593fa5d83ce" />
## Client side
<img width="889" height="245" alt="Screenshot 2026-05-15 135953" src="https://github.com/user-attachments/assets/1776a210-bdf6-44d6-81c7-414d1681af4d" />

## PROGRAM - RARP
## Server.py
```
import socket
s=socket.socket()
s.bind(('localhost',9000))
s.listen(5)
c,addr=s.accept()
address={"6A:08:AA:C2":"192.168.1.100","8A:BC:E3:FA":"192.168.1.99"};
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## Client.py
```
import socket
s=socket.socket()
s.connect(('localhost',9000))
while True:
    ip=input("Enter MAC Address : ")
    s.send(ip.encode())
    print("Logical Address",s.recv(1024).decode())
```
## OUTPUT -RARP
## Server side
<img width="1854" height="137" alt="image" src="https://github.com/user-attachments/assets/2c1f1fef-7b16-4be9-9c6d-e5367b5e3f79" />
## Client side
<img width="1847" height="238" alt="image" src="https://github.com/user-attachments/assets/884981fc-4818-40a1-a4dc-59e988435315" />
## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
