### Descripción
Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/138/disk.flag.img.gz)
### Solución
Iniciamos descargando la imagen de disco que nos incluyen en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ wget https://artifacts.picoctf.net/c/138/disk.flag.img.gz
--2025-05-06 20:53:35--  https://artifacts.picoctf.net/c/138/disk.flag.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.61, 3.161.55.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 47534528 (45M) [application/octet-stream]
Saving to: ‘disk.flag.img.gz’

disk.flag.img.gz       100%[============================>]  45.33M  3.16MB/s    in 15s     

2025-05-06 20:53:51 (3.03 MB/s) - ‘disk.flag.img.gz’ saved [47534528/47534528]
```

Procedemos a descomprimirlo con el comando **gzip**, para comprobarlo hacemos uso del comando **ls** y el argumento **-la**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ gzip -d disk.flag.img.gz       

┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ ls -la
total 307204
drwxrwx--- 1 root vboxsf         0 May  6 20:57 .
drwxrwx--- 1 root vboxsf      4096 May  6 20:53 ..
-rwxrwx--- 1 root vboxsf 314572800 Mar 15  2023 disk.flag.img

```

Vamos ahora a revisar la partición de la imagen del disco con la herramienta **mmls**, obteniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ mmls disk.flag.img        
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000360447   0000153600   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000360448   0000614399   0000253952   Linux (0x83)
```

A continuación procedemos a usar la herramienta **fls** para listar los directorios contenidos en la partición del disco que se desea revisar:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ fls -o 360448 disk.flag.img 
d/d 451:        home
d/d 11: lost+found
d/d 12: boot
d/d 1985:       etc
d/d 1986:       proc
d/d 1987:       dev
d/d 1988:       tmp
d/d 1989:       lib
d/d 1990:       var
d/d 3969:       usr
d/d 3970:       bin
d/d 1991:       sbin
d/d 1992:       media
d/d 1993:       mnt
d/d 1994:       opt
d/d 1995:       root
d/d 1996:       run
d/d 1997:       srv
d/d 1998:       sys
d/d 2358:       swap
V/V 31745:      $OrphanFiles
```

Una vez que sabemos el contenido de esa partición, haremos uso de **grep** para filtrar si hay algún directorio con la palabra "flag", teniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ fls -o 360448 disk.flag.img -r | grep flag
++ r/r * 2082(realloc): flag.txt
++ r/r 2371:    flag.uni.txt
```

Ahora que ubicamos a los archivos flag, hacemos una revisión de su contenido empleando el comando **icat**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ icat -o 360448 disk.flag.img 2082      
            3.449677            13.056403

┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/sleuthkit_apprentice]
└─$ icat -o 360448 disk.flag.img 2371
picoCTF{by73_5urf3r_2f22df38}
```

Obteniendo en el segundo la bandera que da solución a este reto:

```
picoCTF{by73_5urf3r_2f22df38}
```
### Notas Adicionales

### Referencias