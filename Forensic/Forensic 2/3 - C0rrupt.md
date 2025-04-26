### Descripción
We found this [file](https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery). Recover the flag.
### Solución
Iniciamos descargando el archivo que nos proporciona la descripción con ayuda del comando **wget**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ wget https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery       
--2025-04-25 22:22:25--  https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 202940 (198K) [application/octet-stream]
Saving to: ‘mystery’

mystery                      100%[=============================================>] 198.18K  1.08MB/s    in 0.2s    

2025-04-25 22:22:26 (1.08 MB/s) - ‘mystery’ saved [202940/202940]
```

Ahora procedemos a revisarlo con el comando file:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ file mystery       
mystery: data
```

Como podemos ver, solo nos arroja que es un dato, lo cual no nos dice mucho, por lo que revisando en las pistas tenemos que nos dice algo sobre corregir el encabezado, por lo que procedemos a revisarlo con el comando **xxd**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ xxd mystery | head       
00000000: 8965 4e34 0d0a b0aa 0000 000d 4322 4452  .eN4........C"DR
00000010: 0000 066a 0000 0447 0802 0000 007c 8bab  ...j...G.....|..
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 aa00 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f0aa aaff a5ab 4445 5478 5eec bd3f  R$......DETx^..?
00000060: 8e64 cd71 bd2d 8b20 2080 9041 8302 08d0  .d.q.-.  ..A....
00000070: f9ed 40a0 f36e 407b 9023 8f1e d720 8b3e  ..@..n@{.#... .>
00000080: b7c1 0d70 0374 b503 ae41 6bf8 bea8 fbdc  ...p.t...Ak.....
00000090: 3e7d 2a22 336f de5b 55dd 3d3d f920 9188  >}*"3o.[U.==. ..
```

Revisando en internet, obtenemos que los primeros bits hexadecimales podrían corresponder a un archivo .PNG, por lo que procedemos a modificarlo con el comando **hexeditor**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ hexeditor mystery
```

Una vez digitado el comando, obtenemos lo siguiente:

```shell
File: mystery                                                        ASCII Offset: 0x00000000 / 0x000318BB (%00)   
00000000  89 65 4E 34  0D 0A B0 AA   00 00 00 0D  43 22 44 52                                      .eN4........C"DR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB                                      ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00                                      x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00                                      ..gAMA......a...
00000040  00 09 70 48  59 73 AA 00   16 25 00 00  16 25 01 49                                      ..pHYs...%...%.I
```

Haciendo las correcciones, quedaría así:

```shell
File: mystery                                                        ASCII Offset: 0x00000008 / 0x000318BB (%00)  M
00000000  89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  43 22 44 52                                      .PNG........C"DR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB                                      ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00                                      x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00                                      ..gAMA......a...
00000040  00 09 70 48  59 73 AA 00   16 25 00 00  16 25 01 49                                      ..pHYs...%...%.I
```

Una vez modificado, procedemos a revisar si el comando **file** ya lo reconoce como un archivo:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ file mystery 
mystery: data
```

Aún sigue sin reconocer el archivo, por lo que seguimos revisando en el sitio web donde estamos obteniendo la información y encontramos a los chunks, donde se buscará el IHDR, por lo que procedemos otra vez a editar el archivo hexadecimal con **hexeditor**, por lo que tenemos lo siguiente:

```shell
File: mystery                                                        ASCII Offset: 0x00000008 / 0x000318BB (%00)  M
00000000  89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  43 22 44 52                                      .PNG........C"DR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB                                      ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00                                      x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00                                      ..gAMA......a...
00000040  00 09 70 48  59 73 AA 00   16 25 00 00  16 25 01 49                                      ..pHYs...%...%.I
```

Como se puede ver, encontramos un indicio de ese chunk, por lo que modificado quedaría así:

```shell
File: mystery                                                        ASCII Offset: 0x0000000E / 0x000318BB (%00)  M
00000000  89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  49 48 44 52                                      .PNG........IHDR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB                                      ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00                                      x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00                                      ..gAMA......a...
00000040  00 09 70 48  59 73 AA 00   16 25 00 00  16 25 01 49                                      ..pHYs...%...%.I
```

Guardamos y procedemos a consultar otra vez con **file**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ file mystery 
mystery: PNG image data, 1642 x 1095, 8-bit/color RGB, non-interlaced
```

Ahora si es reconocido, pero al intentar abrirlo, nos indica que hay fallos al procesar la imagen, por lo que descargaremos una herramienta llamada *pngcheck*:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ sudo apt install pngcheck
```

Una vez instalada, procedemos a emplearla con de la siguiente manera:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ pngcheck -v mystery         
File: mystery (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 2852132389x5669 pixels/meter
  CRC error in chunk pHYs (computed 38d82c82, expected 495224f0)
ERRORS DETECTED in mystery
```

Ahora que sabemos que los errores son ocasionados por los offsets, procedemos a editar nuevamente el archivo, teniendo al inicio lo siguiente:

```shell
File: mystery                                                        ASCII Offset: 0x0000000E / 0x000318BB (%00)  M
00000000  89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  49 48 44 52                                      .PNG........IHDR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB                                      ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00                                      x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00                                      ..gAMA......a...
00000040  00 09 70 48  59 73 AA 00   16 25 00 00  16 25 01 49                                      ..pHYs...%...%.I
00000050  52 24 F0 AA  AA FF A5 AB   44 45 54 78  5E EC BD 3F                                      R$......DETx^..?
00000060  8E 64 CD 71  BD 2D 8B 20   20 80 90 41  83 02 08 D0                                      .d.q.-.  ..A....
00000070  F9 ED 40 A0  F3 6E 40 7B   90 23 8F 1E  D7 20 8B 3E                                      ..@..n@{.#... .>
```

Después de hacer las correcciones necesarias, queda de la siguiente manera:

```shell
File: mystery                                                        ASCII Offset: 0x00000055 / 0x000318BB (%00)  M
00000000  89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  49 48 44 52                                      .PNG........IHDR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB                                      ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00                                      x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00                                      ..gAMA......a...
00000040  00 09 70 48  59 73 00 00   16 25 00 00  16 25 01 49                                      ..pHYs...%...%.I
00000050  52 24 F0 00  00 FF A5 49   44 41 54 78  5E EC BD 3F                                      R$.....IDATx^..?
00000060  8E 64 CD 71  BD 2D 8B 20   20 80 90 41  83 02 08 D0                                      .d.q.-.  ..A....
00000070  F9 ED 40 A0  F3 6E 40 7B   90 23 8F 1E  D7 20 8B 3E                                      ..@..n@{.#... .>
```

Procedemos a revisar si tenemos más errores usando nuevamente la herramienta pngcheck:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/c0rrupt]
└─$ pngcheck -v mystery
File: mystery (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 5669x5669 pixels/meter (144 dpi)
  chunk IDAT at offset 0x00057, length 65445
    zlib: deflated, 32K window, fast compression
  chunk IDAT at offset 0x10008, length 65524
  chunk IDAT at offset 0x20008, length 65524
  chunk IDAT at offset 0x30008, length 6304
  chunk IEND at offset 0x318b4, length 0
No errors detected in mystery (9 chunks, 96.3% compression).
```

Como podemos ver, ya no hay errores en la imagen, por lo que ahora procedemos a abrirla, obteniendo la bandera que da solución al reto:

```
picoCTF{c0rrupt10n_1847995}
```
### Notas Adicionales

### Referencias
https://en.wikipedia.org/wiki/List_of_file_signatures