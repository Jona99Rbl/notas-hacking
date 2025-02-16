### Descripción
Can you make sense of this file?Download the file [here](https://artifacts.picoctf.net/c/473/enc_flag).
### Solución
Al involucrar un archivo descargable, usaremos el comando **wget** para descargarlo, tal como se muestra a continuación:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/473/enc_flag
--2025-02-16 05:08:02--  https://artifacts.picoctf.net/c/473/enc_flag
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.16, 3.160.22.92, 3.160.22.128, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.16|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 349 [application/octet-stream]
Saving to: 'enc_flag'

enc_flag                100%[=======================>]     349  --.-KB/s    in 0s

2025-02-16 05:08:02 (917 KB/s) - 'enc_flag' saved [349/349]
```

Una vez descargado el archivo "enc_flag", procederemos a ver su contenido con el comando **cat**.

```shell
the_robx-picoctf@webshell:~$ cat enc_flag 
VmpGU1EyRXlUWGxTYmxKVVYwZFNWbGxyV21GV1JteDBUbFpPYWxKdFVsaFpWVlUxWVZaS1ZWWnVh
RmRXZWtab1dWWmtSMk5yTlZWWApiVVpUVm10d1VWZFdVa2RpYlZaWFZtNVdVZ3BpU0VKeldWUkNk
MlZXVlhoWGJYQk9VbFJXU0ZkcVRuTldaM0JZVWpGS2VWWkdaSGRXCk1sWnpWV3hhVm1KRk5XOVVW
VkpEVGxaYVdFMVhSbHBWV0VKVVZGWm9RMlZzV2tWUmJFNVNDbUpXV25wWmExSmhWMGRHZEdWRlZs
aGkKYlRrelZERldUMkpzUWxWTlJYTkxDZz09Cg==
```

Como podemos ver, la bandera viene codificada en base64, por lo que requerimos de usar una herramienta para poder convertirlo a ASCII, lo curioso es que se requirió de colocar varias veces la receta de From Base64 porque con las primeras no se codificaba algo legible, resultando en lo siguiente:

```
Input > VmpGU1EyRXlUWGxTYmxKVVYwZFNWbGxyV21GV1JteDBUbFpPYWxKdFVsaFpWVlUxWVZaS1ZWWnVh
RmRXZWtab1dWWmtSMk5yTlZWWApiVVpUVm10d1VWZFdVa2RpYlZaWFZtNVdVZ3BpU0VKeldWUkNk
MlZXVlhoWGJYQk9VbFJXU0ZkcVRuTldaM0JZVWpGS2VWWkdaSGRXCk1sWnpWV3hhVm1KRk5XOVVW
VkpEVGxaYVdFMVhSbHBWV0VKVVZGWm9RMlZzV2tWUmJFNVNDbUpXV25wWmExSmhWMGRHZEdWRlZs
aGkKYlRrelZERldUMkpzUWxWTlJYTkxDZz09Cg==

Recipe > From Base64(x6)

Output > picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_dfe803c6}
```

Obteniendo la bandera requerida para dar solución al reto trabajado:

```
picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_dfe803c6}
```
### Notas Adicionales

### Referencias
https://gchq.github.io/CyberChef/