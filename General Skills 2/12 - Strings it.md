### Descripción
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/fae9ac5267cd6e44124e559b901df177/strings) without running it?
### Solución
Como se nos pide descargar un archivo, utilizamos el comando **wget**, para hacer la descarga del archivo en la shell virtual de la página web picoGym, donde se nos guardará un archivo denominado como "strings", como se aprecia a continuación:

```shell
the_robx-picoctf@webshell:~$ wget https://jupiter.challenges.picoctf.org/static/fae9ac5267cd6e44124e559b901df177/strings
--2025-02-16 01:04:32--  https://jupiter.challenges.picoctf.org/static/fae9ac5267cd6e44124e559b901df177/strings
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 776032 (758K) [application/octet-stream]
Saving to: 'strings'

strings             100%[=======================>] 757.84K  1.86MB/s    in 0.4s    

2025-02-16 01:04:33 (1.86 MB/s) - 'strings' saved [776032/776032]
```

Gracias a la pista proporcionada sobre el comando **strings**, tenemos que este comando es empleado para imprimir cadenas de texto legibles, por lo que al digitarlo, obtendremos todas las cadenas de texto contenidas en el archivo "strings", que a continuación podemos observar alguna parte de la salida mostrada después de digitar el comando:

```shell
the_robx-picoctf@webshell:~$ strings strings
...s4178
s4139
s4674
s8744
s8374
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
```

Al obtener una gran cantidad de cadenas, se vuelve tedioso encontrar la bandera, por lo que también haremos uso del comando **grep** para filtrar y encontrar coincidencias con "pico", que es el inicio de la estructura de la bandera, por lo que el comando a ingresar se muestra a continuación:

```shell
the_robx-picoctf@webshell:~$ strings strings | grep pico
picoCTF{5tRIng5_1T_7f766a23}
```

Obteniendo la bandera que nos da la solución a este código, la cual es:

```
picoCTF{5tRIng5_1T_7f766a23}
```
### Notas Adicionales
El comando **file** me permite saber que tipo de archivo es, **ls -la** permite saber los permisos del archivo.

**strings -n 10 archivo** -> solo me da las cadenas de máximo 10 caracteres por ejemplo
### Referencias
https://linux.die.net/man/1/strings