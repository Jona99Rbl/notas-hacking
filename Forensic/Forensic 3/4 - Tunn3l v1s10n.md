### Descripción
We found this [file](https://mercury.picoctf.net/static/7b2d7c26630e977197022d0af09e3aeb/tunn3l_v1s10n). Recover the flag.
### Solución
iniciamos descargando el archivo que nos proporcionan en la descripción:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/tunn3l_v1s10n]
└─$ wget https://mercury.picoctf.net/static/7b2d7c26630e977197022d0af09e3aeb/tunn3l_v1s10n
--2025-04-26 20:43:52--  https://mercury.picoctf.net/static/7b2d7c26630e977197022d0af09e3aeb/tunn3l_v1s10n
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2893454 (2.8M) [application/octet-stream]
Saving to: ‘tunn3l_v1s10n’

tunn3l_v1s10n               100%[========================================>]   2.76M  2.72MB/s    in 1.0s    

2025-04-26 20:43:54 (2.72 MB/s) - ‘tunn3l_v1s10n’ saved [2893454/2893454]
```

Ahora procedemos a revisar que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/tunn3l_v1s10n]
└─$ file tunn3l_v1s10n 
tunn3l_v1s10n: data
```

Como se puede ver, no nos arroja mucha información, ya que solo nos menciona que son "datos", por lo que se procede a revisar su contenido hexadecimal:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/tunn3l_v1s10n]
└─$ xxd tunn3l_v1s10n | head 
00000000: 424d 8e26 2c00 0000 0000 bad0 0000 bad0  BM.&,...........
00000010: 0000 6e04 0000 3201 0000 0100 1800 0000  ..n...2.........
00000020: 0000 5826 2c00 2516 0000 2516 0000 0000  ..X&,.%...%.....
00000030: 0000 0000 0000 231a 1727 1e1b 2920 1d2a  ......#..'..) .*
00000040: 211e 261d 1a31 2825 352c 2933 2a27 382f  !.&..1(%5,)3*'8/
00000050: 2c2f 2623 332a 262d 2420 3b32 2e32 2925  ,/&#3*&-$ ;2.2)%
00000060: 3027 2333 2a26 382c 2836 2b27 392d 2b2f  0'#3*&8,(6+'9-+/
00000070: 2623 1d12 0e23 1711 2916 0e55 3d31 9776  &#...#..)..U=1.v
00000080: 668b 6652 996d 569e 7058 9e6f 549c 6f54  f.fR.mV.pX.oT.oT
00000090: ab7e 63ba 8c6d bd8a 69c8 9771 c193 71c1  .~c..m..i..q..q.
```

Dado que nos aparece un "BM", procedemos a buscar en la lista de firmas de archivos, encontrando que hay uno denominado **BMP**, donde después de investigar, encontramos que fue creado en Windows.

Por lo que una vez que investigamos, procedemos a abrir el archivo hexadecimal donde encontramos lo siguiente:

```
File: tunn3l_v1s10n                                            ASCII Offset: 0x00000000 / 0x002C268D (%00)   
00000000  42 4D 8E 26  2C 00 00 00   00 00 BA D0  00 00 BA D0                                BM.&,...........
00000010  00 00 6E 04  00 00 32 01   00 00 01 00  18 00 00 00                                ..n...2.........
00000020  00 00 58 26  2C 00 25 16   00 00 25 16  00 00 00 00                                ..X&,.%...%.....
00000030  00 00 00 00  00 00 23 1A   17 27 1E 1B  29 20 1D 2A                                ......#..'..) .*
00000040  21 1E 26 1D  1A 31 28 25   35 2C 29 33  2A 27 38 2F                                !.&..1(%5,)3*'8/
```

Después de hacer las correcciones, el código hexadecimal queda así:

```
File: tunn3l_v1s10n                                            ASCII Offset: 0x0000000C / 0x002C268D (%00)  M
00000000  42 4D 8E 26  2C 00 00 00   00 00 28 00  00 00 28 00                                BM.&,.....(...(.
00000010  00 00 6E 04  00 00 32 01   00 00 01 00  18 00 00 00                                ..n...2.........
00000020  00 00 58 26  2C 00 25 16   00 00 25 16  00 00 00 00                                ..X&,.%...%.....
00000030  00 00 00 00  00 00 23 1A   17 27 1E 1B  29 20 1D 2A                                ......#..'..) .*
00000040  21 1E 26 1D  1A 31 28 25   35 2C 29 33  2A 27 38 2F                                !.&..1(%5,)3*'8/
```

Procedemos a revisar si ya nos dice que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/tunn3l_v1s10n]
└─$ file tunn3l_v1s10n 
tunn3l_v1s10n: PC bitmap, Windows 3.x format, 1134 x 306 x 24, image size 2893400, resolution 5669 x 5669 px/m, cbSize 2893454, bits offset 40
```

Ahora si nos confirma que es un Bitmap, donde al abrirlo, nos encontramos con la siguiente imagen:

![[Pasted image 20250426201009.png]]

Donde podemos ver que en la imagen en un primer momento no contiene la bandera, procedemos a revisar la información de la imagen, como se muestra a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/tunn3l_v1s10n]
└─$ exiftool tunn3l_v1s10n 
ExifTool Version Number         : 13.10
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2025:04:26 20:59:52-04:00
File Access Date/Time           : 2025:04:26 20:59:56-04:00
File Inode Change Date/Time     : 2025:04:26 20:59:52-04:00
File Permissions                : -rwxrwx---
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Windows V3
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Image Size                      : 1134x306
Megapixels                      : 0.347
```

De esto se obtiene que a lo mejor por las proporciones de la imagen, no se aprecia algo claro sobre la bandera, por lo que procedemos a modificar otra vez el archivo hexadecimal, donde una vez realizadas las modificaciones, quedaría así:

```
File: tunn3l_v1s10n                                            ASCII Offset: 0x00000018 / 0x002C268D (%00)  M
00000000  42 4D 8E 26  2C 00 00 00   00 00 28 00  00 00 28 00                                BM.&,.....(...(.
00000010  00 00 6E 04  00 00 40 03   00 00 01 00  18 00 00 00                                ..n...@.........
00000020  00 00 58 26  2C 00 25 16   00 00 25 16  00 00 00 00                                ..X&,.%...%.....
00000030  00 00 00 00  00 00 23 1A   17 27 1E 1B  29 20 1D 2A                                ......#..'..) .*
00000040  21 1E 26 1D  1A 31 28 25   35 2C 29 33  2A 27 38 2F                                !.&..1(%5,)3*'8/
```

Con lo anterior, volvemos a revisar las propiedades de la imagen, tenemos lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/tunn3l_v1s10n]
└─$ exiftool tunn3l_v1s10n 
ExifTool Version Number         : 13.10
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2025:04:26 21:09:02-04:00
File Access Date/Time           : 2025:04:26 21:09:06-04:00
File Inode Change Date/Time     : 2025:04:26 21:09:02-04:00
File Permissions                : -rwxrwx---
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Windows V3
Image Width                     : 1134
Image Height                    : 832
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Image Size                      : 1134x832
Megapixels                      : 0.943
```

Procedemos a abrir la imagen y nos encontramos con lo siguiente:

![[Captura de pantalla 2025-04-26 201051.png]]

Obteniendo la bandera que da solución a este reto:

```
picoCTF{qu1t3_a_v13w_2020}
```
### Notas Adicionales

### Referencias
https://en.wikipedia.org/wiki/List_of_file_signatures
https://en.wikipedia.org/wiki/BMP_file_format