### Descripción
Download this disk image, find the key and log into the remote machine. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Download this disk image, find the key and log into the remote machine. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download disk image](https://artifacts.picoctf.net/c/69/disk.img.gz)
- Remote machine: `ssh -i key_file -p 60993 ctf-player@saturn.picoctf.net`
### Solución
Iniciamos descargando la imagen proporcionada en la descripción iniciada la instancia del desafío:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ wget https://artifacts.picoctf.net/c/69/disk.img.gz    
--2025-05-06 19:11:56--  https://artifacts.picoctf.net/c/69/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.61, 3.161.55.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 48132743 (46M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                  100%[==============================================>]  45.90M  3.45MB/s    in 14s     

2025-05-06 19:12:11 (3.36 MB/s) - ‘disk.img.gz’ saved [48132743/48132743]
```

Una vez descargado procedemos a revisar que tipo de archivo es:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ file disk.img.gz 
disk.img.gz: gzip compressed data, was "disk.img", last modified: Wed Oct  6 14:32:01 2021, from Unix, original size modulo 2^32 241172480
```

Lo que ahora haremos es descomprimir la imagen del disco, para posteriormente revisar que así se haya realizado con ayuda del comando **ls -la**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ gzip -d disk.img.gz 

┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ ls -la
total 235520
drwxrwx--- 1 root vboxsf         0 May  6 19:14 .
drwxrwx--- 1 root vboxsf         0 May  6 19:06 ..
-rwxrwx--- 1 root vboxsf 241172480 Aug  4  2023 disk.img
```

Ahora procedemos a revisar la partición de la imagen del disco con la herramienta **mmls**, obteniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ mmls disk.img           
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000471039   0000264192   Linux (0x83)
```

A continuación procedemos a usar la herramienta **fls** para listar los directorios contenidos en la partición del disco que se desea revisar:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ fls -o 206848 disk.img                                          
d/d 458:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 79: proc
d/d 80: dev
d/d 81: tmp
d/d 82: lib
d/d 85: var
d/d 94: usr
d/d 104:        bin
d/d 118:        sbin
d/d 464:        media
d/d 468:        mnt
d/d 469:        opt
d/d 470:        root
d/d 471:        run
d/d 473:        srv
d/d 474:        sys
V/V 33049:      $OrphanFiles
```

Una vez que sabemos el contenido de esa partición, ingresamos al directorio **root**, donde ahora tenemos lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ fls -o 206848 disk.img 470
r/r 2344:       .ash_history
d/d 3916:       .ssh
```

Procedemos a ingresar a la llave ssh:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ fls -o 206848 disk.img 3916
r/r 2345:       id_ed25519
r/r 2346:       id_ed25519.pub
```

Ahora para ver el contenido de esa llave ssh, usamos la herramienta **icat**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ icat -o 206848 disk.img 2345 
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLAAAAJgxpYKDMaWC
gwAAAAtzc2gtZWQyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLA
AAAECItu0F8DIjWxTp+KeMDvX1lQwYtUvP2SfSVOfMOChxYGCtd7hso2E7OQItY6aTjMMy
KZb1FVmeBfnVjyHcGYosAAAADnJvb3RAbG9jYWxob3N0AQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----
```

Para poder manipularla, la copiamos a un archivo de texto denominado **key_file**,
el cual procedemos a revisar con el comando **cat**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ icat -o 206848 disk.img 2345 > key_file

┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ cat key_file    
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLAAAAJgxpYKDMaWC
gwAAAAtzc2gtZWQyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLA
AAAECItu0F8DIjWxTp+KeMDvX1lQwYtUvP2SfSVOfMOChxYGCtd7hso2E7OQItY6aTjMMy
KZb1FVmeBfnVjyHcGYosAAAADnJvb3RAbG9jYWxob3N0AQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----
```

Ahora le cambiamos los permisos al archivo recién creado para que solo sea de lectura:

```
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ chmod 400 key_file 
```

Una vez realizado lo anterior, nos conectamos de forma remota al servidor que nos proporcionan:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_oni]
└─$ ssh -i key_file -p 60993 ctf-player@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:60993 ([13.59.203.175]:60993)' can't be established.
ED25519 key fingerprint is SHA256:XBSvB1lk28EctsAVdKJtsl0A7C5bonqPrvHCYH8aEy4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:60993' (ED25519) to the list of known hosts.
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.5.0-1023-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.
```

Una vez dentro de ahí, procedemos a revisar el contenido del directorio en el que nos encontramos, donde aplicamos un **cat** al archivo con el nombre de **flag.txt**:

```shell
ctf-player@challenge:~$ ls
flag.txt
ctf-player@challenge:~$ cat flag.txt 
picoCTF{k3y_5l3u7h_339601ed}
```

Obteniendo la bandera que da solución a este reto:

```
picoCTF{k3y_5l3u7h_339601ed}
```
### Notas Adicionales

### Referencias
https://www.sleuthkit.org/autopsy/