### Descripción
Can you invoke help flags for a tool or binary? [This program](https://mercury.picoctf.net/static/a14be2648c73e3cda5fc8490a2f476af/warm) has extraordinarily helpful information...
### Solución
Primeramente se procede a descargar el programa proporcionado en la descripción del reto, lo anterior con el comando **wget**:

```shell
the_robx-picoctf@webshell:~$ wget https://mercury.picoctf.net/static/a14be2648c73e3cda5fc8490a2f476af/warm
--2025-02-16 01:56:26--  https://mercury.picoctf.net/static/a14be2648c73e3cda5fc8490a2f476af/warm
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10936 (11K) [application/octet-stream]
Saving to: 'warm'

warm                  100%[=======================>]  10.68K  --.-KB/s    in 0s

2025-02-16 01:56:27 (204 MB/s) - 'warm' saved [10936/10936]
```

Para poder ejecutar el programa, el reto nos proporciona la siguiente pista:

```
Run this program by entering the following in the Terminal prompt: `$ ./warm`, but you'll first have to make it executable with `$ chmod +x warm`
```

Por lo que procedemos a iniciar con el comando **chmod**, el cual nos permite asignar permisos de acceso a carpetas y directorios, junto con el argumento **+x** se le dan permisos de ejecución, una vez otorgados, procederemos a ejecutarlo con **./warm**

```shell
the_robx-picoctf@webshell:~$ chmod +x warm
the_robx-picoctf@webshell:~$ ./warm
Hello user! Pass me a -h to learn what I can do!
```

Como podemos ver al ejecutar el programa, nos pide que le pasemos el argumento **-h**, para que este funcione de manera correcta, lo cual al hacerlo nos muestra lo siguiente:

```shell
the_robx-picoctf@webshell:~$ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_755f3544}
```

Obteniendo la bandera, que es la siguiente:

```
picoCTF{b1scu1ts_4nd_gr4vy_755f3544}
```
### Notas Adicionales

### Referencias
https://www.ionos.mx/digitalguide/servidores/know-how/asignacion-de-permisos-de-acceso-con-chmod/