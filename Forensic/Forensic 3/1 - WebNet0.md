### Descripción
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key). Recover the flag.
### Solución
Iniciamos descargando el paquete de captura y la llave que vamos a requerir para dar solución al reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet0]
└─$ wget https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap  
--2025-04-26 10:30:16--  https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 13163 (13K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap                100%[========================================>]  12.85K  --.-KB/s    in 0.002s  

2025-04-26 10:30:16 (5.12 MB/s) - ‘capture.pcap’ saved [13163/13163]
```

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet0]
└─$ wget https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key
--2025-04-26 10:32:36--  https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1704 (1.7K) [application/octet-stream]
Saving to: ‘picopico.key’

picopico.key                100%[========================================>]   1.66K  --.-KB/s    in 0.001s  

2025-04-26 10:32:37 (1.67 MB/s) - ‘picopico.key’ saved [1704/1704]
```

Una vez descargado procedemos a verificar que los archivos sean lo que dicen ser:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet0]
└─$ file capture.pcap  
capture.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 65535)

┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/webnet0]
└─$ file picopico.key 
picopico.key: OpenSSH private key (no password)
```

Ahora procedemos a abrir el paquete de capturas con WiresShark, donde tenemos lo siguiente:

![[Screenshot_2025-04-26_11_10_46.png]]

Procedemos a seguir el steam TLS, pero como podemos ver se encuentran encriptados ya que no se aprecia ningún mensaje al desplazarse por los mismos:

![[Screenshot_2025-04-26_11_12_45.png]]

Entonces procedemos a cargar la llave que nos proporcionaron en la descripción del reto, una vez que lo hemos hecho, se puede apreciar el cambio en donde ahora aparecen paquetes en verde:

![[Screenshot_2025-04-26_11_19_29.png]]

Ahora al seguir los streams TLS de la captura de paquetes, encontramos lo siguiente:

```
GET /starter-template.css HTTP/1.1

Host: ec2-18-223-184-200.us-east-2.compute.amazonaws.com

User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0

Accept: text/css,*/*;q=0.1

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Connection: keep-alive

Referer: https://ec2-18-223-184-200.us-east-2.compute.amazonaws.com/

Pragma: no-cache

Cache-Control: no-cache

  

  

HTTP/1.1 200 OK

Date: Fri, 23 Aug 2019 15:56:36 GMT

Server: Apache/2.4.29 (Ubuntu)

Last-Modified: Mon, 12 Aug 2019 16:47:05 GMT

ETag: "62-58fee462bf227-gzip"

Accept-Ranges: bytes

Vary: Accept-Encoding

Content-Encoding: gzip

Pico-Flag: picoCTF{nongshim.shrimp.crackers}

Content-Length: 100

Keep-Alive: timeout=5, max=100

Connection: Keep-Alive

Content-Type: text/css

  

..........K.O.T..RP(HLI..K.-./.R0-J......+.I,*I-.-I.-.I,IEVj.`.T.`..Q..P.ZQ......g.......2.. ...b...

GET /favicon.ico HTTP/1.1

Host: ec2-18-223-184-200.us-east-2.compute.amazonaws.com

User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0

Accept: image/webp,*/*

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Connection: keep-alive

Pragma: no-cache

Cache-Control: no-cache

  

  

HTTP/1.1 404 Not Found

Date: Fri, 23 Aug 2019 15:56:37 GMT

Server: Apache/2.4.29 (Ubuntu)

Content-Length: 326

Keep-Alive: timeout=5, max=99

Connection: Keep-Alive

Content-Type: text/html; charset=iso-8859-1

  

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">

<html><head>

<title>404 Not Found</title>

</head><body>

<h1>Not Found</h1>

<p>The requested URL /favicon.ico was not found on this server.</p>

<hr>

<address>Apache/2.4.29 (Ubuntu) Server at ec2-18-223-184-200.us-east-2.compute.amazonaws.com Port 443</address>

</body></html>
```

Si revisamos el desplegado en el stream, nos daremos cuenta de que se encuentra la bandera, la cual es:

```
picoCTF{nongshim.shrimp.crackers}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Seguridad_de_la_capa_de_transporte