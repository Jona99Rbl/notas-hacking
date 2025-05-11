### Descripción
Decrypt this [message](https://jupiter.challenges.picoctf.org/static/6385b895dcb30c74dbd1f0ea271e3563/ciphertext).
### Solución
Iniciamos descargando el mensaje que tenemos en la descripción:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1/caesar]
└─$ wget https://jupiter.challenges.picoctf.org/static/6385b895dcb30c74dbd1f0ea271e3563/ciphertext     
--2025-05-11 00:29:23--  https://jupiter.challenges.picoctf.org/static/6385b895dcb30c74dbd1f0ea271e3563/ciphertext
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 35 [application/octet-stream]
Saving to: ‘ciphertext’

ciphertext             100%[===========================>]      35  --.-KB/s    in 0s      

2025-05-11 00:29:23 (19.1 MB/s) - ‘ciphertext’ saved [35/35]
```

Procedemos a revisar que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1/caesar]
└─$ file ciphertext     
ciphertext: ASCII text, with no line terminators
```

Una vez que sabemos que es una cadena de texto en ASCII, procedemos a revisar su contenido: 

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1/caesar]
└─$ cat ciphertext 
picoCTF{dspttjohuifsvcjdpoabrkttds}
```

Encontramos la estructura de la bandera, pero lo que se encuentra entre corchetes, parece estar codificado, por lo que después de investigar en la red, encontramos que corresponde a una codificación Caesar, esta es una forma simple y antigua de encriptar mensajes.

Una vez conocido esto, se procede a utilizar una herramienta como CyberChef para realizar esa tarea, siguiendo la siguiente receta:

```
Input > dspttjohuifsvcjdpoabrkttds

Recipe > ROT13 (Rotate numbers amount 25)

Output > crossingtherubiconzaqjsscr
```

Por lo que se hace la sustitución en la estructura de la bandera original, dándonos la que resuelve este reto:

```
picoCTF{crossingtherubiconzaqjsscr}
```
### Notas Adicionales
También puede hacerse con un script de python:

```python
import string
import re

abc = string.ascii_lowercase  

with open('ciphertext', 'r') as f:
    contenido = f.read()


encriptado = re.findall(r'\{(.*?)\}', contenido)[0]

rot = 25
salida = ''

for car in encriptado:
    if car in abc:
        salida += abc[(abc.find(car) + rot) % 26]
    else:
        salida += car  

print(salida)

```
### Referencias
https://learncryptography.com/classical-encryption/caesar-cipher