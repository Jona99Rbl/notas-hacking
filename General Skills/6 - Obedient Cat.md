### Descripción
This file has a flag in plain sight (aka "in-the-clear"). [Download flag](https://mercury.picoctf.net/static/704f877da185904ec3992e7255a15c6c/flag).
### Solución
En este caso al involucrar la descarga de un archivo, se realizará de forma semejante al ejercicio anterior (**First Grep**), por lo que se volverá a hacer uso del shell virtual proporcionado por la plataforma de picoCTF (picoGym Challenges), una vez que la hayamos abierto, ingresaremos el comando **wget** junto con el link de descarga del archivo que previamente habíamos copiado de las pistas del problema, resultando en lo que muestra a continuación:

```shell
the_robx-picoctf@webshell:~$ wget https://mercury.picoctf.net/static/704f877da185904ec3992e7255a15c6c/flag
--2025-02-10 19:16:31--  https://mercury.picoctf.net/static/704f877da185904ec3992e7255a15c6c/flag
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 34 [application/octet-stream]
Saving to: 'flag.1'

flag.1                         100%[============>]      34  --.-KB/s    in 0s 

2025-02-10 19:16:31 (14.9 MB/s) - 'flag.1' saved [34/34]
```

Una vez que hemos descargado el archivo que en este caso se llama *flag*, procederemos a usar el comando **cat** para leer el contenido del archivo, donde según el resultado, veremos si hace falta volver a utilizar **grep**, o en este caso solo con el primero basta, dicho resultado se muestra enseguida:

```shell
the_robx-picoctf@webshell:~$ cat flag
picoCTF{s4n1ty_v3r1f13d_1a94e0f9}
```

Como podemos ver, en este caso no hizo falta hacer uso de **grep**, por lo que obtuvimos nuestra bandera de forma rápida, la cual es:

```
picoCTF{s4n1ty_v3r1f13d_1a94e0f9}
```
### Notas Adicionales

### Referencias
https://www.freecodecamp.org/espanol/news/comandos-de-linux/