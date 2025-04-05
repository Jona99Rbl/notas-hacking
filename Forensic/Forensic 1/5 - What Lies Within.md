### Descripción
There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?
### Solución
Iniciamos descargando el archivo proporcionado por la descripción con el comando **wget** en consola, como se aprecia a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/what_lies_within]
└─$ wget https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png
--2025-04-04 23:45:51--  https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 625219 (611K) [application/octet-stream]
Saving to: ‘buildings.png’

buildings.png                100%[=============================================>] 610.57K  1.76MB/s    in 0.3s    

2025-04-04 23:45:52 (1.76 MB/s) - ‘buildings.png’ saved [625219/625219]
```

Por lo que una vez que ya se descargo primero procedemos a revisar que tipo de archivo es con el comando **file**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/what_lies_within]
└─$ file buildings.png 
buildings.png: PNG image data, 657 x 438, 8-bit/color RGBA, non-interlaced
```

Como se puede ver, efectivamente es una imagen **.png**, pero como en las pistas nos hace mención de que puede haber información oculta, gracias a la ayuda de los vídeos proporcionados por el profesor, tenemos que esto se conoce como **Esteganografía**, que es la práctica de **ocultar un mensaje secreto** dentro (o incluso encima) de algo que no es secreto. En estos días, muchos **ejemplos de esteganografía** implican incrustar un texto secreto dentro de una imagen. O esconder un mensaje secreto o un script dentro de un documento de Word o Excel.

Por lo que después de descargar la herramienta **zsteg**, procederemos a utilizarla para descubrir la información oculta en la imagen del edificio, además de usar el comando **grep** para filtrar únicamente la bandera, tal como se mira a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics/what_lies_within]
└─$ zsteg buildings.png | grep picoCTF
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"
```

Por lo cual hemos obtenido la bandera requerida para resolver el reto, siendo esta:

```
picoCTF{h1d1ng_1n_th3_b1t5}
```
### Notas Adicionales

### Referencias
https://ayudaleyprotecciondatos.es/2021/03/17/esteganografia/
https://www.simplilearn.com/what-is-steganography-article
https://stylesuxx.github.io/steganography/