# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
```
client.py

import socket
s = socket.socket()
s.connect(('localhost', 8000))
size = int(input("Enter number of frames to send : "))
frames = list(range(size))
win_size = int(input("Enter Window Size : "))
i = 0
while i < len(frames):
    end = i + win_size
    s.send(str(frames[i:end]).encode())  
    ack = s.recv(1024).decode()
    if ack:
        print(ack)
    i = end  

s.close()

```
```
sever.py

import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is waiting for connection...")
c, addr = s.accept()
print("Connected with:", addr)
while True:
    data = c.recv(1024).decode()
    if not data:
        break
    print(data)  
    c.send("acknowledgement recived from the server".encode())

c.close()
```

## OUPUT
<img width="1920" height="1200" alt="Screenshot (9)" src="https://github.com/user-attachments/assets/bec09fb1-2b17-4213-866b-2d63e576d6ba" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
