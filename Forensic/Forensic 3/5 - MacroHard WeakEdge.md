### Descripción
I've hidden a flag in this file. Can you find it? [Forensics is fun.pptm](https://mercury.picoctf.net/static/c0da20f29337e87ffb58ea987d8c596e/Forensics is fun.pptm)
### Solución
Iniciamos descargando el archivo **.pptm** proporcionado en la descripción:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/macrohard_weakedge]
└─$ wget https://mercury.picoctf.net/static/c0da20f29337e87ffb58ea987d8c596e/Forensics%20is%20fun.pptm
--2025-04-26 21:27:16--  https://mercury.picoctf.net/static/c0da20f29337e87ffb58ea987d8c596e/Forensics%20is%20fun.pptm
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 100093 (98K) [application/octet-stream]
Saving to: ‘Forensics is fun.pptm’

Forensics is fun.pptm       100%[========================================>]  97.75K  --.-KB/s    in 0.09s   

2025-04-26 21:27:16 (1.02 MB/s) - ‘Forensics is fun.pptm’ saved [100093/100093]
```

Aunque se intuye que el archivo es una presentación de diapositivas, procedemos a revisarlo:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/macrohard_weakedge]
└─$ file Forensics\ is\ fun.pptm 
Forensics is fun.pptm: Microsoft PowerPoint 2007+
```

Ahora procederemos a desenpaquetar debido a que estos archivos con la extensión **.pptm** se pueden considerar como empaquetado, con el siguiente comando:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/macrohard_weakedge]
└─$ unzip Forensics\ is\ fun.pptm 
```

Dandonos una salida como la siguiente:

```
Archive:  Forensics is fun.pptm
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: ppt/presentation.xml    
  inflating: ppt/slides/_rels/slide46.xml.rels  
  inflating: ppt/slides/slide1.xml   
  inflating: ppt/slides/slide2.xml   
  inflating: ppt/slides/slide3.xml   
  inflating: ppt/slides/slide4.xml   
  inflating: ppt/slides/slide5.xml   
  inflating: ppt/slides/slide6.xml   
  inflating: ppt/slides/slide7.xml   
  inflating: ppt/slides/slide8.xml   
  inflating: ppt/slides/slide9.xml   
  inflating: ppt/slides/slide10.xml ...
```

Una vez desempaquetado el archivo, procederemos a utilizar **visual studio code**, ya que esta nos permitirá realizar la busqueda a traves de las carpetas de una forma más sencilla. Lo cual se hará de la siguiente manera:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/macrohard_weakedge]
└─$ code .  
```

Una vez lanzado, tenemos lo siguiente:

![[Screenshot_2025-04-26_21_44_49.png]]

Después de andar revisando las carpetas, encontramos la siguiente cadena de caracteres, que aparentemente está codificada en base64:

```
Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
```

Por lo que recurrimos a la consola para hacer su decodificación hacia ASCII, lo cual se realiza de la siguiente manera:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_3/macrohard_weakedge]
└─$ echo 'Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q' | tr -d ' ' | base64 -d
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5} 
```

Dándonos así la bandera que soluciona el reto:

```
picoCTF{D1d_u_kn0w_ppts_r_z1p5}
```
### Notas Adicionales

### Referencias