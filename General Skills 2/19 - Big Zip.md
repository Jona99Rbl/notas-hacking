### Descripción
Unzip this archive and find the flag.

- [Download zip file](https://artifacts.picoctf.net/c/503/big-zip-files.zip)
### Solución
Empezamos descargando el archivo **.zip**, para lo cual usamos el comando wget, como podemos ver a continuación:
```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/503/big-zip-files.zip
--2025-02-16 05:22:23--  https://artifacts.picoctf.net/c/503/big-zip-files.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.43, 3.160.22.92, 3.160.22.128, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.43|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3182988 (3.0M) [application/octet-stream]
Saving to: 'big-zip-files.zip.'

big-zip-files.zip.       100%[=======================>]  3.04M  1.82MB/s    in 1.7s

2025-02-16 05:22:25 (1.82 MB/s) - 'big-zip-files.zip.' saved [3182988/3182988]
```

Una vez descargado, procederemos a descomprimirlo, para lo cual usaremos nuevamente el comando **unzip**, el cual nos extraerá todas las carpetas contenidas en el comprimido.

```
the_robx-picoctf@webshell:~$ unzip big-zip-files.zip
```

Cuando hayamos finalizado la descomprensión del paquete, usamos el comando **ls** para saber el contenido del directorio donde podemos ver la carpeta big-zip-files resultante después de la extracción, como podemos ver a continuación:

```shell
the_robx-picoctf@webshell:~$ ls
Addadshashanammu  Addadshashanammu.zip  README.txt  big-zip-files  big-zip-files.zip  enc_flag  file  flag  ltdis.sh  static  strings  warm
```

Ahora con **cd** cambiamos de directorio e ingresamos a la carpeta de big-zip-files, donde usaremos el comando **grep** para buscar coincidencias de cadenas de texto, además del argumento **-r** para realizar una búsqueda recursiva, es decir no solo buscará en el directorio actual, si no también en los demás subdirectorios, tal como se muestra:

```shell
the_robx-picoctf@webshell:~$ cd big-zip-files/
the_robx-picoctf@webshell:~/big-zip-files$ grep -r pico
folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}
```

Con lo cual hemos obtenido la bandera que da solución a este reto:

```
picoCTF{gr3p_15_m4g1c_ef8790dc}
```
### Notas Adicionales

### Referencias
https://www.hostinger.mx/tutoriales/comando-grep-linux