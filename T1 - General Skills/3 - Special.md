### Descripción
Don't power users get tired of making spelling mistakes in the shell? Not anymore! Enter Special, the Spell Checked Interface for Affecting Linux. Now, every word is properly spelled and capitalized... automatically and behind-the-scenes! Be the first to test Special in beta, and feel free to tell us all about how Special streamlines every development process that you face. When your co-workers see your amazing shell interface, just tell them: That's Special (TM)Start your instance to see connection details.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Start your instance to see connection details.`ssh -p 59786 ctf-player@saturn.picoctf.net`The password is `d137d16e`
### Solución
Iniciamos conectándonos al servidor con la instrucción que nos da la descripción una vez iniciada la instancia del desafío, donde después tenemos que colocar la contraseña que también nos es proporcionada ahí:

```shell
the_robx-picoctf@webshell:~$ ssh -p 59786 ctf-player@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:59786 ([13.59.203.175]:59786)' can't be established.
ED25519 key fingerprint is SHA256:tJ0wuU5yBvNO/FrkHmR9iY36VJClMhKV+Hq2sxqKFmg.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:59786' (ED25519) to the list of known hosts.
ctf-player@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 6.5.0-1023-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
```

Una vez dentro podemos apreciar que cambia nuestro prompt de `the_robx-picoctf@webshell:~$` a `Special$` donde se intenta probar con el comando **ls** para descubrir que es lo que contiene el directorio actual, dicho comando nos dice que no es reconocido.

```shell
Special$ ls
Is 
sh: 1: Is: not found
```

Se prueba usar el signo ampersand (&) para probar si se pueden concatenar comandos, lo cual como podemos ver si es posible, pero en definitiva el comando **ls** no está soportado.

```shell
Special$ ls & ls
Is & is 
sh: 1: is: not found
sh: 1: Is: not found
```

Ahora se intenta con **ls** y el comando **find**, donde podemos darnos cuenta de que este shell siempre va a ignorar el primer comando ingresado y solo va a ejecutar el segundo, debido a que en el caso de find si nos arroja resultados, resaltando el que hace mención a **flag.txt**

```shell
Special$ ls & find .
Is & find . 
sh: 1: Is: not found
.
./blargh
./blargh/flag.txt
./.cache
./.cache/motd.legal-displayed
```

Por lo que se vuelve a ingresar el comando **ls**, que al final y al cabo va a ser ignorado y se usa el comando **cat** para ver el contenido de ese archivo.

```shell
Special$ ls & cat blargh/flag.txt
Is & cat blargh/flag.txt 
sh: 1: Is: not found
picoCTF{5p311ch3ck_15_7h3_w0r57_3befb794}Special$ 
```

Como se pudo comprobar mientras el primero comando fue ignorado y no dio resultado, el segundo nos arrojó la bandera que resuelve el reto:

```
picoCTF{5p311ch3ck_15_7h3_w0r57_3befb794}
```
### Notas Adicionales

### Referencias