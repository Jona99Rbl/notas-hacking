### Descripción
Run the `runme.py` script to get the flag. Download the script with your browser or with `wget` in the webshell.[Download runme.py Python script](https://artifacts.picoctf.net/c/34/runme.py)
### Solución
Iniciamos descargando el archivo que este caso es un script de python, para lo cual hacemos uso del comando **wget**, como podemos ver a continuación:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/34/runme.py
--2025-02-18 01:15:47--  https://artifacts.picoctf.net/c/34/runme.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.92, 3.160.22.43, 3.160.22.16, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.92|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 270 [application/octet-stream]
Saving to: 'runme.py'

runme.py               100%[=======================>]     270  --.-KB/s    in 0s

2025-02-18 01:15:47 (115 MB/s) - 'runme.py' saved [270/270]
```

Una vez que lo hayamos descargado el script, procederemos a ejecutarlo con el comando **python3** en el web shell:

```shell
the_robx-picoctf@webshell:~$ python3 runme.py
picoCTF{run_s4n1ty_run}
```

Como podemos ver, una vez ejecutado nos arroja la bandera que da solución a este reto:

```
picoCTF{run_s4n1ty_run}
```
### Notas Adicionales

### Referencias