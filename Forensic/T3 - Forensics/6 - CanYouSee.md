### Descripción
How about some hide and seek? 
Download this file [here](https://artifacts.picoctf.net/c_titan/5/unknown.zip).
### Solución
Iniciamos descargando el archivo que se nos presenta en la descripción:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/canyousee]
└─$ wget https://artifacts.picoctf.net/c_titan/5/unknown.zip   
--2025-05-10 19:18:47--  https://artifacts.picoctf.net/c_titan/5/unknown.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.61, 3.161.55.26, 3.161.55.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.61|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2252228 (2.1M) [application/octet-stream]
Saving to: ‘unknown.zip’

unknown.zip            100%[===========================>]   2.15M  3.20MB/s    in 0.7s    

2025-05-10 19:18:48 (3.20 MB/s) - ‘unknown.zip’ saved [2252228/2252228]
```

Al apreciar que es un archivo .zip comprimido, procedemos a descomprimirlo:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/canyousee]
└─$ unzip unknown.zip 
Archive:  unknown.zip
  inflating: ukn_reality.jpg 
```

Ahora procedemos a revisar el tipo de archivo que es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/canyousee]
└─$ file ukn_reality.jpg                  
ukn_reality.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 4308x2875, components 3
```

Sabiendo que es una imagen jpg, procedemos a revisar sus metadatos con la herramienta exiftool:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/canyousee]
└─$ exiftool ukn_reality.jpg 
ExifTool Version Number         : 13.10
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:02:15 17:40:17-05:00
File Access Date/Time           : 2025:05:10 19:21:39-04:00
File Inode Change Date/Time     : 2025:05:10 19:19:13-04:00
File Permissions                : -rwxrwx---
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fNGRhYmRkY2J9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4
```

Se destaca la cadena de caracteres que pareciera estar codificada en base64 en el apartado de "Attribution URL": `cGljb0NURntNRTc0RDQ3QV9ISUREM05fNGRhYmRkY2J9Cg==`, por lo que se necesitará de hacer su decodificación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/canyousee]
└─$ echo 'cGljb0NURntNRTc0RDQ3QV9ISUREM05fNGRhYmRkY2J9Cg==' | base64 -d
picoCTF{ME74D47A_HIDD3N_4dabddcb}
```

Encontrando así la bandera que da solución a este reto:

```
picoCTF{ME74D47A_HIDD3N_4dabddcb}
```
### Notas Adicionales

### Referencias