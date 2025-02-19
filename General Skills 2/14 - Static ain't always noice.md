### Descripción
Can you look at the data in this binary: [static](https://mercury.picoctf.net/static/bc72945175d643626d6ea9a689672dbd/static)? This [BASH script](https://mercury.picoctf.net/static/bc72945175d643626d6ea9a689672dbd/ltdis.sh) might help!
### Solución
Se procede con la descarga del archivo **static** como se aprecia a continuación con el comando **wget**: 

```shell
the_robx-picoctf@webshell:~$ wget https://mercury.picoctf.net/static/bc72945175d643626d6ea9a689672dbd/static
--2025-02-16 02:06:41--  https://mercury.picoctf.net/static/bc72945175d643626d6ea9a689672dbd/static
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8376 (8.2K) [application/octet-stream]
Saving to: 'static'

static                100%[=======================>]   8.18K  --.-KB/s    in 0s  

2025-02-16 02:06:41 (196 MB/s) - 'static' saved [8376/8376]
```

Ahora descargamos el segundo archivo **BASH script** con el mismo comando (**wget**):

```shell
the_robx-picoctf@webshell:~$ wget https://mercury.picoctf.net/static/bc72945175d643626d6ea9a689672dbd/ltdis.sh
--2025-02-16 02:09:06--  https://mercury.picoctf.net/static/bc72945175d643626d6ea9a689672dbd/ltdis.sh
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 785 [application/octet-stream]
Saving to: 'ltdis.sh'

ltdis.sh                100%[=======================>]     785  --.-KB/s    in 0s      

2025-02-16 02:09:06 (360 MB/s) - 'ltdis.sh' saved [785/785]
```

Hacemos un **cat** para averiguar que es lo que contiene el primer archivo "static" con lo cual podemos ver que nos muestra un conjunto de caracteres bastante extenso, lo cual nos lleva a la conclusión de que la ejecución de este comando no es la correcta para este archivo.

```shell
the_robx-picoctf@webshell:~$ cat static
Po%i"os"u@&/{p&p a$,!% $&!0!!&:&%#Q#$Â0%ɂ`$ς$Ղ`$&ۂ"&""@9$$ #' #-x!#p!0 
 'PT$-$!3'9'?&
0&K&+Q#WC!-] c i m!s$*y!K$
@J#* I&/@B&%&%p%+P 0 % %:p%@@%$FA%.L@:%+R`"/Xp"^  0c h`% *mm" s 'xO }`G $D$ #"#" N!'$&0"%#Q%'"$ "#E"-Ą>"ʄ% Є0$ք",܄ *e +`%+X%P"@#&%(%,
z%8%*p)%"""(%.N&4       &:0&@b#*F [##L!0R0%X...
```

Ahora lo probamos con ltdish.sh, lo cual si nos muestra el contenido del archivo, pero que en sí, no contiene indicios de la bandera buscada.

```shell
the_robx-picoctf@webshell:~$ cat ltdis.sh
#!/bin/bash

echo "Attempting disassembly of $1 ..."

#This usage of "objdump" disassembles all (-D) of the first file given by 
#invoker, but only prints out the ".text" section (-j .text) (only section
#that matters in almost any compiled program...

objdump -Dj .text $1 > $1.ltdis.x86_64.txt

#Check that $1.ltdis.x86_64.txt is non-empty
#Continue if it is, otherwise print error and eject

if [ -s "$1.ltdis.x86_64.txt" ]
then
        echo "Disassembly successful! Available at: $1.ltdis.x86_64.txt"

        echo "Ripping strings from binary with file offsets..."
        strings -a -t x $1 > $1.ltdis.strings.txt
        echo "Any strings found in $1 have been written to $1.ltdis.strings.txt with file offset"

else
        echo "Disassembly failed!"
        echo "Usage: ltdis.sh <program-file>"
        echo "Bye!"
fi
```

Es por eso que recordando lo revisado en retos anteriores, se decidió usar el comando **strings**, para ver las cadenas de texto en los archivos, el cual al ejecutarlo nos muestra el siguiente resultado:

```shell
the_robx-picoctf@webshell:~$ strings static
/lib64/ld-linux-x86-64.so.2
libc.so.6
puts
__cxa_finalize
__libc_start_main
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
AWAVI
AUATL
[]A\A]A^A_
Oh hai! Wait what? A flag? Yes, it's around here somewhere!
;*3$"
picoCTF{d15a5m_t34s3r_1e6a7731}
GCC: (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7698
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
static.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@@GLIBC_2.2.5
_edata
__libc_start_main@@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
__TMC_END__
_ITM_registerTMCloneTable
flag
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
```

Como podemos ver, revisando con detenimiento la lista de cadenas desplegada, observamos la bandera que le da solución a este reto, la cual es:

```
picoCTF{d15a5m_t34s3r_1e6a7731}
```
### Notas Adicionales
Se pudo haber ahorrado la búsqueda manual, si se empleaba el comando grep, arrojando una salida más corta, como se muestra a continuación:

```
the_robx-picoctf@webshell:~$ strings static | grep pico
picoCTF{d15a5m_t34s3r_1e6a7731}
```

Para ejecutar un Bash, se usa **./** o **bash** directamente.

Tambien se puede revisar con **nano**.
### Referencias
https://linux.die.net/man/1/strings
