### Descripción
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key). Recover the flag.
### Solución
Iniciamos descargando ambos documentos proporcionados, es decir la captura de paquetes y la llave:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet1]
└─$ wget https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap
--2025-04-26 11:27:42--  https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 92525 (90K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap                100%[========================================>]  90.36K  --.-KB/s    in 0.09s   

2025-04-26 11:27:43 (1013 KB/s) - ‘capture.pcap’ saved [92525/92525]
```

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet1]
└─$ wget https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key
--2025-04-26 11:28:01--  https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1704 (1.7K) [application/octet-stream]
Saving to: ‘picopico.key’

picopico.key                100%[========================================>]   1.66K  --.-KB/s    in 0.002s  

2025-04-26 11:28:01 (889 KB/s) - ‘picopico.key’ saved [1704/1704]
```

Ahora procedemos a revisar que en realidad los archivos sean lo que aparentan ser:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet1]
└─$ file capture.pcap 
capture.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 65535)

┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet1]
└─$ file picopico.key 
picopico.key: OpenSSH private key (no password)
```

Procedemos a abrir el paquete de captura con WireShark donde observamos lo siguiente:

![[Screenshot_2025-04-26_11_44_31.png]]

Por lo que otra vez procedemos a cargar la llave proporcionada, al hacerlo podemos ver la aparición de paquetes en verde, lo cual nos dice que el los paquetes TLS fueron desencriptados correctamente:

![[Screenshot_2025-04-26_11_46_44.png]]

Ahora resalta la descarga de una imagen, como se aprecia a continuación:

![[Screenshot_2025-04-26_12_01_55.png]]

Por lo que ahora aplicamos un **strings** filtrando la cadena de caracteres "pico" con grep, encontramos lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet1]
└─$ strings vulture.jpg | grep pico
picoCTF{honey.roasted.peanuts}
```

Obteniendo así la bandera que da solución al reto:

```
picoCTF{honey.roasted.peanuts}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Seguridad_de_la_capa_de_transporte