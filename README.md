# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
Server -
```
import socket

# Create socket
server_socket = socket.socket()
server_socket.bind(('localhost', 12345))
server_socket.listen(1)

print("Server is waiting for connection...")

conn, addr = server_socket.accept()
print("Connected to client:", addr)

while True:
    frame = conn.recv(1024).decode()

    if frame == "exit":
        print("Transmission completed.")
        break

    print("Received frame:", frame)

    # Send ACK
    ack = "ACK"
    conn.send(ack.encode())
    print("ACK sent\n")

conn.close()
server_socket.close()
```
Client -
```
import socket
import time

# Create socket
client_socket = socket.socket()
client_socket.connect(('localhost', 12345))

n = int(input("Enter number of frames to send: "))

for i in range(1, n + 1):
    frame = f"Frame {i}"
    print("Sending:", frame)
    client_socket.send(frame.encode())

    # Wait for ACK
    ack = client_socket.recv(1024).decode()
    print("Received:", ack)
    time.sleep(1)

client_socket.send("exit".encode())
client_socket.close()
```
## OUTPUT
Server :
<img width="637" height="337" alt="server output" src="https://github.com/user-attachments/assets/731b9c67-358d-4310-b6b0-3f4b8f0ae5da" />

Client :
<img width="652" height="322" alt="client output" src="https://github.com/user-attachments/assets/f31fddca-ac3d-4864-a319-f4a4b743727b" />



## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
