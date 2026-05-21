# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To write a python program to perform sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
```
client side:
import socket
s = socket.socket()
s.connect(('localhost', 9000))
while True:
    data = s.recv(1024).decode()
    if not data:
        break
    print(data)
    s.send("Acknowledgement received from client".encode())
s.close()

server side:
import socket
s = socket.socket()
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind(('localhost', 9000))
s.listen(5)
print("Waiting for connection...")
c, addr = s.accept()
print("Connected with", addr)
size = int(input("Enter number of frames to send : "))
l = list(range(size))
ws = int(input("Enter Window Size : "))
st = 0
i = 0
while i < len(l):
    st += ws
    data = str(l[i:st])
    c.send(data.encode())
    ack = c.recv(1024).decode()
    if ack:
        print(ack)
    i += ws
c.close()
s.close()
```
## OUTPUT
<img width="1264" height="661" alt="Screenshot (157)" src="https://github.com/user-attachments/assets/c8e8c362-951d-4823-a1bf-bf02a40077d6" />
<img width="1385" height="1024" alt="Screenshot (159)" src="https://github.com/user-attachments/assets/2601d933-9586-4475-9095-77929a904963" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
