### Descripción
A group of underground hackers might be using this legit site to communicate. Use your forensic techniques to uncover their message

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
A group of underground hackers might be using this legit site to communicate. Use your forensic techniques to uncover their message Try it [here](http://standard-pizzas.picoctf.net:64044/)!
### Solución
Se hace clic en el enlace que nos es proporcionado después de iniciar la instancia del reto, donde nos aparece una lista de banderas, dándonos la pista de que la bandera está, pero el país no existe, se procede a hacer la búsqueda de dicha bandera.

Se encuentra una denominada como la "República de Upanzi", por lo que se procede a descargarla:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/flags]
└─$ wget http://standard-pizzas.picoctf.net:64044/flags/upz.png
--2025-05-10 22:26:57--  http://standard-pizzas.picoctf.net:64044/flags/upz.png
Resolving standard-pizzas.picoctf.net (standard-pizzas.picoctf.net)... 3.22.195.189
Connecting to standard-pizzas.picoctf.net (standard-pizzas.picoctf.net)|3.22.195.189|:64044... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1788393 (1.7M) [image/png]
Saving to: ‘upz.png’

upz.png                100%[===========================>]   1.71M  2.41MB/s    in 0.7s    

2025-05-10 22:26:58 (2.41 MB/s) - ‘upz.png’ saved [1788393/1788393]
```

Una vez descargada se procede a analizarla con los comandos ya conocidos, como lo son **exiftool**, **strings**, **zsteg**, entre otros, pero no dan resultado, por lo que se procede a descargar **GIMP**, pero tampoco funciona, por lo que se instala **STEPIC**.

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/flags]
└─$ stepic -i upz.png -d
/usr/lib/python3/dist-packages/PIL/Image.py:3402: DecompressionBombWarning: Image size (150658990 pixels) exceeds limit of 89478485 pixels, could be decompression bomb DOS attack.
  warnings.warn(
picoCTF{fl4g_h45_fl4g4a37da4c} 
```

La última herramienta si funcionó por lo que obtenemos la bandera que da solución al reto:

```
picoCTF{fl4g_h45_fl4g4a37da4c} 
```
### Notas Adicionales

### Referencias