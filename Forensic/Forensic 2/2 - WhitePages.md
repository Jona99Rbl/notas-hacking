### Descripción
I stopped using YellowPages and moved onto WhitePages... but [the page they gave me](https://jupiter.challenges.picoctf.org/static/95be9526e162185c741259a75dffa0ab/whitepages.txt) is all blank!
### Solución
Iniciamos descargando el archivo proporcionado en la descripción del reto con el comando **wget**: 

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/white_pages]
└─$ wget https://jupiter.challenges.picoctf.org/static/95be9526e162185c741259a75dffa0ab/whitepages.txt
--2025-04-25 13:57:06--  https://jupiter.challenges.picoctf.org/static/95be9526e162185c741259a75dffa0ab/whitepages.txt
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2976 (2.9K) [application/octet-stream]
Saving to: ‘whitepages.txt’

whitepages.txt               100%[=============================================>]   2.91K  --.-KB/s    in 0.001s  

2025-04-25 13:57:06 (2.20 MB/s) - ‘whitepages.txt’ saved [2976/2976]
```

Ahora descargado, procedemos a revisar que tipo de archivo es con el comando **file**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/white_pages]
└─$ file whitepages.txt 
whitepages.txt: Unicode text, UTF-8 text, with very long lines (1376), with no line terminators
```

Como podemos ver, es un archivo de texto **Unicode**, con el formato **UTF-8**, por lo que investigando en internet, tenemos lo que es un estándar y un formato respectivamente en la codificación de caracteres.

Se intentó hacer un **cat** al archivo, pero aparentemente no contiene nada, por lo que procedemos a revisar la codificación hexadecimal del encabezado con el comando **xxd**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/white_pages]
└─$ xxd whitepages.txt | head
00000000: e280 83e2 8083 e280 83e2 8083 20e2 8083  ............ ...
00000010: 20e2 8083 e280 83e2 8083 e280 83e2 8083   ...............
00000020: 20e2 8083 e280 8320 e280 83e2 8083 e280   ...... ........
00000030: 83e2 8083 20e2 8083 e280 8320 e280 8320  .... ...... ... 
00000040: 2020 e280 83e2 8083 e280 83e2 8083 e280    ..............
00000050: 8320 20e2 8083 20e2 8083 e280 8320 e280  .  ... ...... ..
00000060: 8320 20e2 8083 e280 83e2 8083 2020 e280  .  .........  ..
00000070: 8320 20e2 8083 2020 2020 e280 8320 e280  .  ...    ... ..
00000080: 83e2 8083 e280 83e2 8083 2020 e280 8320  ..........  ... 
00000090: e280 8320 e280 8320 e280 83e2 8083 e280  ... ... ........
```

Revisando lo anterior, tenemos la repetición del código Unicode `e28083e` por lo que al buscar en red que significa, obtenemos que es un espacio, por lo que ahora se entiende el resultado de ejecución del comando **cat**, donde los `20` que se ven corresponden al código hexadecimal correspondiente a un espacio, teniendo así dos tipos de espacios.

Es entonces que se procede a instalar una librería de python que nos permitirá trabajar con archivos binarios, dicha librería es *pwntools*, una vez instalada, procederemos a crear un script como el siguiente:

```python                                                 
from pwn import *

file = open('whitepages.txt', 'rb')
data = bytearray(file.read())
data = data.replace(b'\xe2\x80\x83',b'0')
data = data.replace(b'\x20',b'1')
data = data.decode('ascii')
data = unbits(data)

print(data)
```

Una vez codificado el script, procedemos a ejecutarlo con el comando **python**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/white_pages]
└─$ python exp.py
b'\n\t\tpicoCTF\n\n\t\tSEE PUBLIC RECORDS & BACKGROUND REPORT\n\t\t5000 Forbes Ave, Pittsburgh, PA 15213\n\t\tpicoCTF{not_all_spaces_are_created_equal_7100860b0fa779a5bd8ce29f24f586dc}\n\t\t'
```

Obteniendo así la bandera que da solución a este reto:

```
picoCTF{not_all_spaces_are_created_equal_7100860b0fa779a5bd8ce29f24f586dc}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Unicode
https://es.wikipedia.org/wiki/UTF-8