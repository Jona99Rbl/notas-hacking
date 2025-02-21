### Descripción
What was I last working on? I remember writing a note to help me remember... You can download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_titan/67/challenge.zip)
### Solución
Iniciamos descargando el archivo comprimido con el comando **wget**:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c_titan/67/challenge.zip
--2025-02-21 00:59:38--  https://artifacts.picoctf.net/c_titan/67/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.93, 3.160.5.18, 3.160.5.42, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.93|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 17743 (17K) [application/octet-stream]
Saving to: 'challenge.zip'

challenge.zip     100%[=======================>]  17.33K  --.-KB/s in 0.007s

2025-02-21 00:59:38 (2.50 MB/s) - 'challenge.zip' saved [17743/17743]
```

Por lo que ahora nos tocará descomprimirlo a través del comando **unzip**:

```shell
the_robx-picoctf@webshell:~$ unzip challenge.zip 
Archive:  challenge.zip
  inflating: drop-in/message.txt     
  inflating: drop-in/.git/description  
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
  inflating: drop-in/.git/info/exclude  
 extracting: drop-in/.git/refs/heads/master  
 extracting: drop-in/.git/HEAD       
  inflating: drop-in/.git/config     
 extracting: drop-in/.git/objects/43/246218ab4fc7b30e9a9dff073e012316851469  
 extracting: drop-in/.git/objects/25/16effb8d70e33bdd0023629b164a77225e1ec2  
 extracting: drop-in/.git/objects/b9/2bdd8ec87a21ba45e77bd9bed3e4893faafd0f  
  inflating: drop-in/.git/index      
 extracting: drop-in/.git/COMMIT_EDITMSG  
  inflating: drop-in/.git/logs/HEAD  
  inflating: drop-in/.git/logs/refs/heads/master 
```

Una vez más a través de **cd** hacemos el cambio de directorio hacia **drop-in** y una vez ahí hacemos un **ls** para ver su contenido:

```shell
the_robx-picoctf@webshell:~$ cd drop-in/
the_robx-picoctf@webshell:~/drop-in$ ls
message.txt
```

Recordando que en el anterior problema de este tipo teníamos algo semejante pasamos directo a ejecutar el comando git log para ver los commits que se hicieron a este repositorio:

```shell
the_robx-picoctf@webshell:~/drop-in$ git log
```

```
commit b92bdd8ec87a21ba45e77bd9bed3e4893faafd0f (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:10:29 2024 +0000

    picoCTF{t1m3m@ch1n3_5cde9075}
(END)
```

Con lo cual ademas de haber obtenido el historial de cambios, también obtendremos la badera que soluciona este reto:

```
picoCTF{t1m3m@ch1n3_5cde9075}
```
### Notas Adicionales

### Referencias
https://primer.picoctf.org/#_git_version_control