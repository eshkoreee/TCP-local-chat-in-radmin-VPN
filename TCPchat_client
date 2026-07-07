import socket # клиентская часть
import threading
IP = input('введите айпи хоста написанном в radmin vpn ')
PORT = 4444
socketconnect = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
socketconnect.connect((IP, 4444))


def receive_messages(socketconnect):
    while True:
        message = socketconnect.recv(1024).decode('utf-8')
        print(message)

def main():
    thread = threading.Thread(target = receive_messages, args=(socketconnect,))
    thread.start()
    while True:
        
        message = input()
        encode_message = message.encode('utf-8')
        if message != 'quit':
            socketconnect.send(encode_message)
        else:
            socketconnect.close()

main()
