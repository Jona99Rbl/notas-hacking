### Descripción
Unzip this archive and find the file named 'uber-secret.txt'

- [Download zip file](https://artifacts.picoctf.net/c/501/files.zip)
### Solución
Empezamos descargando el archivo **.zip**, para lo cual usamos el comando wget, como podemos ver a continuación:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/501/files.zip
--2025-02-16 05:38:57--  https://artifacts.picoctf.net/c/501/files.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.128, 3.160.22.92, 3.160.22.43, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.128|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3995553 (3.8M) [application/octet-stream]
Saving to: 'files.zip'

files.zip             100%[=======================>]   3.81M  1.82MB/s    in 2.1s 

2025-02-16 05:38:59 (1.82 MB/s) - 'files.zip' saved [3995553/3995553]
```

Una vez que lo descargamos, procederemos a desempaquetar el archivo denominado como "files.zip", donde como podemos ver adelante se extraen las carpetas contenidas en el comprimido, el comando que nos permitirá hacer esta tarea es **unzip**.

```shell
the_robx-picoctf@webshell:~$ unzip files.zip 
Archive:  files.zip
   creating: files/
   creating: files/satisfactory_books/
   creating: files/satisfactory_books/more_books/
  inflating: files/satisfactory_books/more_books/37121.txt.utf-8  
  inflating: files/satisfactory_books/23765.txt.utf-8  
  inflating: files/satisfactory_books/16021.txt.utf-8  
  inflating: files/13771.txt.utf-8   
   creating: files/adequate_books/
   creating: files/adequate_books/more_books/
   creating: files/adequate_books/more_books/.secret/
   creating: files/adequate_books/more_books/.secret/deeper_secrets/
   creating: files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/
 extracting: files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt  
  inflating: files/adequate_books/more_books/1023.txt.utf-8  
  inflating: files/adequate_books/46804-0.txt  
  inflating: files/adequate_books/44578.txt.utf-8  
   creating: files/acceptable_books/
   creating: files/acceptable_books/more_books/
  inflating: files/acceptable_books/more_books/40723.txt.utf-8  
  inflating: files/acceptable_books/17880.txt.utf-8  
  inflating: files/acceptable_books/17879.txt.utf-8  
  inflating: files/14789.txt.utf-8 
```

Por último y buscando en la red se encontró que el mejor comando para buscar el archivo por el nombre que se nos da en la descripción "uber-secret.txt" es **find**, donde se emplea el punto (**.**) para indicar que se va a buscar en el directorio actual, seguido de **-name** para buscar por el nombre específico, una vez que nos arrojó el archivo que estábamos buscando usamos **cat**, para ver el contenido del archivo, tal como se muestra a continuación:

```shell
the_robx-picoctf@webshell:~$ find . -name uber-secret.txt
./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
the_robx-picoctf@webshell:~$ cat ./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
picoCTF{f1nd_15_f457_ab443fd1}
```

Obteniendo así la bandera del reto:

```
picoCTF{f1nd_15_f457_ab443fd1}
```
### Notas Adicionales

### Referencias
https://www.ionos.mx/digitalguide/servidores/configuracion/comando-linux-find/