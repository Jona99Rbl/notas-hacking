### Descripción
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file? Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/8/flag2of2-final.pdf).
### Solución
Se inicia descargando el archivo presentado en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/secret_polyglot]
└─$ wget https://artifacts.picoctf.net/c_titan/8/flag2of2-final.pdf
--2025-05-10 20:14:56--  https://artifacts.picoctf.net/c_titan/8/flag2of2-final.pdf
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.100, 3.161.55.64, 3.161.55.26, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3362 (3.3K) [application/octet-stream]
Saving to: ‘flag2of2-final.pdf’

flag2of2-final.pdf     100%[===========================>]   3.28K  --.-KB/s    in 0s      

2025-05-10 20:14:56 (96.3 MB/s) - ‘flag2of2-final.pdf’ saved [3362/3362]
```

Una vez descargado, se procede a averiguar que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/secret_polyglot]
└─$ file flag2of2-final.pdf 
flag2of2-final.pdf: PNG image data, 50 x 50, 8-bit/color RGBA, non-interlaced
```

Al decir que el archivo es una imagen png, procedemos a copiar el archivo para luego cambiar la extensión del archivo para poder abrirlo

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/secret_polyglot]
└─$ cp flag2of2-final.pdf flag2of2-final.png 
```

Por lo que ahora se procede a abrir ambos archivos y ver si contienen algo en ellos, el primero en ser abierto será la imagen png, donde nos aparece lo siguiente:

```
picoCTF{f1u3n7_
```

Dándonos así la primera parte de la bandera, por lo que ahora se revisará el archivo pdf, proporcionando lo siguiente:

```
1n_pn9_&_pdf_249d05c0}
```

Resultando así en la bandera que da solución al reto:

```
picoCTF{f1u3n7_1n_pn9_&_pdf_249d05c0}
```
### Notas Adicionales

### Referencias