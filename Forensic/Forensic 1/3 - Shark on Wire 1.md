### Descripción
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap). Recover the flag.
### Solución
Iniciamos descargando el paquete de captura que nos es proporcionado en la descripción del reto mediante el comando **wget**, como se aprecia a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/shark_on_wire_1]
└─$ wget https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap
--2025-04-03 23:36:25--  https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 239455 (234K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap                 100%[=============================================>] 233.84K  1008KB/s    in 0.2s    

2025-04-03 23:36:25 (1008 KB/s) - ‘capture.pcap’ saved [239455/239455]
```

Una vez descargado procedemos a investigar que son las capturas de paquetes, encontrando que es el proceso de interceptar y registrar los paquetes de datos que pasan a través de una red informática. Este método permite a individuos u organizaciones monitorear el tráfico en su red y analizar los datos con varios fines, incluyendo la resolución de problemas de red, el análisis de seguridad y la optimización del rendimiento.

Ahora que sabemos lo que es, procedemos a verificar que tipo de archivo es con el comando **file**, como se aprecia a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/shark_on_wire_1]
└─$ file capture.pcap 
capture.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)
```

Por lo que ahora se hará es emplear la herramienta **wireshark**, lo cual después de lanzarla y cargar el archivo descargado, obtendremos una vista como la siguiente:

![[Screenshot_2025-04-03_23_51_44.png]]

Enseguida nos posicionamos sobre un paquete UDP, hacemos clic derecho sobre él y seleccionamos la opción de **Follow > UDP Stream**, donde una vez colocado eso, encontraremos lo siguiente, que son streams, iniciando con el stream 4:

```
fjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdn
```

Luego con el stream 5:

```
picopicopicopico
```

Y por último el stream 6, donde habremos encontrado la bandera que resuleve este reto:

```
picoCTF{StaT31355_636f6e6e}
```
### Notas Adicionales

### Referencias
https://www.vpnunlimited.com/es/help/cybersecurity/packet-capture?srsltid=AfmBOop382ABdm2_-QkO1SGu8LB67payOKDE_oJCk4QqWXHuIT2NDbCE