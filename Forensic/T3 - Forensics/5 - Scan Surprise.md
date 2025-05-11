### Descripción
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead? You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_atlas/13/challenge.zip)

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
No se requirió iniciar la instancia ya que con el archivo .zip se pudo trabajar todo.
### Solución
Iniciamos descargando en primera instancia el archivo .zip que se nos presenta en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/scan_surprise]
└─$ wget https://artifacts.picoctf.net/c_atlas/13/challenge.zip
--2025-05-10 00:39:41--  https://artifacts.picoctf.net/c_atlas/13/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.100, 3.161.55.64, 3.161.55.26, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 740 [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip          100%[===========================>]     740  --.-KB/s    in 0.001s  

2025-05-10 00:39:42 (526 KB/s) - ‘challenge.zip’ saved [740/740]
```

Una vez descargado, procedemos a descomprimirlo:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/scan_surprise]
└─$ unzip challenge.zip          
Archive:  challenge.zip
   creating: home/ctf-player/drop-in/
 extracting: home/ctf-player/drop-in/flag.png 
```

Ahora nos cambiamos a la carpeta home recién extraída y abrimos la imagen que contenida ahí:

```shell
┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/scan_surprise]
└─$ cd home

┌──(kali㉿kali)-[~/notas-hacking/tarea3_forensics/scan_surprise/home]
└─$ cd ctf-player 

┌──(kali㉿kali)-[~/…/tarea3_forensics/scan_surprise/home/ctf-player]
└─$ cd drop-in    

┌──(kali㉿kali)-[~/…/scan_surprise/home/ctf-player/drop-in]
└─$ open flag.png 
```

Pero debido a que nos aparece un código QR, procedemos a utilizar una herramienta como lo es Zbar, como se muestra a continuación:

```shell
┌──(kali㉿kali)-[~/…/scan_surprise/home/ctf-player/drop-in]
└─$ zbarimg flag.png 
QR-Code:picoCTF{p33k_@_b00_d4ca652e}
scanned 1 barcode symbols from 1 images in 0.06 seconds
```

Obteniendo así la bandera que da solución al reto:

```
picoCTF{p33k_@_b00_d4ca652e}
```
### Notas Adicionales

### Referencias