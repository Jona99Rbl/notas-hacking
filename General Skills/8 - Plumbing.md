### Descripción
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to `jupiter.challenges.picoctf.org 7480`.
### Solución
En este ejercicio también se va a utilizar netcat en el shell virtual que dispone la página de picoCTF en la sección de picoGym, donde se empleará el comando **nc** seguido del link y del puerto al cual conectarse como podemos ver a continuación:

```shell
the_robx-picoctf@webshell:~$ nc jupiter.challenges.picoctf.org 7480
```

Una vez ejecutada la linea de comando anterior, nos arroja un resultado como el siguiente

```shell
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Not a flag either
This is defintely not a flag
This is defintely not a flag
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
Not a flag either
Again, I really don't think this is a flag
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
This is defintely not a flag
```

Esto en realidad no nos dice nada es por eso que volvemos a hacer uso del comando **grep** con la palabra picoCTF para que pueda buscar una coincidencia, la cual como podemos ver, nos arroja lo siguiente:

```shell
the_robx-picoctf@webshell:~$ nc jupiter.challenges.picoctf.org 7480 | grep picoCTF
picoCTF{digital_plumb3r_06e9d954}
```

Dándonos así la bandera del problema:

```
picoCTF{digital_plumb3r_06e9d954}
```
### Notas Adicionales

### Referencias
https://www.linfo.org/pipes.html