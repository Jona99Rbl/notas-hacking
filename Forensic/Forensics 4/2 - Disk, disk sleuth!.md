### Descripción
Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image: [dds1-alpine.flag.img.gz](https://mercury.picoctf.net/static/2f998eee12730cf5766624681212a441/dds1-alpine.flag.img.gz)
### Solución
Iniciamos descargando la imagen que tenemos en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/disk_sleuth]
└─$ wget https://mercury.picoctf.net/static/2f998eee12730cf5766624681212a441/dds1-alpine.flag.img.gz
--2025-05-06 20:40:30--  https://mercury.picoctf.net/static/2f998eee12730cf5766624681212a441/dds1-alpine.flag.img.gz
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29768911 (28M) [application/octet-stream]
Saving to: ‘dds1-alpine.flag.img.gz’

dds1-alpine.flag.img.g 100%[============================>]  28.39M  3.52MB/s    in 8.5s    

2025-05-06 20:40:39 (3.35 MB/s) - ‘dds1-alpine.flag.img.gz’ saved [29768911/29768911]
```

Una vez descargada procedemos a revisar que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/disk_sleuth]
└─$ file dds1-alpine.flag.img.gz 
dds1-alpine.flag.img.gz: gzip compressed data, was "dds1-alpine.flag.img", last modified: Tue Mar 16 00:19:31 2021, from Unix, original size modulo 2^32 134217728
```

Resultando ser una imagen de disco comprimida, por lo que procedemos a descomprimirla con el siguiente comando:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/disk_sleuth]
└─$ gzip -d dds1-alpine.flag.img.gz 
```

Una vez descomprimido, procedemos a aplicar un comando **strings** además de usar **grep** para filtrar la palabra pico, obteniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/disk_sleuth]
└─$ strings dds1-alpine.flag.img | grep pico
ffffffff81399ccf t pirq_pico_get
ffffffff81399cee t pirq_pico_set
ffffffff820adb46 t pico_router_probe
  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_267e38f6}
```

Obteniendo la bandera que da solución al reto:

```
picoCTF{f0r3ns1c4t0r_n30phyt3_267e38f6}
```
### Notas Adicionales

### Referencias