# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
client.py
```
import socket

c = socket.socket()
c.connect(('localhost', 8080))

n = int(input("Enter number of frames to send: "))

for i in range(n):
    frame = f"Frame {i+1}"
    c.send(frame.encode())
    ack = c.recv(1024).decode()
    print(f"Server reply for {frame}: {ack}")
    if ack == "NACK":
        print("Resending frame...")
        c.send(frame.encode())
        print("Resent:", c.recv(1024).decode())

c.send(b"exit")
c.close()
print("Client closed.")


```
server.py
```
import socket
import random

s = socket.socket()
s.bind(('localhost', 8080))
s.listen(1)
print("Server listening...")

conn, addr = s.accept()
print("Connected from:", addr)

while True:
    data = conn.recv(1024).decode()
    if not data or data.lower() == 'exit':
        break

    print("Received:", data)
    # Randomly simulate ACK or NACK
    ack = "ACK" if random.choice([True, False]) else "NACK"
    conn.send(ack.encode())

conn.close()
s.close()
print("Server closed.")


```
## OUTPUT
<img width="658" height="390" alt="Screenshot 2025-11-11 091723" src="https://github.com/user-attachments/assets/3260c177-20c9-462a-8ca5-20c4855c1ceb" />
<img width="642" height="509" alt="Screenshot 2025-11-11 091737" src="https://github.com/user-attachments/assets/f8e856f7-455d-4594-9d25-22e3ab185570" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
