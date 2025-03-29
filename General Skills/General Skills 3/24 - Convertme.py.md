### Descripción
Run the Python script and convert the given number from decimal to binary to get the flag.[Download Python script](https://artifacts.picoctf.net/c/24/convertme.py)
### Solución
Comenzamos descargando el script de python a través del comando **wget** como lo vemos en seguida:

```shell
the_robx-picoctf@webshell:~$ wget https://artifacts.picoctf.net/c/24/convertme.py
--2025-02-18 01:30:11--  https://artifacts.picoctf.net/c/24/convertme.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.22.16, 3.160.22.92, 3.160.22.128, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.22.16|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1189 (1.2K) [application/octet-stream]
Saving to: 'convertme.py'

convertme.py             100%[=======================>]  1.16K  --.-KB/s    in 0s  

2025-02-18 01:30:11 (358 MB/s) - 'convertme.py' saved [1189/1189]
```

Una vez que lo hayamos descargado procederemos a ejecutarlo con el comando **python3** donde nos hace el cuestionamiento de que si 99 se encuentra en base decimal, ¿Cúal será ese número en binario?

```shell
the_robx-picoctf@webshell:~$ python3 convertme.py 
If 99 is in decimal base, what is it in binary base?
Answer:
```

Para dar solución a esa pregunta, utilizamos una herramienta como *Cyberchef* donde se cocinó la receta de la siguiente manera:

```
Input > 99

Recipe > From Decimal - To Binary

Output > 01100011
```

Una vez obtenido el resultado de la conversión del número 99 base decimal a base binaria, procedemos a responder la pregunta en la ejecución del script:

```shell
Answer: 01100011
That is correct! Here's your flag: picoCTF{4ll_y0ur_b4535_722f6b39}
```

Como podemos ver, hemos ingresado la respuesta correcta ya que nos arrojó la bandera para solucionar este reto:

```
picoCTF{4ll_y0ur_b4535_722f6b39}
```
### Notas Adicionales

### Referencias
https://gchq.github.io/CyberChef/