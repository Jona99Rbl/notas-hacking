### Descripción
This is a really weird text file [TXT](https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt)? Can you find the flag?
### Solución
Iniciamos descargando el archivo "**.txt**" que nos aparece en la descripción con el comando **wget** en la consola:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/extensions]
└─$ wget https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt    
--2025-04-04 00:30:38--  https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9984 (9.8K) [application/octet-stream]
Saving to: ‘flag.txt’

flag.txt                     100%[=============================================>]   9.75K  --.-KB/s    in 0.001s  

2025-04-04 00:30:38 (8.92 MB/s) - ‘flag.txt’ saved [9984/9984]
```

Una vez descargado procedemos a revisar que tipo de archivo es con el comando **file**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/extensions]
└─$ file flag.txt    
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
```

Como podemos apreciar, pese a que descargamos un archivo **.txt**, en realidad es una imagen **.png**, por lo que hora debemos investigar algunas cosas como lo son los formatos de archivo, que son las extensiones con las que las computadoras manejan los archivos que contienen.

Por lo que ahora revisamos la firma del documento, ya que esta contiene los números mágicos que identifican al tipo del archivo, esto se realiza con el comando **xxd**, como se podrá ver a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/extensions]
└─$ xxd flag.txt | head
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR
00000010: 0000 06a1 0000 0260 0802 0000 0085 ad5e  .......`.......^
00000020: 9a00 0000 0173 5247 4200 aece 1ce9 0000  .....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 0000 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f000 0026 9549 4441 5478 5eed dd6b  R$...&.IDATx^..k
00000060: 421b 39b7 05d0 3b2e 0694 f130 9a4c 2683  B.9...;....0.L&.
00000070: f9ae 5f80 4e3d 25bb 4cb3 f15a bfba a14a  .._.N=%.L..Z...J
00000080: 7574 2413 7927 c0ff fd0f 0000 0000 4826  ut$.y'........H&
00000090: e303 0000 0080 6c32 3e00 0000 00c8 26e3  ......l2>.....&.
```

Por lo que confirmamos que el archivo es en realidad una imagen **.png** con los números `8950 4e47 0d0a 1a0a`, por lo que ahora solo nos resta cambiarle el formato de **.txt** a **.png**, con ayuda del comando **mv**:

```
┌──(kali㉿kali)-[~/notas-hacking/Forensics/extensions]
└─$ mv flag.txt flag.png 
```

Una vez realizado esto, se procede a revisar la imagen, donde encontramos la bandera que da solución a este reto:

```
picoCTF{now_you_know_about_extensions}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Anexo:Formatos_de_archivo
https://en.wikipedia.org/wiki/List_of_file_signatures