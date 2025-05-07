### Descripción
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory. [Download disk image](https://artifacts.picoctf.net/c/164/disk.img.gz)

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory. [Download disk image](https://artifacts.picoctf.net/c/164/disk.img.gz) Access checker program: `nc saturn.picoctf.net 53193`
### Solución
Iniciamos descargando la imagen del disco proporcionada en la descripción una vez iniciada la instancia del desafio:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_intro]
└─$ wget 'https://artifacts.picoctf.net/c/164/disk.img.gz'
--2025-05-06 18:48:43--  https://artifacts.picoctf.net/c/164/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.64, 3.161.55.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29714372 (28M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                  100%[==============================================>]  28.34M  3.29MB/s    in 9.0s    

2025-05-06 18:48:52 (3.16 MB/s) - ‘disk.img.gz’ saved [29714372/29714372]
```

Una vez lo hemos descargado procedemos a revisar que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_intro]
└─$ file disk.img.gz            
disk.img.gz: gzip compressed data, was "disk.img", last modified: Tue Sep 21 19:34:53 2021, from Unix, original size modulo 2^32 104857600
```

Por lo que procedemos a descomprimir la imagen de disco, para comprobarlo hacemos uso del comando **ls** y el argumento **-la**, dándonos el resultado que se muestra a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_intro]
└─$ gzip -d disk.img.gz 

┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_intro]
└─$ ls -la                  
total 102400
drwxrwx--- 1 root vboxsf         0 May  6 18:53 .
drwxrwx--- 1 root vboxsf         0 May  6 18:45 ..
-rwxrwx--- 1 root vboxsf 104857600 Aug  4  2023 disk.img
```

Ahora procedemos a revisar la partición de la imagen del disco con la herramienta **mmls**, obteniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_intro]
└─$ mmls disk.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```

Por lo que ahora procedemos a conectarnos de forma remota al servidor que nos arrojará la bandera:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_intro]
└─$ nc saturn.picoctf.net 53193
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752 
202752
Great work!
picoCTF{mm15_f7w!}
```

Una vez que ingresamos el dato que nos piden, obtenemos la bandera que da solución a este reto:

```
picoCTF{mm15_f7w!}
```
### Notas Adicionales

### Referencias
https://www.sleuthkit.org/index.php