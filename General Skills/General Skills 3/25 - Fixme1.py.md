### Descripción
Fix the syntax error in this Python script to print the flag.[Download Python script](https://artifacts.picoctf.net/c/25/fixme1.py)
### Solución
Iniciamos descargando el código de Python al cual debemos encontrar un error en su sintaxis, lo anterior como ya es costumbre lo haremos con el comando **wget**:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/25/fixme1.py
--2025-02-18 01:38:57--  https://artifacts.picoctf.net/c/25/fixme1.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.43, 3.160.22.16, 3.160.22.128, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.43|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 837 [application/octet-stream]
Saving to: 'fixme1.py'

fixme1.py               100%[=======================>]     837  --.-KB/s    in 0s      

2025-02-18 01:38:58 (507 MB/s) - 'fixme1.py' saved [837/837]
```

Una vez que lo hemos descargado, procederemos a abrirlo desde la shell mediante el comando **nano**:

```shell
the_robx-picoctf@webshell:~$ nano fixme1.py
```

Ejecutado el comando veremos el siguiente código en python, el cual aparentemente se encuentra correcto, pero no es hasta la última línea donde se aprecia una identación incorrecta del **print**, lo cual nos impediría ejecutar el script:

```python
import random


def str_xor(secret, key):

    #extend key to secret length

    new_key = key

    i = 0

    while len(new_key) < len(secret):

        new_key = new_key + key[i]

        i = (i + 1) % len(key)        

    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])

flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x5a) + chr(0x07) + chr(0x00) + chr(0x46) + chr(0x0b) + chr(0x1a) + chr(0x5a) + chr(0x1d) + chr(0x1d) + chr(0x2a) + chr(0x06) + chr(0x1c) + chr(0x5a) + chr(0x5c) + chr(0x55) + chr(0x40) + chr(0x3a) + chr(0x58) + chr(0x0a) + chr(0x5d) + chr(0x53) + chr(0x43) + chr(0x06) + chr(0x56) + chr(0x0d) + chr(0x14) 

flag = str_xor(flag_enc, 'enkidu')

  print('That is correct! Here\'s your flag: ' + flag)
```

Una vez corregido el código al darle la correcta identación a print, obtendremos el siguiente código donde no se aprecian grandes cambios:

```python
import random


def str_xor(secret, key):

    #extend key to secret length

    new_key = key

    i = 0

    while len(new_key) < len(secret):

        new_key = new_key + key[i]

        i = (i + 1) % len(key)        

    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])

flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x5a) + chr(0x07) + chr(0x00) + chr(0x46) + chr(0x0b) + chr(0x1a) + chr(0x5a) + chr(0x1d) + chr(0x1d) + chr(0x2a) + chr(0x06) + chr(0x1c) + chr(0x5a) + chr(0x5c) + chr(0x55) + chr(0x40) + chr(0x3a) + chr(0x58) + chr(0x0a) + chr(0x5d) + chr(0x53) + chr(0x43) + chr(0x06) + chr(0x56) + chr(0x0d) + chr(0x14) 

flag = str_xor(flag_enc, 'enkidu')

print('That is correct! Here\'s your flag: ' + flag)
```

Una vez que guardamos las modificaciones realizadas, procedemos a ejecutar el script con el comando **python3**

```shell
the_robx-picoctf@webshell:~$ python3 fixme1.py 
That is correct! Here's your flag: picoCTF{1nd3nt1ty_cr1515_6a476c8f}
```

Como podemos ver, se pudo corregir la falla presente en este código, ya que no nos marcó algún error o advertencia, además de arrojarnos la bandera que da solución a este reto:

```
picoCTF{1nd3nt1ty_cr1515_6a476c8f}
```
### Notas Adicionales

### Referencias