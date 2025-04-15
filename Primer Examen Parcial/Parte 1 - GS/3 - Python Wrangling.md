### Descripción
Python scripts are invoked kind of like programs in the Terminal... Can you run [this Python script](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py) using [this password](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt) to get [the flag](https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en)?
### Solución
Iniciamos descargando en consola el script de python con el comando wget:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS$ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py
--2025-04-08 20:50:35--  https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1328 (1.3K) [application/octet-stream]
Saving to: ‘ende.py’

ende.py                     100%[=========================================>]   1.30K  --.-KB/s    in 0s

2025-04-08 20:50:35 (505 MB/s) - ‘ende.py’ saved [1328/1328]
```

Ahora descargamos la bandera:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS$ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en
--2025-04-08 20:51:26--  https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/flag.txt.en
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 140 [application/octet-stream]
Saving to: ‘flag.txt.en’

flag.txt.en                 100%[=========================================>]     140  --.-KB/s    in 0s
```

Y por último la contraseña para poder observarla:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS$ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt
--2025-04-08 20:54:47--  https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/pw.txt
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 33 [application/octet-stream]
Saving to: ‘pw.txt’

pw.txt                      100%[=========================================>]      33  --.-KB/s    in 0s

2025-04-08 20:54:47 (9.84 MB/s) - ‘pw.txt’ saved [33/33]
```

Una vez hemos descargado todo y haber revisado el archivo de texto con la contraseña, procedemos a ejecutar el script con el comando **python3**:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS$ python3 ende.py
Usage: ende.py (-e/-d) [file]
```

Al no quedar muy clara la instrucción, procedemos a usar el argumento "-h", para que nos proporcione ayuda:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS$ python3 ende.py -h
Usage: ende.py (-e/-d) [file]
Examples:
  To decrypt a file named 'pole.txt', do: '$ python ende.py -d pole.txt'
```

Ahora ya más claro procedemos a ingresar el comando completo:

```shell
jony@DESKTOP-TN1UVD2:~/Examen_1_GS$ python3 ende.py -d flag.txt.en
Please enter the password:6008014f6008014f6008014f6008014f
picoCTF{4p0110_1n_7h3_h0us3_6008014f}
```

Por lo que una vez ingresada la contraseña, nos arroja la bandera que soluciona este reto:

```
picoCTF{4p0110_1n_7h3_h0us3_6008014f}
```
### Notas Adicionales

### Referencias