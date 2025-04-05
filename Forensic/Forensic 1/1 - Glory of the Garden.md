### Descripción
This [garden](https://jupiter.challenges.picoctf.org/static/43c4743b3946f427e883f6b286f47467/garden.jpg) contains more than it seems.
### Solución
Iniciamos descargando en la consola el archivo que vamos a explorar a través del comando **wget**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics]
└─$ wget https://jupiter.challenges.picoctf.org/static/43c4743b3946f427e883f6b286f47467/garden.jpg
--2025-04-03 21:29:17--  https://jupiter.challenges.picoctf.org/static/43c4743b3946f427e883f6b286f47467/garden.jpg
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2295192 (2.2M) [application/octet-stream]
Saving to: ‘garden.jpg’

garden.jpg                   100%[=============================================>]   2.19M  2.40MB/s    in 0.9s    

2025-04-03 21:29:18 (2.40 MB/s) - ‘garden.jpg’ saved [2295192/2295192]
```

Luego procedemos a revisar el tipo de archivo con el comando **file**, como se muestra a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics]
└─$ file garden.jpg                                                         
garden.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 2999x2249, components 3    
```

Una vez que sabemos el tipo de archivo con el que estamos trabajando, procedemos a revisarlo con un editor de hexadecimal, ya que en las pistas se nos hace mención de eso, por lo que ahora usaremos la herramienta **hexeditor**, incluida ya en Kali:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics]
└─$ hexeditor garden.jpg
```

Una vez ejecutado el comando obtenemos:

```shell
File: garden.jpg                                                     ASCII Offset: 0x00000000 / 0x00230597 (%00)   
00000000  FF D8 FF E0  00 10 4A 46   49 46 00 01  01 01 00 48                                      ......JFIF.....H
00000010  00 48 00 00  FF E2 0C 58   49 43 43 5F  50 52 4F 46                                      .H.....XICC_PROF
00000020  49 4C 45 00  01 01 00 00   0C 48 4C 69  6E 6F 02 10                                      ILE......HLino..
00000030  00 00 6D 6E  74 72 52 47   42 20 58 59  5A 20 07 CE                                      ..mntrRGB XYZ ..
00000040  00 02 00 09  00 06 00 31   00 00 61 63  73 70 4D 53                                      .......1..acspMS
00000050  46 54 00 00  00 00 49 45   43 20 73 52  47 42 00 00                                      FT....IEC sRGB..
00000060  00 00 00 00  00 00 00 00   00 00 00 00  F6 D6 00 01                                      ................
```

Por lo que usando CTRL+W, procedemos a buscar la bandera con **picoCTF** entre todo el archivo revisado, lo cual nos muestra lo siguiente:

```shell
File: garden.jpg                                                     ASCII Offset: 0x0023056E / 0x00230597 (%100)  
00230560  72 65 20 69  73 20 61 20   66 6C 61 67  20 22 70 69                                      re is a flag "pi
00230570  63 6F 43 54  46 7B 6D 6F   72 65 5F 74  68 61 6E 5F                                      coCTF{more_than_
00230580  6D 33 33 74  73 5F 74 68   65 5F 33 79  33 36 35 37                                      m33ts_the_3y3657
00230590  42 61 42 32  43 7D 22 0A                                                                 BaB2C}". 
```

Por lo que hemos obtenido la bandera que da solución al reto:

```
picoCTF{more_than_m33ts_the_3y3657BaB2C}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Editor_hexadecimal