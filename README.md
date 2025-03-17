# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## NAME: SHYAM S
## REGISTER NUMBER: 212223240156
## AIM
To write a python program to perform sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program.


## PROGRAM
### server:
```python
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close()  
```

### client:
```python
import socket
c = socket.socket()
c.connect(('localhost', 9999))
size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))
i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  

        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  
    break
c.close()  

```
## OUPUT

### server
![Screenshot 2025-03-13 103808](https://github.com/user-attachments/assets/f6ac4127-2754-4133-b70d-6e2c2ee01363)








.

### client
![Screenshot 2025-03-13 103816](https://github.com/user-attachments/assets/36358ef9-3c0f-400e-a98c-cb80c329a3ed)





.

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

