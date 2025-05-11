### Descripción
Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://mercury.picoctf.net/static/e5825f58ef798fdd1af3f6013592a971/cat.jpg)
### Solución
Iniciamos descargando la imagen denominada como **cat.jpg** con el comando wget:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/information]
└─$ wget https://mercury.picoctf.net/static/e5825f58ef798fdd1af3f6013592a971/cat.jpg
--2025-05-09 22:50:17--  https://mercury.picoctf.net/static/e5825f58ef798fdd1af3f6013592a971/cat.jpg
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 878136 (858K) [application/octet-stream]
Saving to: ‘cat.jpg’

cat.jpg                100%[===========================>] 857.55K  1.48MB/s    in 0.6s    

2025-05-09 22:50:18 (1.48 MB/s) - ‘cat.jpg’ saved [878136/878136]
```

Una vez descargado, procedemos a revisar los metadatos con **exiftool**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/information]
└─$ exiftool cat.jpg     
ExifTool Version Number         : 13.10
File Name                       : cat.jpg
Directory                       : .
File Size                       : 878 kB
File Modification Date/Time     : 2021:03:15 14:24:46-04:00
File Access Date/Time           : 2025:05:09 22:50:18-04:00
File Inode Change Date/Time     : 2025:05:09 22:50:18-04:00
File Permissions                : -rwxrwx---
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
```

De aquí se destaca la cadena de caracteres contenida en el campo de "LIcense": `cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9`, dicha cadena parece estar codificada en base64, por lo que procedemos a hacer su decodificación en ASCII:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/information]
└─$ echo 'cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9' | base64 -d
picoCTF{the_m3tadata_1s_modified}  
```

Obteniendo la bandera que da solución a este reto:

```
picoCTF{the_m3tadata_1s_modified} 
```
### Notas Adicionales

### Referencias