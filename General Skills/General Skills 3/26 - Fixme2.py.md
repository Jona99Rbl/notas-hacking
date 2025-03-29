### Descripción
Fix the syntax error in the Python script to print the flag.[Download Python script](https://artifacts.picoctf.net/c/6/fixme2.py)
### Solución
Procedemos a realizar la descarga del script de python que contiene un error de sintaxis mediante el comando **wget**

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/6/fixme2.py
--2025-02-18 02:01:40--  https://artifacts.picoctf.net/c/6/fixme2.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.128, 3.160.22.43, 3.160.22.92, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.128|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1029 (1.0K) [application/octet-stream]
Saving to: 'fixme2.py'

fixme2.py                   100%[=======================>]  1.00K  --.-KB/s    in 0s      

2025-02-18 02:01:41 (265 MB/s) - 'fixme2.py' saved [1029/1029]
```

Cuando ya lo hemos descargado, procederemos a abrir el código de python en un editor mediante el comando **nano**:

```shell
the_robx-picoctf@webshell:~$ nano fixme2.py 
```

Ejecutado el comando veremos el siguiente código, a primera vista el código parece estar correcto como en el caso del ejercicio anterior, pues se aprecia que todo tiene la identación correcta, no hay palabras mal escritas o algo así, no es hasta que vemos la comparación de `if flag = ""` que vemos el error, puesto que esta se debe de hacer con doble signo de igual (=)

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

flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x58) + chr(0x18) + chr(0x11) + chr(0x41) + chr(0x09) + chr(0x5f) + chr(0x1f) + chr(0x10) + chr(0x3b) + chr(0x1b) + chr(0x55) + chr(0x1a) + chr(0x34) + chr(0x5d) + chr(0x51) + chr(0x40) + chr(0x54) + chr(0x09) + chr(0x05) + chr(0x04) + chr(0x57) + chr(0x1b) + chr(0x11) + chr(0x31) + chr(0x0d) + chr(0x5f) + chr(0x05) + chr(0x40) + chr(0x04) + chr(0x0b) + chr(0x0d) + chr(0x0a) + chr(0x19)

flag = str_xor(flag_enc, 'enkidu')

# Check that flag is not empty

if flag = "":

  print('String XOR encountered a problem, quitting.')

else:

  print('That is correct! Here\'s your flag: ' + flag)
```

Realizada la corrección que consiste en agregar otro signo "=" en la comparación, resultando en lo siguiente if flag == "", como se aprecia en el siguiente código ya corregido: 

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

flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x58) + chr(0x18) + chr(0x11) + chr(0x41) + chr(0x09) + chr(0x5f) + chr(0x1f) + chr(0x10) + chr(0x3b) + chr(0x1b) + chr(0x55) + chr(0x1a) + chr(0x34) + chr(0x5d) + chr(0x51) + chr(0x40) + chr(0x54) + chr(0x09) + chr(0x05) + chr(0x04) + chr(0x57) + chr(0x1b) + chr(0x11) + chr(0x31) + chr(0x0d) + chr(0x5f) + chr(0x05) + chr(0x40) + chr(0x04) + chr(0x0b) + chr(0x0d) + chr(0x0a) + chr(0x19)

flag = str_xor(flag_enc, 'enkidu')

# Check that flag is not empty

if flag == "":

  print('String XOR encountered a problem, quitting.')

else:

  print('That is correct! Here\'s your flag: ' + flag)
```

Una vez corregido, guardamos esos cambios y procederemos a ejecutarlo con el comando **python3**:

```shell
the_robx-picoctf@webshell:~$ python3 fixme2.py
That is correct! Here's your flag: picoCTF{3qu4l1ty_n0t_4551gnm3nt_f6a5aefc}
```

La modificación fue correcta debido a que nos da la bandera que se requiere para solucionar el presente reto:

```
picoCTF{3qu4l1ty_n0t_4551gnm3nt_f6a5aefc}
```
### Notas Adicionales

### Referencias