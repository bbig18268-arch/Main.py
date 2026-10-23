import socket
import sys
from datetime import datetime
# Definindo o alvo (vamos testar o sua própria máquina local)
alvo = "127.0.0.1"
print("-" * 50)
print(f"Escaneando o alvo: {alvo}")
print(f"iniciando do escaneamento: {str(datetime.now())}")
print("-" * 50)

#portas mais comum que serviços de rede e hackers costumam usar
# 21 (FTP), 22 (SSH), 80 (HTTP), 443 (HTTPS)
portas_para_testar = [21, 22, 80, 443, 8000]
try:
    for porta in portas_para_testar:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)  # Definindo um tempo limite para a conexão
        resultado = sock.connect_ex((alvo, porta))  # Tentando conectar à porta
        if resultado == 0:
            print(f"Porta {porta} está aberta")
        else:
            print(f"Porta {porta} está fechada")
        sock.close()
except KeyboardInterrupt:
    print("\nSaindo do programa.")
    sys.exit()
except socket.gaierror:
    print("\nHostname não pôde ser resolvido. Encerrando.")
    sys.exit()
