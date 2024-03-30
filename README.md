# 3b.CREATION FOR CHAT USING TCP SOCKETS
## AIM
To write a python program for creating Chat using TCP Sockets Links.
## ALGORITHM:
1. Import the necessary modules in python
2. Create a socket connection to using the socket module.
3. Send message to the client and receive the message from the client using the Socket module in
 server
4. Send and receive the message using the send function in socket.
## PROGRAM:
```
Chat Server


import socket
import threading

def handle_client(client_socket, client_address):
    print(f"Accepted connection from {client_address}")

    while True:
        # Receive data from the client
        data = client_socket.recv(1024)
        if not data:
            break

        print(f"Received from {client_address}: {data.decode()}")

        # Send the data back to the client
        client_socket.sendall(data)

    print(f"Connection closed by {client_address}")
    client_socket.close()

def start_chat_server():
    # Create a socket object
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Bind the socket to a specific address and port
    server_address = ('localhost', 5555)
    server_socket.bind(server_address)

    # Listen for incoming connections
    server_socket.listen(5)
    print(f'Server listening on {server_address[0]}:{server_address[1]}')

    while True:
        # Wait for a connection
        print('Waiting for a connection...')
        client_socket, client_address = server_socket.accept()

        # Start a new thread to handle the client
        client_handler = threading.Thread(target=handle_client, args=(client_socket, client_address))
        client_handler.start()

if __name__ == "__main__":
    start_chat_server()
```

```
Chat Client1 and Client2

import socket
import threading

def receive_messages(client_socket):
    while True:
        # Receive data from the server
        data = client_socket.recv(1024)
        if not data:
            break
        print(f"Received from server: {data.decode()}")

def start_chat_client():
    # Create a socket object
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Connect to the server
    server_address = ('localhost', 5555)
    client_socket.connect(server_address)

    # Start a thread to receive messages from the server
    receive_thread = threading.Thread(target=receive_messages, args=(client_socket,))
    receive_thread.start()

    # Send messages to the server
    while True:
        message = input('Enter a message to send to the server (type "exit" to quit): ')
        if message.lower() == 'exit':
            break

        # Send the message to the server
        client_socket.sendall(message.encode())

    # Close the connection
    client_socket.close()

if __name__ == "__main__":
    start_chat_client()
```
## OUPUT:
## Chat Server:
![Screenshot 2024-03-11 160910](https://github.com/EzhilsreeJ/3b_CHAT_USING_TCP_SOCKETS/assets/144870412/4e8d08f5-f8fa-4d5c-8f57-0783c380bace)

## Chat Client1:
![Screenshot 2024-03-11 190419](https://github.com/EzhilsreeJ/3b_CHAT_USING_TCP_SOCKETS/assets/144870412/40e70bfd-40e2-4ce4-905b-08c1bc464a35)


## Chat Client2:
![image](https://github.com/EzhilsreeJ/3b_CHAT_USING_TCP_SOCKETS/assets/144870412/2a0e2ecb-cbf3-44db-8d54-1d6671694ff7)

## RESULT
Thus, the python program for creating Chat using TCP Sockets Links was successfully 
created and executed.

