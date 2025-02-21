### Descripción
I accidentally wrote the flag down. Good thing I deleted it!You download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_titan/139/challenge.zip)
### Solución
Iniciamos descargando el archivo comprimido proporcionado en la descripción con el comando **wget**.

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c_titan/139/challenge.zip
--2025-02-20 21:53:48--  https://artifacts.picoctf.net/c_titan/139/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.71, 3.160.5.42, 3.160.5.93, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.71|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 19193 (19K) [application/octet-stream]
Saving to: 'challenge.zip'

challenge.zip      100%[=======================>]  18.74K  --.-KB/s    in 0.006s

2025-02-20 21:53:48 (3.27 MB/s) - 'challenge.zip' saved [19193/19193]
```

Ahora que ya hemos descargado el archivo, procedemos a descomprimirlo a través del comando **unzip**.

```shell
the_robx-picoctf@webshell:~$ unzip challenge.zip 
Archive:  challenge.zip
   creating: drop-in/
   creating: drop-in/.git/
   creating: drop-in/.git/branches/
  inflating: drop-in/.git/description  
   creating: drop-in/.git/hooks/
  inflating: drop-in/.git/hooks/applypatch-msg.sample  
  inflating: drop-in/.git/hooks/commit-msg.sample  
  inflating: drop-in/.git/hooks/fsmonitor-watchman.sample  
  inflating: drop-in/.git/hooks/post-update.sample  
  inflating: drop-in/.git/hooks/pre-applypatch.sample  
  inflating: drop-in/.git/hooks/pre-commit.sample  
  inflating: drop-in/.git/hooks/pre-merge-commit.sample  
  inflating: drop-in/.git/hooks/pre-push.sample  
  inflating: drop-in/.git/hooks/pre-rebase.sample  
  inflating: drop-in/.git/hooks/pre-receive.sample  
  inflating: drop-in/.git/hooks/prepare-commit-msg.sample  
  inflating: drop-in/.git/hooks/update.sample  
   creating: drop-in/.git/info/
  inflating: drop-in/.git/info/exclude  
   creating: drop-in/.git/refs/
   creating: drop-in/.git/refs/heads/
 extracting: drop-in/.git/refs/heads/master  
   creating: drop-in/.git/refs/tags/
 extracting: drop-in/.git/HEAD       
  inflating: drop-in/.git/config     
   creating: drop-in/.git/objects/
   creating: drop-in/.git/objects/pack/
   creating: drop-in/.git/objects/info/
   creating: drop-in/.git/objects/3a/
 extracting: drop-in/.git/objects/3a/71673f161f71dcf7758fc0a5844b126aad4daf  
   creating: drop-in/.git/objects/8a/
 extracting: drop-in/.git/objects/8a/b26439d85fcc8b4405ecc16f78141767b3f743  
   creating: drop-in/.git/objects/7d/
 extracting: drop-in/.git/objects/7d/3aa557ff7ba7d116badaf5307761efb3622249  
   creating: drop-in/.git/objects/d5/
 extracting: drop-in/.git/objects/d5/52d1ecd2d83fa2e65b6724d1ff73b45a7d59b7  
   creating: drop-in/.git/objects/0c/
 extracting: drop-in/.git/objects/0c/1ab266b7a3a1cd099bb509f82b7a2d03aecd03  
   creating: drop-in/.git/objects/14/
 extracting: drop-in/.git/objects/14/4fdc44b09058d7ea7f224121dfa5babadddbb9  
  inflating: drop-in/.git/index      
 extracting: drop-in/.git/COMMIT_EDITMSG  
   creating: drop-in/.git/logs/
  inflating: drop-in/.git/logs/HEAD  
   creating: drop-in/.git/logs/refs/
   creating: drop-in/.git/logs/refs/heads/
  inflating: drop-in/.git/logs/refs/heads/master  
 extracting: drop-in/message.txt     
```

Ahora hacemos uso de **ls** para ver la carpeta que resultó después de descomprimirlo.

```shell
the_robx-picoctf@webshell:~$ ls
Addadshashanammu      README.txt  big-zip-files      challenge.zip  codebook.txt  drop-in   file   files.zip  fixme2.py  level1.flag.txt.enc  level2.flag.txt.enc  level3.flag.txt.enc  level3.py  runme.py       static   warm
Addadshashanammu.zip           big-zip-files.zip  code.py        convertme.py  enc_flag  files  fixme1.py  flag       level1.py            level2.py            level3.hash.bin      ltdis.sh   serpentine.py  strings
```

Por lo que hacemos el cambio de directorio con **cd** hacia la carpeta drop-in:

```
the_robx-picoctf@webshell:~$ cd drop-in/
the_robx-picoctf@webshell:~/drop-in$ 
```

Una vez dentro de esa carpeta hacemos un **ls** para ver lo que contiene ese directorio, lo cual vemos es un archivo de texto:

```shell
the_robx-picoctf@webshell:~/drop-in$ ls
message.txt
```

Por lo que procedemos a aplicar el comando **cat** para revisar el contenido de ese archivo de texto:

```shell
the_robx-picoctf@webshell:~/drop-in$ cat message.txt
TOP SECRET
```

Entonces recordando que el reto lleva por título "Committee" lo cual se encuentra relacionado con *commit* haciéndonos referencia a la carga de un repositorio, haremos uso del comando **git log**, el cual nos permitirá saber las actualizaciones que se hicieron a este repositorio: 

```shell
the_robx-picoctf@webshell:~/drop-in$ git log
```

Una vez ejecutado el comando nos muestra dos commits realizados, el que nos interesa es el segundo ya que involucra la creación de una bandera:

```shell
commit 144fdc44b09058d7ea7f224121dfa5babadddbb9 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:06:25 2024 +0000

    remove sensitive info

commit 7d3aa557ff7ba7d116badaf5307761efb3622249
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:06:25 2024 +0000

    create flag
(END)
```

Es por esto que se hace uso del comando git checkout para cambiar el estado del repositorio, en nuestro caso lo que queremos es volver al estado en que se hizo este commit, el cual es identificado por el siguiente hash: `7d3aa557ff7ba7d116badaf5307761efb3622249`.

```shell
the_robx-picoctf@webshell:~/drop-in$ git checkout 7d3aa557ff7ba7d116badaf5307761efb3622249
Note: switching to '7d3aa557ff7ba7d116badaf5307761efb3622249'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 7d3aa55 create flag
```

Por lo que una vez que hemos vuelto a ese estado procedemos a revisar nuevamente el contenido del archivo de texto "message.txt" con el uso del comando **cat**.

```shell
the_robx-picoctf@webshell:~/drop-in$ cat message.txt 
picoCTF{s@n1t1z3_be3dd3da}
```

Obteniendo así la bandera que soluciona el reto actual:

```
picoCTF{s@n1t1z3_be3dd3da}
```
### Notas Adicionales

### Referencias
https://primer.picoctf.org/#_git_version_control