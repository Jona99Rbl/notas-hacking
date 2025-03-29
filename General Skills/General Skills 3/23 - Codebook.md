### Descripción
Run the Python script `code.py` in the same directory as `codebook.txt`.

- [Download code.py](https://artifacts.picoctf.net/c/3/code.py)
- [Download codebook.txt](https://artifacts.picoctf.net/c/3/codebook.txt)
### Solución
En este caso iniciamos descargando el script de python denominado como "code.py" con el uso del comando wget:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/3/code.py
--2025-02-18 01:24:30--  https://artifacts.picoctf.net/c/3/code.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.16, 3.160.22.43, 3.160.22.92, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.16|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1278 (1.2K) [application/octet-stream]
Saving to: 'code.py'

code.py                      100%[=======================>]   1.25K  --.-KB/s    in 0s      

2025-02-18 01:24:31 (392 MB/s) - 'code.py' saved [1278/1278]
```

Ahora descargamos el archivo de texto con el uso del mismo comando mencionado anteriormente:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/3/codebook.txt
--2025-02-18 01:25:41--  https://artifacts.picoctf.net/c/3/codebook.txt
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.128, 3.160.22.92, 3.160.22.43, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.128|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 27 [application/octet-stream]
Saving to: 'codebook.txt'

codebook.txt                 100%[=======================>]     27  --.-KB/s    in 0s      

2025-02-18 01:25:41 (13.1 MB/s) - 'codebook.txt' saved [27/27]
```

Una vez descargados ambos archivos, aplicamos un comando **ls** para poder ver el contenido de ese directorio, donde claramente podemos ver que tenemos tanto a **codebook.txt** y a **runme.py**, los archivos que nos interesan en este reto:

```shell
the_robx-picoctf@webshell:~$ ls
Addadshashanammu      README.txt     big-zip-files.zip  codebook.txt  file   files.zip  ltdis.sh  static   warm
Addadshashanammu.zip  big-zip-files  code.py            enc_flag      files  flag       runme.py  strings
```

Por lo que ahora solo nos resta ejecutar el script de python con **python3** y pasándole como argumento el archivo de texto:

```shell
the_robx-picoctf@webshell:~$ python3 code.py codebook.txt 
picoCTF{c0d3b00k_455157_197a982c}
```

Una vez ejecutado el script nos arrojará la bandera buscada para darle solución a este reto:

```
picoCTF{c0d3b00k_455157_197a982c}
```
### Notas Adicionales

### Referencias