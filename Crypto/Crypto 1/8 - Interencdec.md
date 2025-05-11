### Descripción
Can you get the real meaning from this file. 
Download the file [here](https://artifacts.picoctf.net/c_titan/1/enc_flag).
### Solución
Iniciamos descargando el archivo que nos es proporcionado en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1/interencdec]
└─$ wget https://artifacts.picoctf.net/c_titan/1/enc_flag
--2025-05-11 19:36:05--  https://artifacts.picoctf.net/c_titan/1/enc_flag
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.64, 3.161.55.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 73 [application/octet-stream]
Saving to: ‘enc_flag’

enc_flag               100%[===========================>]      73  --.-KB/s    in 0s      

2025-05-11 19:36:05 (30.3 MB/s) - ‘enc_flag’ saved [73/73]
```

Una vez descargado, procedemos a abrir el archivo, donde encontramos lo siguiente:

```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyeG9OakJzTURCcGZRPT0nCg==
```

Como al final se encuentran dos signos igual (=), se intuye que el texto se encuentra codificado en base64, por lo que usando CyberChef, procedemos a decodificarlo de la siguiente manera:

```
Input > YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyeG9OakJzTURCcGZRPT0nCg==

Recipe > From Base64

Output > b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2xoNjBsMDBpfQ=='
```

La salida obtenida es otra cadena codificada en base64, por lo que otra vez se vuelve a usar la misma herramienta, como se muestra a continuación:

```
Input > d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2xoNjBsMDBpfQ==

Recipe > From Base64

Output > wpjvJAM{jhlzhy_k3jy9wa3k_lh60l00i}
```

Ahora esta nueva salida se aprecia con un formato semejante al que han tenido todas las banderas de los retos picoCTF, pero ahora se puede ver que está cifrado con un método de rotación, el cual se intuye que es ROT13, por lo cual se vuelve a emplear la misma herramienta:

```
Input > wpjvJAM{jhlzhy_k3jy9wa3k_lh60l00i}

Recipe > ROT13 (Rotate numbers amount 19)

Output > picoCTF{caesar_d3cr9pt3d_ea60e00b}
```

Encontrando así la bandera que da solución a este reto:

```
picoCTF{caesar_d3cr9pt3d_ea60e00b}
```
### Notas Adicionales

### Referencias
https://gchq.github.io/CyberChef/
