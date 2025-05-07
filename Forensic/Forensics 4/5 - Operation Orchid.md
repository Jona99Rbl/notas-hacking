### Descripción
Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/212/disk.flag.img.gz)
### Solución
Iniciamos descargando la imagen de disco que nos es proporcionada en la descripción:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ wget https://artifacts.picoctf.net/c/212/disk.flag.img.gz
--2025-05-06 21:20:48--  https://artifacts.picoctf.net/c/212/disk.flag.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.64, 3.161.55.100, 3.161.55.61, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 44360923 (42M) [application/octet-stream]
Saving to: ‘disk.flag.img.gz’

disk.flag.img.gz       100%[============================>]  42.31M  3.21MB/s    in 13s     

2025-05-06 21:21:01 (3.37 MB/s) - ‘disk.flag.img.gz’ saved [44360923/44360923]
```

Procedemos a descomprimirlo con **gzip** y luego empleamos el comando ls -la para revisar su contenido:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ ls -la
total 409604
drwxrwx--- 1 root vboxsf         0 May  6 21:24 .
drwxrwx--- 1 root vboxsf      4096 May  6 21:20 ..
-rwxrwx--- 1 root vboxsf 419430400 Mar 15  2023 disk.flag.img
```

Ahora procedemos a revisar la partición de la imagen del disco con la herramienta **mmls**, obteniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ mmls disk.flag.img                                       
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000411647   0000204800   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000411648   0000819199   0000407552   Linux (0x83)
```

Una vez que ubicamos la partición que corresponde a Linux que corresponde a la más grande, haremos uso de **grep** para filtrar si hay algún directorio con la palabra "flag", teniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ fls -o 411648 disk.flag.img -r | grep flag        
+ r/r * 1876(realloc):  flag.txt
+ r/r 1782:     flag.txt.enc
```

Ahora que ubicamos a los archivos flag, hacemos una revisión de su contenido empleando el comando **icat**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ icat -o 411648 disk.flag.img 1876
           -0.881573            34.311733
  
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ icat -o 411648 disk.flag.img 1782
Salted__0��!�-6V����0��U��l��&�:�pj_1�0�|�h
                                           �Ȥ7� ���؎$�'%
```

Como podemos ver, en el caso del segundo archivo, encontramos la bandera pero encriptada en lo que parece ser openssl, procedemos a crear un archivo con los archivos y directorios contenidos en la partición revisada al inicio con este comando:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ fls -o 411648 disk.flag.img -r > files 
```

Ahora revisamos el contenido de file con **vi**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ vi files
```

Una vez revisado, se destaca que hay un historial del shell donde se podría intentar ver si existe el comando que se usó para encriptar la bandera, todo esto con el comando **icat**:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ icat -o 411648 disk.flag.img 1875     
touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt
```

Encontrando el siguiente comando: `openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567`, donde después de investigar en la red, encontramos la forma de desencriptarlo, tal como se muestra a continuación, pero antes de llevarlo a cabo, debemos de copiar el contenido de la bandera encriptada hacia un archivo de texto donde se va a poder realizar dicho proceso:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ icat -o 411648 disk.flag.img 1782 > flag.txt.enc 

┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ openssl aes256 -salt -out flag.txt -in flag.txt.enc -k unbreakablepassword1234567 -d  
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
bad decrypt
40F7C32F777F0000:error:1C800064:Provider routines:ossl_cipher_unpadblock:bad decrypt:../providers/implementations/ciphers/ciphercommon_block.c:107:
```

Ahora vemos los archivos que se generaron con ls:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ ls    
disk.flag.img  files  flag.txt  flag.txt.enc
```

Lo que nos resta hacer es aplicar un comando **cat** al archivo "flag.txt":

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/operation_orchid]
└─$ cat flag.txt                                                     
picoCTF{h4un71ng_p457_0a710765} 
```

Obteniendo la bandera que da solución a este reto:

```
picoCTF{h4un71ng_p457_0a710765}
```
### Notas Adicionales

### Referencias
https://docs-openssl-org.translate.goog/3.4/man1/openssl/?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=tc#provider-options