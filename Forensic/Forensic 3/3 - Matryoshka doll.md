### Descripción
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [this](https://mercury.picoctf.net/static/f6cc2560a70b1ea811c151accba5390f/dolls.jpg)
### Solución
Iniciamos descargando la imagen que no es proporcionada en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/matrioshka_doll]
└─$ wget https://mercury.picoctf.net/static/f6cc2560a70b1ea811c151accba5390f/dolls.jpg              
--2025-04-26 12:56:13--  https://mercury.picoctf.net/static/f6cc2560a70b1ea811c151accba5390f/dolls.jpg
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 651635 (636K) [application/octet-stream]
Saving to: ‘dolls.jpg’

dolls.jpg                   100%[========================================>] 636.36K  1.81MB/s    in 0.3s    

2025-04-26 12:56:14 (1.81 MB/s) - ‘dolls.jpg’ saved [651635/651635]
```

Se revisa la imagen pero no contiene nada a simple vista, por lo que se procede a aplicar un comando strings, obteniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/matrioshka_doll]
└─$ strings -n 10  dolls.jpg
eiCCPICC Profile
Screenshot
iTXtXML:com.adobe.xmp
<x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="XMP Core 5.4.0">
   <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
      <rdf:Description rdf:about=""
            xmlns:exif="http://ns.adobe.com/exif/1.0/">
         <exif:PixelXDimension>594</exif:PixelXDimension>
         <exif:UserComment>Screenshot</exif:UserComment>
         <exif:PixelYDimension>1104</exif:PixelYDimension>
      </rdf:Description>
   </rdf:RDF>
</x:xmpmeta>
IDEEb^*Qcb4
Z9vT?vA/_$
a#;s;[gyjD
n3zY[>GAD
=,e< =*?Yp
3Sn'&bbGf'
\sMKn$R`eG
~wkwwG;~A
base_images/2_c.jpgUT
C}-Zjvj"""Z
/\6c7l*18Mj
Hr~&    8Ja7i,
t+Vp`B2AYq
se\45~|_4Z
%(oQ1y~?e?
Db^!u"tE=O
9)IZ9Rj|Fn
|YrAkJI_S,
cG3CKkcs3G
=T*N+b_Io8
-8(Ly<7-"`
kT_S0/,0L3
mlKszlh<f$
>,\vxk~[        .R
l_(ZU2&?IX
>KO<K-j3|sD
base_images/2_c.jpgUT

```

De lo anterior se destaca que aparece lo que pudiera ser una imagen dentro de la imagen, para poderlo comprobar, vamos ahora a hacer uso de la herramienta **binwalk**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/matrioshka_doll]
└─$ binwalk dolls.jpg  

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378955, uncompressed size: 383936, name: base_images/2_c.jpg
651613        0x9F15D         End of Zip archive, footer length: 22
```

Lo anterior nos dice que se tiene la imagen **PNG**, pero también contiene un archivo *.Zip* y dentro de ese archivo tenemos otra imagen. Por lo que ahora vamos a extraer el contenido usando la misma herramienta, de la siguiente forma `binwalk -e dolls.jpg`.

Una vez extraido, revisamos si se creo una carpeta donde se tengan los archivos extraidos:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/matrioshka_doll]
└─$ ls
dolls.jpg  _dolls.jpg.extracted
```

Ahora ingresamos a la carpeta creada y procedemos a revisar su contenido:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/matrioshka_doll]
└─$ cd _dolls.jpg.extracted 

┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/matrioshka_doll/_dolls.jpg.extracted]
└─$ ls
4286C.zip  base_images
```

Ingresamos a la carpeta de "base_images", tenemos ahora otra imagen la cual procedemos a abrir y se nos muestra una matryoshka más pequeña y que hace sentido a la misma.

Por lo que volvemos a utilizar otra vez la herramienta de **binwalks**, para revisar si hay algo más dentro de la imagen, lo cual se muestra a continaución:

```shell
┌──(kali㉿kali)-[~/…/Forensics_3/matrioshka_doll/_dolls.jpg.extracted/base_images]
└─$ binwalk 2_c.jpg     

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 526 x 1106, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196041, uncompressed size: 201443, name: base_images/3_c.jpg
383803        0x5DB3B         End of Zip archive, footer length: 22
383914        0x5DBAA         End of Zip archive, footer length: 22
```

Esto nos indica que sí hay mas imagenes subsecuentes contenidas, simulando a la figura de la matrioshka, lo cual nos dice que vamos a seguir extrayendo dicha figura hasta que lleguemos a la más pequeña, la cual resulta ser la 4ta matrioshka, debido a que en la carpeta extraída tenemos lo siguiente:

```shell
┌──(kali㉿kali)-[~/…/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted]
└─$ ls
136DA.zip  flag.txt
```

Donde al aplicar un cat al archivo "flag.txt", obtenemos la siguiente salida: 

```shell
┌──(kali㉿kali)-[~/…/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted]
└─$ cat flag.txt         
picoCTF{ac0072c423ee13bfc0b166af72e25b61} 
```

Obteniendo así la bandera que da solución al reto:

```
picoCTF{ac0072c423ee13bfc0b166af72e25b61}
```
### Notas Adicionales

### Referencias