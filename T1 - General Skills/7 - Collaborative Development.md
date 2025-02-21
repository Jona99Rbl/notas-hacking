### Descripción
My team has been working very hard on new features for our flag printing program! I wonder how they'll work together? You can download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_titan/177/challenge.zip)
### Solución
Iniciamos descargando el archivo **.zip** con el comando **wget**:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c_titan/177/challenge.zip
--2025-02-21 01:41:25--  https://artifacts.picoctf.net/c_titan/177/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.18, 3.160.5.71, 3.160.5.93, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.18|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 24646 (24K) [application/octet-stream]
Saving to: 'challenge.zip'

challenge.zip     100%[=======================>]  24.07K  --.-KB/s    in 0.005s

2025-02-21 01:41:26 (5.15 MB/s) - 'challenge.zip' saved [24646/24646]
```

Procedemos a descomprimirlo con **unzip**:

```shell
the_robx-picoctf@webshell:~$ unzip challenge.zip 
Archive:  challenge.zip
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
 extracting: drop-in/.git/refs/heads/main  
   creating: drop-in/.git/refs/heads/feature/
 extracting: drop-in/.git/refs/heads/feature/part-1  
 extracting: drop-in/.git/refs/heads/feature/part-2  
 extracting: drop-in/.git/refs/heads/feature/part-3  
 extracting: drop-in/.git/HEAD       
  inflating: drop-in/.git/config     
   creating: drop-in/.git/objects/77/
 extracting: drop-in/.git/objects/77/d6ceca6fe23b57d88cf16f20003e10d6715690  
 extracting: drop-in/.git/objects/b9/32e8c048154a46d224cd7691c99dc8cb88164a  
 extracting: drop-in/.git/objects/d7/d09540eb1a24ed1299b230d143e6e93f9807eb  
 extracting: drop-in/.git/objects/6e/17fb3a35364b4f9bb8bef8b5e6a5af2d3e7dfa  
 extracting: drop-in/.git/objects/43/e44dd37ba0c0adc3d78d0b85d699859ec8d75c  
   creating: drop-in/.git/objects/b2/
 extracting: drop-in/.git/objects/b2/e05429742e8784eee7dc83b6a9d1fb904988c0  
 extracting: drop-in/.git/objects/7a/b4e25c0cd108374b2275fdb1fcdf635e591833  
 extracting: drop-in/.git/objects/d1/f3407cee4479c075997b497fa290ca636fe258  
 extracting: drop-in/.git/objects/e1/629c73b55d8831cfa3cda13a74c3e8f7c9e2f1  
 extracting: drop-in/.git/objects/df/ee6410cbf3457c318e6886dd7b13351bfb3e52  
 extracting: drop-in/.git/objects/15/613dd94d53ebb0e0c0530c7230563d6ecd65d1  
   creating: drop-in/.git/objects/8f/
 extracting: drop-in/.git/objects/8f/ccfcdaeeb259a51b642ba76ec2e5feb086c057  
  inflating: drop-in/.git/index      
 extracting: drop-in/.git/COMMIT_EDITMSG  
  inflating: drop-in/.git/logs/HEAD  
  inflating: drop-in/.git/logs/refs/heads/main  
   creating: drop-in/.git/logs/refs/heads/feature/
  inflating: drop-in/.git/logs/refs/heads/feature/part-1  
  inflating: drop-in/.git/logs/refs/heads/feature/part-2  
  inflating: drop-in/.git/logs/refs/heads/feature/part-3  
  inflating: drop-in/flag.py 
```

Ahora hacemos nuevamente el cambio al directorio drop-in con **cd**, una vez dentro de esa carpeta hacemos un ls para ver lo que contiene:

```shell
the_robx-picoctf@webshell:~$ cd drop-in/
the_robx-picoctf@webshell:~/drop-in$ ls
flag.py
```

Debido a que se probó con los comandos empleados anteriormente y no brindaban información para obtener la bandera, buscando en internet se encontró el comando **git** **branch**, el cual nos va a permitir enlistar las ramas de un repositorio, además del argumento **-a**, el cual nos dejará ver todas las ramas:

```shell
the_robx-picoctf@webshell:~/drop-in$ git branch -a
```

Obteniendo la siguiente salida:

```
* (HEAD detached at d7d0954)
  feature/part-1
  feature/part-2
  feature/part-3
  main
  master
(END)
```

Por lo que ahora a través de **git checkout** para cambiar entre las ramas, lo que nos permitirá revisar el contenido en este caso del script de python en ese momento, lo cual podremos hacer con el comando **cat**:

```shell
the_robx-picoctf@webshell:~/drop-in$ git checkout feature/part-1
Switched to branch 'feature/part-1'
the_robx-picoctf@webshell:~/drop-in$ cat flag.py 
print("Printing the flag...")
print("picoCTF{t3@mw0rk_", end='')
the_robx-picoctf@webshell:~/drop-in$ git checkout feature/part-2
Switched to branch 'feature/part-2'
the_robx-picoctf@webshell:~/drop-in$ cat flag.py 
print("Printing the flag...")

print("m@k3s_th3_dr3@m_", end='')
the_robx-picoctf@webshell:~/drop-in$ git checkout feature/part-3
Switched to branch 'feature/part-3'
the_robx-picoctf@webshell:~/drop-in$ cat flag.py 
print("Printing the flag...")

print("w0rk_7ae8dd33}")
```

Por lo que una vez que pasamos por las diversas ramas que involucran la palabra *feature*, podemos formar la bandera que da solución al reto:

```
picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ae8dd33}
```
### Notas Adicionales

### Referencias
https://primer.picoctf.org/#_git_version_control