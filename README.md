# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## Name : Sashtitha.K
## Reg.NO: 212225230253
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
server.py
```
import socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

server.bind(('localhost', 12345))
server.listen(1)

print("Server is waiting for client...")

conn, addr = server.accept()
print("Client connected:", addr)

while True:
    data = conn.recv(1024)

    if not data:
        break

    if data == b'END':
        print("Communication stopped")
        break

    print("Frame received:", data.decode())

    
    conn.send(b'ACK')

conn.close()
server.close()
```
client.py
```
import socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect(('localhost', 12345))

print("Connected to server")
frame_size = int(input("Enter frame size: "))

message = input("Enter web page data: ")

frames = [message[i:i+frame_size]
          for i in range(0, len(message), frame_size)]


for frame in frames:

    client.send(frame.encode())

    ack = client.recv(1024).decode()

    if ack == "ACK":
        print("ACK received - Frame sent successfully:", frame)
    else:
        print("NACK received - Frame not received")

client.send(b'END')

print("Program stopped")

client.close()
```
## OUTPUT
client.py
<img width="1600" height="805" alt="image" src="https://github.com/user-attachments/assets/ae9eee43-a3b8-4576-ba75-8a857f894220" />
server.py
<img width="1600" height="811" alt="image" src="https://github.com/user-attachments/assets/63dc2187-48d4-4320-8dd2-81f007218853" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
