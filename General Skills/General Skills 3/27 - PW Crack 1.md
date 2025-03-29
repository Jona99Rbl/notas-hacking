### Descripción
Can you crack the password to get the flag? Download the password checker [here](https://artifacts.picoctf.net/c/12/level1.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/12/level1.flag.txt.enc) in the same directory too.
### Solución
Primero procedemos a descargar el script de python a través de **wget**:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/12/level1.py
--2025-02-18 03:25:34--  https://artifacts.picoctf.net/c/12/level1.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.92, 3.160.22.128, 3.160.22.43, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.92|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 876 [application/octet-stream]
Saving to: 'level1.py'

level1.py           100%[=======================>]      876  --.-KB/s    in 0s

2025-02-18 03:25:35 (444 MB/s) - 'level1.py' saved [876/876]
```

Ahora descargamos el archivo con la bandera encriptada:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/12/level1.flag.txt.enc
--2025-02-18 03:27:23--  https://artifacts.picoctf.net/c/12/level1.flag.txt.enc
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.92, 3.160.22.43, 3.160.22.128, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.92|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 30 [application/octet-stream]
Saving to: 'level1.flag.txt.enc'

level1.flag.txt.enc    100%[=======================>]    30  --.-KB/s    in 0s

2025-02-18 03:27:23 (8.79 MB/s) - 'level1.flag.txt.enc' saved [30/30]
```

Una vez descargados ambos archivos, procedemos a revisar el código del script a través de **nano**:

```
the_robx-picoctf@webshell:~$ nano level1.py 
```

A continuación se muestra el código de "level1.py", donde si nos ponemos a revisarlo con detenimiento, en este caso el mismo código trae la contraseña, como se puede observar en la siguiente línea: `if(user_pw == "8713"):`

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

flag_enc = open('level1.flag.txt.enc', 'rb').read()

def level_1_pw_check():

    user_pw = input("Please enter correct password for flag: ")

    if( user_pw == "8713"):

        print("Welcome back... your flag, user:")

        decryption = str_xor(flag_enc.decode(), user_pw)

        print(decryption)

        return

    print("That password is incorrect")

level_1_pw_check()
```

Para poner a prueba lo que suponemos es la contraseña, procedemos a salir del editor de texto y a ejecutar el script con el comando **python3**, luego ingresamos la contraseña `8713`.

```shell
the_robx-picoctf@webshell:~$ python3 level1.py
Please enter correct password for flag: 8713
Welcome back... your flag, user:
picoCTF{545h_r1ng1ng_1b2fd683}
```

Como podemos ver nuestra observación fue correcta, dado que después de ingresar la contraseña mencionada, nos arrojó la bandera que daba solución al reto:

```
picoCTF{545h_r1ng1ng_1b2fd683}
```
### Notas Adicionales

### Referencias