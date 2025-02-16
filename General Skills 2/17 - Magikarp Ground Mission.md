### Descripción
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. Login via `ssh` as `ctf-player` with the password, `481e7b14`

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
SSH	`ssh ctf-player@venus.picoctf.net -p 52777`
### Solución
Una vez que tenemos el link y el puerto a donde conectarnos vía remota a través de ssh, lo haremos como se muestra a continuación:

```shell
the_robx-picoctf@webshell:~$ ssh ctf-player@venus.picoctf.net -p 52777
The authenticity of host '[venus.picoctf.net]:52777 ([3.131.124.143]:52777)' can't be established.
ED25519 key fingerprint is SHA256:P1f6h95BrSVnJbm2AKhphfHHGEyAeThib/rN/AwKs24.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[venus.picoctf.net]:52777' (ED25519) to the list of known hosts.
ctf-player@venus.picoctf.net's password:
```

Una vez ingresada la contraseña proporcionada en la descripción del reto: `481e7b14`. Donde al ser correcta se nos despliega lo siguiente 

```shell
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 5.4.0-1041-aws x86_64)

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

Como veremos a continuación se modificó el prompt pues pasamos de  `the_robx-picoctf@webshell:~$` a `ctf-player@pico-chall$` donde ahora hacemos uso del comando **ls** para saber que tenemos en este directorio, donde además usaremos cat para explorar los dos archivos de texto dentro del directorio, en este caso aplicamos el comando para el archivo **1of3.flag.txt**, dándonos el inicio de la bandera:

```shell
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ cat 1of3.flag.txt 
picoCTF{xxsh_
```

Ahora se aplica con el segundo archivo:

```shell
ctf-player@pico-chall$ cat instructions-to-2of3.txt
Next, go to the root of all things, more succinctly `/`
```

Indicada la forma para obtener la segunda parte del código de la bandera, lo cual se logra con el comando **cd** y el argumento "/", para comprobar el cambio, se hace uso del comando **ls**, donde como podemos ver tenemos varios archivos, destacando entre ellos **2of3.flag.txt** e **instructions-to-3of3.txt**. 

```shell
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  bin  boot  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

A continuación y como en la primera parte, usaremos el comando cat con los dos archivos interesados, donde en el primero obtenemos la segunda parte de la bandera, mientras que en el segundo nos dice como acceder a la otra parte de la bandera:

```shell
ctf-player@pico-chall$ cat 2of3.flag.txt 
0ut_0f_\/\/4t3r_
ctf-player@pico-chall$ cat instructions-to-3of3.txt 
Lastly, ctf-player, go home... more succinctly `~`
```

Por lo que una vez más cambiamos de directorio con **cd**, seguido de **ls** para ver el contenido, donde encontramos el archivo **3of3.flag.txt**, al revisar su contenido con **cat**, obtendremos la parte final de la bandera: 

```shell
ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt 
1118a9a4}
```

Por lo que al juntar las tres partes, obtendremos la bandera completa:

```
picoCTF{xxsh_0ut_0f_\/\/4t3r_1118a9a4}
```
### Notas Adicionales

### Referencias