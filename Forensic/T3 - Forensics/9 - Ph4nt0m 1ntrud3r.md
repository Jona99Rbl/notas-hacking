### Descripción
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag. To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder! Find the PCAP file here [Network Traffic PCAP file](https://challenge-files.picoctf.net/c_verbal_sleep/960abba2fdbc9be5013ef87f1df67213e9b63d4561d7a8c8c1ce7a4ce40a547e/myNetworkTraffic.pcap) and try to get the flag.
### Solución
Iniciamos descargando el archivo de la captura de paquetes:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/ph4nt0m_1ntrud3r]
└─$ wget https://challenge-files.picoctf.net/c_verbal_sleep/960abba2fdbc9be5013ef87f1df67213e9b63d4561d7a8c8c1ce7a4ce40a547e/myNetworkTraffic.pcap
--2025-05-10 21:58:26--  https://challenge-files.picoctf.net/c_verbal_sleep/960abba2fdbc9be5013ef87f1df67213e9b63d4561d7a8c8c1ce7a4ce40a547e/myNetworkTraffic.pcap
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 65.9.149.85, 65.9.149.24, 65.9.149.59, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|65.9.149.85|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1452 (1.4K) [application/octet-stream]
Saving to: ‘myNetworkTraffic.pcap’

myNetworkTraffic.pcap  100%[===========================>]   1.42K  --.-KB/s    in 0.002s  

2025-05-10 21:58:26 (772 KB/s) - ‘myNetworkTraffic.pcap’ saved [1452/1452]
```

Al saber que es un archivo de captura de paquetes, se procede a usar wireshark, donde al abrir encontramos diversos paquetes, al estarlo analizando, nos encontramos con que hay algunos que contienen fragmentos de cadena codificados en base64, siendo estos los paquetes con longitud de 4 y 12, por lo que se aplica el siguiente filtro:

```
tcp.len == 4  || tcp.len == 12
```

Una vez que nos aparecen los paquetes filtrados, ahora procedemos a ordenarlos por tiempo, de menor a mayor, una vez organizados así empezamos a extraer las cadenas convertidas de base64 a ASCII, a continuación se muestra la cadena del primer paquete:

```
picoCTF
```

Ahora del segundo:

```
{1t_w4s
```

Tercero:

```
nt_th4t
```

Cuarto:

```
_34sy_t
```

Quinto:

```
bh_4r_e
```

Sexto:

```
5e8c78d
```

Séptimo:

```
}
```

Si juntamos todas las partes, tendremos la bandera que da solución al reto:

```
picoCTF{1t_w4snt_th4t_34sy_tbh_4r_e5e8c78d}
```
### Notas Adicionales

### Referencias