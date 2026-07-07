import socket # серверная часть
import threading
IP = '127.0.0.1'
PORT = 4444
HOST = 'host.roman'
clients = dict()

def handle_client(connection, adress):
    nickname = connection.recv(1024).decode('utf-8')
    notification = '[+] подключен новый клиент к чату! здравствуй ' + nickname
    print(notification)
    clients[nickname] = connection
    for key, humansocket in clients.items():
                if humansocket != connection:                   
                    humansocket.send(notification.encode('utf-8'))
    while True:
        encode_message = connection.recv(1024)
        decode_message = encode_message.decode('utf-8')
        if encode_message == b'' or decode_message == 'quit':
            for key, humansocket in clients.items():
                try:
                    if humansocket == connection:
                        delete_connection = key
                    else:
                        humansocket.send( f'пользователь {key} отключился'.encode('utf-8')) 
                except:
                    pass
            del clients[delete_connection]
            break
        
        
       

        for key, humansocket in clients.items():
            try:
                if humansocket != connection:
                    finalmessage = '[' + nickname + ']: ' + decode_message
                    humansocket.send(finalmessage.encode('utf-8'))
            except:
                pass

    connection.close()


def main():
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind((IP, PORT))
    server.listen(5)
    while True:
        connection, address = server.accept()
        thread = threading.Thread(target=handle_client, args=(connection, address))
        thread.start()


main()
