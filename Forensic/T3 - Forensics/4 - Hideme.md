### Descripción
Every file gets a flag. 
The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye [here](https://artifacts.picoctf.net/c/262/flag.png).
### Solución
Iniciamos descargando el archivo contenido en la descripción del reto con el comando wget:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/hideme]
└─$ wget https://artifacts.picoctf.net/c/262/flag.png                        
--2025-05-09 23:31:22--  https://artifacts.picoctf.net/c/262/flag.png
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.61, 3.161.55.100, 3.161.55.26, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.61|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 42945 (42K) [application/octet-stream]
Saving to: ‘flag.png’

flag.png               100%[===========================>]  41.94K  --.-KB/s    in 0.06s   

2025-05-09 23:31:23 (672 KB/s) - ‘flag.png’ saved [42945/42945]
```

Ahora procedemos a revisar con binwalk para ver si el archivo tiene más cosas ocultas:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/hideme]
└─$ binwalk flag.png  

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2884, uncompressed size: 3038, name: secret/flag.png
42923         0xA7AB          End of Zip archive, footer length: 22
```

Como se puede ver, hay un archivo dentro de la carpeta secret, el cual se denomina como flag.png, por lo que procedemos a descomprimirlo:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/hideme]
└─$ binwalk -e flag.png 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2884, uncompressed size: 3038, name: secret/flag.png
```

Ahora procedemos a revisar la carpeta que nos interesaba y que acabamos de extraer y abrir el archivo que contiene:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/hideme/_flag.png.extracted]
└─$ cd secret              

┌──(kali㉿kali)-[~/…/tarea3_forensics/hideme/_flag.png.extracted/secret]
└─$ ls
flag.png

┌──(kali㉿kali)-[~/…/tarea3_forensics/hideme/_flag.png.extracted/secret]
└─$ open flag.png
```

Una vez abierta la imagen, encontramos la bandera que da solución a este reto:

```
picoCTF{Hiddinng_An_imag3_within_@n_ima9e_82101824}
```
### Notas Adicionales

### Referencias