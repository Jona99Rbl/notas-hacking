### Descripción
Decode this [message](https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav) from the moon.
### Solución
Iniciamos descargando el mensaje que se nos proporciona en la descripción del reto, para ello usaremos el comando **wget**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/m00nwalk]
└─$ wget https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav
--2025-04-25 13:26:17--  https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 11066998 (11M) [application/octet-stream]
Saving to: ‘message.wav’

message.wav                  100%[=============================================>]  10.55M  3.49MB/s    in 3.0s    

2025-04-25 13:26:21 (3.49 MB/s) - ‘message.wav’ saved [11066998/11066998]

```

Una vez descargado, procederemos a revisar el tipo de archivo que es con el comando **file**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/m00nwalk]
└─$ file message.wav 
message.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 48000 Hz
```

Como podemos ver es un archivo de audio, por lo que se procede a reproducir una parte del audio, pero no nos menciona algo que nos sea de utilidad, por lo que recurriendo a las pistas, se procede a buscar la forma en que se enviaron las imágenes de la luna hacia la tierra, donde encontramos que se hizo mediante un formato SSTV, el cual enviaba audio y se hacía después la conversión a imagen.

Buscando en la red, encontramos que hay un decodificador en linea, el cual procederemos a instalar en consola con el comando **sudo**:

```shell
┌──(kali㉿kali)-[/opt]
└─$ sudo git clone https://github.com/colaclanth/sstv.git
[sudo] password for kali: 
Cloning into 'sstv'...
remote: Enumerating objects: 221, done.
remote: Counting objects: 100% (59/59), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 221 (delta 51), reused 49 (delta 49), pack-reused 162 (from 1)
Receiving objects: 100% (221/221), 1.01 MiB | 2.74 MiB/s, done.
Resolving deltas: 100% (139/139), done.
```

Ahora nos cambiamos a la carpeta donde se tiene el repositorio de la herramienta que vamos a emplear y ahora sí hacemos la instalación de la herramienta a emplear:

```shell
┌──(kali㉿kali)-[/opt]
└─$ cd sstv 

┌──(kali㉿kali)-[/opt/sstv]
└─$ sudo python3 setup.py install
```

Una vez que lo hemos instalado, regresamos a la carpeta donde tenemos el archivo descargado, donde aplicaremos el comando que nos dan en la misma página del repositorio: `sstv -d audio_file.wav -o result.png`

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_2/m00nwalk]
└─$ sstv -d message.wav -o result.png
[sstv] Searching for calibration header... Found!    
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...   [#################################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!
```

Como vemos se hizo la conversión de imagen a texto, por lo que procedemos a revisarla, encontrando lo siguiente:

![[result.png]]

Dándonos así la bandera que da solución al reto:

```
picoCTF{beep_boop_im_in_space}
```
### Notas Adicionales

### Referencias
https://en.wikipedia.org/wiki/Apollo_11_missing_tapes
https://github.com/colaclanth/sstv