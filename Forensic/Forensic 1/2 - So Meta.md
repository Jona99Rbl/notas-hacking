### Descripción
Find the flag in this [picture](https://jupiter.challenges.picoctf.org/static/00efdf2961da1e21470ffc0d496c3cc2/pico_img.png).
### Solución
Iniciamos descargando la imagen en la consola, haciendo uso del comando **wget**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/so_meta]
└─$ wget https://jupiter.challenges.picoctf.org/static/00efdf2961da1e21470ffc0d496c3cc2/pico_img.png
--2025-04-03 23:12:04--  https://jupiter.challenges.picoctf.org/static/00efdf2961da1e21470ffc0d496c3cc2/pico_img.png
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 108795 (106K) [application/octet-stream]
Saving to: ‘pico_img.png’

pico_img.png                 100%[=============================================>] 106.25K  --.-KB/s    in 0.1s    

2025-04-03 23:12:05 (728 KB/s) - ‘pico_img.png’ saved [108795/108795]
```

Por lo que una vez descargado, procedemos a revisar que tipo de archivo es con el uso del comando **file**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/so_meta]
└─$ file pico_img.png                                                       
pico_img.png: PNG image data, 600 x 600, 8-bit/color RGB, non-interlaced
```

Como podemos ver, es una imagen con formato *.png*, por lo que se procede ahora a investigar sobre los **metadatos**, ya que se nos hace mención sobre ellos en las pistas del reto, siendo estos un grupo de datos que describen el contenido informativo de un objeto al que se denomina recurso.

Una vez conocido esto, procederemos a utilizar la herramienta **exiftool**, ya incluida en Kali, esto se hará a través de la consola, como se muestra a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/so_meta]
└─$ exiftool pico_img.png 
ExifTool Version Number         : 13.10
File Name                       : pico_img.png
Directory                       : .
File Size                       : 109 kB
File Modification Date/Time     : 2020:10:26 14:38:23-04:00
File Access Date/Time           : 2025:04:03 23:15:22-04:00
File Inode Change Date/Time     : 2025:04:03 23:12:07-04:00
File Permissions                : -rwxrwx---
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Warning                         : [minor] Text/EXIF chunk(s) found after PNG IDAT (may be ignored by some readers)
Artist                          : picoCTF{s0_m3ta_fec06741}
Image Size                      : 600x600
Megapixels                      : 0.360
```

Donde si nos ponemos a leer el resultado de la ejecución del comando encontraremos la bandera que da solución a este reto:

```
picoCTF{s0_m3ta_fec06741}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Metadatos