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

#server
```
import socket

s = socket.socket()

# allow port reuse
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

s.bind(('localhost', 9000))
s.listen(1)

print("Waiting for connection...")

conn, addr = s.accept()
print("Connected to", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Frames received:", data)

    ack = "ACK for " + data
    conn.send(ack.encode())

conn.close()
s.close()

```

#client
```
import socket

s = socket.socket()

# connect to same port used in server
s.connect(('localhost', 9000))

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = list(range(1, n+1))
i = 0

while i < n:
    send_frames = frames[i:i+w]
    msg = " ".join(map(str, send_frames))

    print("Sending frames:", msg)
    s.send(msg.encode())

    ack = s.recv(1024).decode()
    print("Received:", ack)

    i += w

s.close()

```
## OUPUT
<img width="1858" height="240" alt="Screenshot 2026-03-12 142337" src="https://github.com/user-attachments/assets/ef2a68b7-2b2b-4cce-a310-a9facebd21d3" />
<img width="1855" height="221" alt="Screenshot 2026-03-12 142423" src="https://github.com/user-attachments/assets/07288e5f-96d1-4405-b187-f4b36830cf57" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
