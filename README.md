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
print("Server waiting for connection...")

conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()  # Receive frames
    if not frames:
        break
    print(f"Received: {frames}")

    ack = f"ACK for {frames}"  # Send acknowledgment
    conn.send(ack.encode())

conn.close()
s.close()
  
```

### client:
```python
import socket

c = socket.socket()
c.connect(('localhost', 9999))

# Get number of frames and window size
size = int(input("Enter number of frames: "))
window_size = int(input("Enter window size: "))

frames = list(range(size))  # Frame numbers
i = 0

while i < size:
    send_frames = frames[i:i + window_size]  # Sending window-sized frames
    print(f"Sending frames: {send_frames}")
    c.send(str(send_frames).encode())  # Send frames

    ack = c.recv(1024).decode()  # Receive acknowledgment
    print(f"Received: {ack}")

    i += window_size  # Move window

c.close()

```
## OUPUT

### server
![image](https://github.com/user-attachments/assets/84c04f19-c06e-4328-89f5-f86fb7233290)


### client
![image](https://github.com/user-attachments/assets/bb5bf23c-5cf1-4f67-b8c7-bee5ff8bf129)


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed

