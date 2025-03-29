### Descripción
Can you crack the password to get the flag? Download the password checker [here](https://artifacts.picoctf.net/c/16/level3.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/16/level3.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/16/level3.hash.bin) in the same directory too. There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.
### Solución
Iniciamos descargando el script del password checker:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/16/level3.py
--2025-02-18 03:56:24--  https://artifacts.picoctf.net/c/16/level3.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.92, 3.160.22.16, 3.160.22.43, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.92|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1337 (1.3K) [application/octet-stream]
Saving to: 'level3.py'

level3.py                  100%[=======================>]    1.31K  --.-KB/s    in 0s      

2025-02-18 03:56:24 (562 MB/s) - 'level3.py' saved [1337/1337]
```

Ahora descargamos la bandera encriptada

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/16/level3.flag.txt.enc
--2025-02-18 03:57:50--  https://artifacts.picoctf.net/c/16/level3.flag.txt.enc
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.128, 3.160.22.92, 3.160.22.16, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.128|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 31 [application/octet-stream]
Saving to: 'level3.flag.txt.enc'

level3.flag.txt.enc           100%[=======================>]       31  --.-KB/s    in 0s      

2025-02-18 03:57:51 (429 KB/s) - 'level3.flag.txt.enc' saved [31/31]
```

Y por ultimo el hash

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/16/level3.hash.bin
--2025-02-18 03:59:52--  https://artifacts.picoctf.net/c/16/level3.hash.bin
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.43, 3.160.22.92, 3.160.22.16, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.43|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16 [application/octet-stream]
Saving to: 'level3.hash.bin'

level3.hash.bin        100%[=======================>]      16  --.-KB/s    in 0s   

2025-02-18 03:59:52 (12.5 MB/s) - 'level3.hash.bin' saved [16/16]
```

Ahora procedemos a realizar la apertura del script de python con el editor de texto a través de **nano**:

```shell
the_robx-picoctf@webshell:~$ nano level3.py
```

Por lo que una vez abierto observaremos el siguiente código, donde al revisarlo cuidadosamente encontramos la siguiente línea al igual que en los dos ejercicios retos anteriores de este mismo tipo: `if( user_pw_hash == correct_pw_hash ):`.
En este caso no es fácil determinar la contraseña ya que la comparación nos redirige a otra línea del código, la cual es: `correct_pw_hash = open('level3.hash.bin', 'rb').read()`.

```python
import hashlib

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

flag_enc = open('level3.flag.txt.enc', 'rb').read()

correct_pw_hash = open('level3.hash.bin', 'rb').read()


def hash_pw(pw_str):

    pw_bytes = bytearray()

    pw_bytes.extend(pw_str.encode())

    m = hashlib.md5()

    m.update(pw_bytes)

    return m.digest()

  
  
def level_3_pw_check():

    user_pw = input("Please enter correct password for flag: ")

    user_pw_hash = hash_pw(user_pw)

    if( user_pw_hash == correct_pw_hash ):

        print("Welcome back... your flag, user:")

        decryption = str_xor(flag_enc.decode(), user_pw)

        print(decryption)

        return

    print("That password is incorrect")


level_3_pw_check()


# The strings below are 7 possibilities for the correct password.

#   (Only 1 is correct)

pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
```

Es por esto que recurrimos a revisar el archivo hash que descargamos al inicio, puesto a que ahí se podría encontrar la contraseña solicitada para este reto, dado que el archivo es binario investigando en internet, se encontró el comando **bvi**, el cual nos permite hacer ediciones en archivos binarios

```shell
the_robx-picoctf@webshell:~$ bvi level3.hash.bin
```

Al abrir el archivo binario, encontramos la siguiente contraseña codificada:

```
1B 18 E1 31 6F 92 18 CC 5B 05 3E 1C EA 28 E0 2E
```

Después de estar investigando en internet nuevamente, se encontró que la contraseña estaba codificada mediante el algoritmo ***md5*** y esto fue confirmado después con una herramienta llamada *CrackStation*, la cual es un Cracker de Hash de Contraseña, donde solo colocamos la entrada de datos, es decir la secuencia contenida en el archivo binario:

```
Input > 1B18E1316F9218CC5B053E1CEA28E02E

Type = md5

Result > 865e
```

Una vez que la contraseña fue crackeada y nos es otorgada en texto, procederemos a ejecutar el script python con el comando **python3**, donde se puede apreciar el ingreso de la contraseña solicitada

```shell
the_robx-picoctf@webshell:~$ python3 level3.py 
Please enter correct password for flag: 865e
Welcome back... your flag, user:
picoCTF{m45h_fl1ng1ng_2b072a90}
```

Pudiendo obtener así la bandera que soluciona este reto:

```
picoCTF{m45h_fl1ng1ng_2b072a90}
```

### Notas Adicionales

### Referencias
https://linux.die.net/man/1/bvi
https://es.wikipedia.org/wiki/MD5
https://crackstation.net/