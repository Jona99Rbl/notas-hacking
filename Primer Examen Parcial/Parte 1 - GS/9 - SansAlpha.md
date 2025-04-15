### Descripción
The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols.`ssh -p 55479 ctf-player@mimas.picoctf.net`Use password: `84b12bae`
### Solución
Iniciamos realizando la conexión ssh al servidor proporcionado por la descripción del reto después de iniciada la instancia del desafío, donde solo colocamos la contraseña proporcionada ahí mismo:

```
the_robx-picoctf@webshell:~$ ssh -p 55479 ctf-player@mimas.picoctf.net
ctf-player@mimas.picoctf.net's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 6.5.0-1016-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Last login: Fri Apr 11 02:04:55 2025 from 127.0.0.1
SansAlpha$  
```

Una vez hemos accedido, probamos dos comandos básicos. los cuales no son ejecutados, ya que nos marcan que tienen un carácter desconocido:

```shell
SansAlpha$ ls
SansAlpha: Unknown character detected
SansAlpha$ cat
SansAlpha: Unknown character detected
```

Es entonces que se intenta probar con caracteres especiales, hasta que con el asterisco por fin reconoce un comando y se permite la interacción con el diagonal:

```shell
SansAlpha$ *
bash: blargh: command not found

SansAlpha$ */*
bash: blargh/flag.txt: Permission denied
```

Luego se prueba con el signo de cierre de interrogación, el cual nos permite manipular directorios según la cantidad que sea empleada

```shell
SansAlpha$ /*/???
E: Invalid operation /bin/awk

SansAlpha$ /*/??????
/bin/base32: extra operand ‘/bin/base64’
Try '/bin/base32 --help' for more information.
```

Después de enterarnos que existe una carpeta de base 64, procedemos a acceder a ese directorio y a manipular las cadenas de caracteres en este caso para que no nos aparezcan directorios que contengan un guión bajo:

```shell
SansAlpha$ /*/????64 */*
/bin/base64: extra operand ‘/bin/x86_64’
Try '/bin/base64 --help' for more information.

SansAlpha$ /*/???[!_]64 */*
/bin/base64: extra operand ‘blargh/flag.txt’
Try '/bin/base64 --help' for more information.
```

Por último buscamos en los archivos del directorio raíz que involucren el número 64 sin guión bajo, donde como resultado de esa ejecución nos aparece una cadena codificada en base64:

```shell
SansAlpha$ /*/???[!_]64 */????.*
cmV0dXJuIDAgcGljb0NURns3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV9iMGQ1ZTg1NX0=
```

Por lo que haciendo uso de la función echo, procedemos a decodificarlo:

```shell
SansAlpha$ exit
Connection to mimas.picoctf.net closed.
the_robx-picoctf@webshell:~$ echo cmV0dXJuIDAgcGljb0NURns3aDE1X211MTcxdjNyNTNfMTVfbTRkbjM1NV9iMGQ1ZTg1NX0= | base64 -d
return 0 picoCTF{7h15_mu171v3r53_15_m4dn355_b0d5e855}
```

Arrojándonos así la bandera que da solución a este reto:

```
picoCTF{7h15_mu171v3r53_15_m4dn355_b0d5e855}
```
### Notas Adicionales

### Referencias