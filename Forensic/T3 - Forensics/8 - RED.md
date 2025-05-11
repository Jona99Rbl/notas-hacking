### Descripción
RED, RED, RED, RED 
Download the image: [red.png](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)
### Solución
Iniciamos descargando la imagen proporcionada en la descripción:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/red]
└─$ wget https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png
--2025-05-10 20:29:27--  https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 65.9.149.59, 65.9.149.24, 65.9.149.95, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|65.9.149.59|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 796 [application/octet-stream]
Saving to: ‘red.png’

red.png                100%[===========================>]     796  --.-KB/s    in 0s      

2025-05-10 20:29:28 (27.5 MB/s) - ‘red.png’ saved [796/796]
```

Una vez descargado, procedemos a utilizar el comando strings, dándonos el siguiente resultado:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/red]
└─$ strings red.png                         
IHDR
tEXtPoem
Crimson heart, vibrant and bold,
Hearts flutter at your sight.
Evenings glow softly red,
Cherries burst with sweet life.
Kisses linger with your warmth.
Love deep as merlot.
Scarlet leaves falling softly,
Bold in every stroke.x
IDATx
IEND
```

Si nos fijamos en las iniciales de cada párrafo, tenemos la siguiente frase: "CHECK LSB", esto se puede hacer con el comando zteg:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/red]
└─$ zsteg -a red.png                          
meta Poem           .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."         
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="                                                                             
b1,rgba,msb,xy      .. file: OpenPGP Public Key
b2,g,lsb,xy         .. text: "ET@UETPETUUT@TUUTD@PDUDDDPE"
b2,rgb,lsb,xy       .. file: OpenPGP Secret Key
b2,bgr,msb,xy       .. file: OpenPGP Public Key
b2,rgba,lsb,xy      .. file: OpenPGP Secret Key
b2,rgba,msb,xy      .. text: "CIkiiiII"
b2,abgr,lsb,xy      .. file: OpenPGP Secret Key
b2,abgr,msb,xy      .. text: "iiiaakikk"
b3,rgba,msb,xy      .. text: "#wb#wp#7p"
b3,abgr,msb,xy      .. text: "7r'wb#7p"
b3p,r,msb,xy        .. text: "{[{_[_[_{_["
b3p,g,lsb,xy        .. text: "%!%! !%!%%%!"
b3p,rgb,lsb,xy      .. file: OpenPGP Secret Key
...
```

De lo anterior se destaca la cadena de texto codificada en lo que parece ser base64, por lo que procedemos a hacer su decodificación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/red]
└─$ echo 'cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==' | base64 -d
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_} 
```

Como se aprecia, se tenía codificada varias veces la bandera que da solución al reto, siendo esta:

```
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```
### Notas Adicionales

### Referencias