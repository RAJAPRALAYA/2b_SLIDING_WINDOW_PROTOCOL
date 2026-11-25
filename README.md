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
## Server
```

import socket

s = socket.socket()
s.bind(('127.0.0.1', 9000))
s.listen(5)

print("Server is waiting for connection...", flush=True)

c, addr = s.accept()

print("CLIENT IS CONNECTED", flush=True)
print("Client address:", addr, flush=True)

size = int(input("Enter number of frames to send: "))
frames = list(range(size))

w = int(input("Enter Window Size: "))

i = 0

while i < len(frames):
    st = min(i + w, len(frames))

    c.send(str(frames[i:st]).encode())

    ack = c.recv(1024).decode()
    print(ack)

    i = st

print("All frames sent successfully!")

c.close()
s.close()




```

## Client
```

import socket

s = socket.socket()

s.connect(('127.0.0.1', 9000))

print("Connected to server")

while True:
    data = s.recv(1024).decode()

    if not data:
        break

    print("Received frames:", data)

    s.send("Acknowledgement received".encode())

print("Communication completed")

s.close()



```
## OUPUT
## Server
<img width="1395" height="271" alt="image" src="https://github.com/user-attachments/assets/c65ef5f4-3081-4d1b-937e-124911341ae4" />

## Client
<img width="1422" height="240" alt="image" src="https://github.com/user-attachments/assets/914ca834-b662-4572-a549-7a927f4593b5" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
