import os
import optparse
import sys
import re
import socket
import time

ROJO = '\033[91m'  # Color rojo para errores o advertencias
VERDE = '\033[92m'  # Color verde para éxitos
AMARILLO = '\033[93m'  # Color amarillo para advertencias o énfasis
AZUL = '\033[94m'  # Color azul para información general
MAGENTA = '\033[95m'  # Color magenta para encabezados
CIAN = '\033[96m'  # Color cian para otros usos
RESET = '\033[0m'  # Restablece los colores y estilos
NEGRITA = '\033[1m'  # Aplica negrita al texto
SUBRAYADO = '\033[4m'  # Subraya el texto

def main():
    os.system("clear")
    time.sleep(0.5)
    try:
        print(NEGRITA + "\n [*] ¿Que servidor quieres crear? [*] \n" + RESET)
        print(NEGRITA + "1." + RESET ,  VERDE + "Server local" + RESET , " - Descarga archivos de la caperta actual."  )
        print(NEGRITA + "2." + RESET ,  VERDE + "Server upload" + RESET , "- Envia archivos a la carpeta actual.\n")
        time.sleep(0.5)
        resultado = input(NEGRITA + "  [*] Eligue: " + RESET)
        eleccion(resultado)
    except KeyboardInterrupt:
        exit()

def eleccion(input):
    if input == "1":
        local()
    if input == "2":
        upload()
    else:
        ayuda()


def local():
    os.system("clear")
    ip = re.search(r"\b(?:\d{1,3}\.){3}\d{1,3}\b", socket.gethostbyname(socket.gethostname())).group()
    print("\n Busca en tu navegador la ip en rojo")
    print("  Ip: " , ROJO + ip + RESET,  "\n  Puerto:  8080")
    print( VERDE + "\n\t Ejemplo:" + RESET , " http://",  ROJO + "IP" + RESET , ":8080\n") 
    os.system("python3 -m http.server 8080" )
    exit()


def upload():
    os.system("clear")
    ip2 = re.search(r"\b(?:\d{1,3}\.){3}\d{1,3}\b", socket.gethostbyname(socket.gethostname())).group()
    print("\nBusca en tu navegador la ip en rojo ")
    print("  Ip: " , ROJO + ip2 + RESET,  "\n  Puerto:  8080")
    print( VERDE + "\n\t Ejemplo:" + RESET , " http://",  ROJO + "IP" + RESET , ":8080/upload\n") 
    os.system("python3 -m uploadserver 8080")
    exit()

def exit():
    os.system("clear")
    print(ROJO + "\n [+]" + RESET,  NEGRITA + "Saliendo" + RESET, ROJO + "[+]\n" + RESET)
    sys.exit()

def ayuda():
    os.system("clear")
    print( NEGRITA + "\n\t\t\t     Panel de ayuda" + RESET )
    print("\n   1) Para levantar un servidor local debes presionar el numero 1 que te permitira")
    print("      ver los contenidos que tienes en la carpeta que inciaste este script en python.")
    print( VERDE + "\n\t  [*] Ejemplo:" + RESET, NEGRITA + "http://192.168.100.94:8080\n" + RESET)

    print("\n   2) Para levantar un servidor upload debes presionar el numero 2 que te permitira")
    print("      subir archivos a la carpeta donde iniciaste este script de python.")
    print("      Deberas abrir el navegador y poner la ip que te indica en pantalla para acceder")
    print("      al panel de subida de archivos.")
    print( VERDE + "\n\t  [*] Ejemplo:" + RESET, NEGRITA + "http://192.168.100.94:8080/upload\n" + RESET)


if __name__ == "__main__":
    main()


