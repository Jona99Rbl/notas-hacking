### Descripción
Can you crack the password to get the flag? Download the password checker [here](https://artifacts.picoctf.net/c/14/level2.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/14/level2.flag.txt.enc) in the same directory too.
### Solución
Comenzamos descargando el script de python para este reto con el comando **wget**

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/14/level2.py
--2025-02-18 03:37:01--  https://artifacts.picoctf.net/c/14/level2.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.43, 3.160.22.92, 3.160.22.16, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.43|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 914 [application/octet-stream]
Saving to: 'level2.py'

level2.py                    100%[=======================>]     914  --.-KB/s    in 0s      

2025-02-18 03:37:01 (297 MB/s) - 'level2.py' saved [914/914]
```

En seguida descargamos la bandera encriptada

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/14/level2.flag.txt.enc
--2025-02-18 03:38:13--  https://artifacts.picoctf.net/c/14/level2.flag.txt.enc
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.128, 3.160.22.43, 3.160.22.92, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.128|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 31 [application/octet-stream]
Saving to: 'level2.flag.txt.enc'

level2.flag.txt.enc          100%[=======================>]     31  --.-KB/s    in 0s      

2025-02-18 03:38:13 (16.5 MB/s) - 'level2.flag.txt.enc' saved [31/31]
```

Una vez más lanzamos el editor de texto para observar el código de python contenido en el script a través de **nano**:

```
the_robx-picoctf@webshell:~$ nano level2.py 
```

Abierto el script, tenemos el siguiente código donde encontramos una línea que contiene la contraseña, pues al igual que en el ejercicio anterior tenemos la siguiente línea: `if( user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39) ):`

```python
### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################

def str_xor(secret, key):

    #extend key to secret length

    new_key = key

    i = 0

    while len(new_key) < len(secret):

        new_key = new_key + key[i]

        i = (i + 1) % len(key)        

    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])

###############################################################################

flag_enc = open('level2.flag.txt.enc', 'rb').read()
 

def level_2_pw_check():

    user_pw = input("Please enter correct password for flag: ")

    if( user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39) ):

        print("Welcome back... your flag, user:")

        decryption = str_xor(flag_enc.decode(), user_pw)

        print(decryption)

        return

    print("That password is incorrect")


level_2_pw_check()
```

Dado a que el formato en que viene codificada la contraseña es hexadecimal, requerimos de una herramienta para poder hacer la conversión a código ASCII, por lo que hacemos uso de Cyberchef con la siguiente receta:

```
Input > 34 65 63 39

Recipe > From Hex

Output > 4ec9
```

Ahora que ya tenemos la contraseña en código ASCII procedemos a probarla ejecutando el script con el comando **python3**, en donde podemos ver que la contraseña resultó correcta.

```shell
the_robx-picoctf@webshell:~$ python3 level2.py
Please enter correct password for flag: 4ec9
Welcome back... your flag, user:
picoCTF{tr45h_51ng1ng_9701e681}
```

Dándonos la bandera para solucionar este reto:

```
picoCTF{tr45h_51ng1ng_9701e681}
```
### Notas Adicionales

### Referencias
https://gchq.github.io/CyberChef/