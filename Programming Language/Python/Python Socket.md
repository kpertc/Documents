#python 

[127.0.0.1和localhost和本机IP三者的区别](https://blog.csdn.net/msdnwolaile/article/details/51278867)

```python
# https://youtu.be/3QiPPX-KeSc?si=_KOTusTtEffAk6ox  
  
import socket  
import threading  
  
PORT = 65432  
SERVER = "127.0.0.1" # localHost  http://localhost:65432
ADDR = (SERVER, PORT)  
  
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  
server.bind(ADDR)  
  
def handle_client(conn, addr):  
    print(f"Resolving the new connection, {addr} connected")  
  
def start():  
    print(f'[SERVER STARTED on {SERVER} {PORT}]')  
    server.listen()  
    while True:  
        conn, addr = server.accept()  
        print(conn)  
        print(addr)  
  
start()
```