### Descripción
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap). Recover the flag that was pilfered from the network.
### Solución
Iniciamos descargando el paquete de capturas de wireshark con el comando wget:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/shark_on_wire_2]
└─$ wget https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap
--2025-04-26 00:05:53--  https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 112318 (110K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap              100%[==================================>] 109.69K  --.-KB/s    in 0.1s    

2025-04-26 00:05:54 (743 KB/s) - ‘capture.pcap’ saved [112318/112318]
```

Procedemos ahora a abrir el paquete que descargamos con la aplicación wireshark, donde encontramos lo siguiente:

![[Captura de pantalla 2025-04-25 221830.png]]

Después de estar analizando el paquete de capturas se descubre que los paquetes UDP con destino al puerto 22, en el stream 32 tenemos la palabra "start" y en el stream 60 tenemos "end", por lo que al filtrar solo los paquetes que tienen como destino al puerto 22, tenemos lo siguiente:

![[Captura de pantalla 2025-04-25 222013.png]]

Como podemos ver, tenemos en el inicio y el fin al puerto origen 5000, ya los demás son puertos que inician con 5000 y tienen diferentes números, los cuales van a ser convertidos a su respectivo carácter hexadecimal, iniciando con python:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/shark_on_wire_2]
└─$ python3                     
Python 3.13.2 (main, Feb  5 2025, 01:23:35) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> chr(112)
'p'
>>> chr(105)
'i'
>>> chr(99)
'c'
>>> chr(111)
'o'
>>>
```

Con lo anterior podemos ver que se empieza a formar la bandera que da solución a este reto, pero estar ingresando los 35 números puede resultar aburrido, se procede a utilizar una herramienta como lo es: Scapy Project, una vez que revisamos se encuentra instalada, creamos un script que nos va a permitir realizar esta tarea, dicho script es el siguiente:

```python
from scapy.all import *

packets = rdpcap('capture.pcap')

flag = ''

for p in packets:
        if UDP in p and p[UDP].dport == 22:
                if p[UDP].sport > 5000:
                        flag += chr(p[UDP].sport - 5000)

print(flag)
```

Por lo que una vez guardado, procedemos a ejecutar este script:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/shark_on_wire_2]
└─$ python3 exp.py
picoCTF{p1LLf3r3d_data_v1a_st3g0}
```

El cual nos arroja la bandera que da solución a este reto:

```
picoCTF{p1LLf3r3d_data_v1a_st3g0}
```
### Notas Adicionales

### Referencias
https://scapy.net/