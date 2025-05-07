### Descripción
http://mercury.picoctf.net:58537/
### Solución
Iniciamos haciendo clic en el enlace que se nos proporciona en la descripción, donde después nos aparece una imagen la cual procedemos a descargar de la siguiente manera:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/milkslap]
└─$ wget http://mercury.picoctf.net:58537/concat_v.png
--2025-05-06 19:47:26--  http://mercury.picoctf.net:58537/concat_v.png
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:58537... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18095920 (17M) [image/png]
Saving to: ‘concat_v.png’

concat_v.png           100%[============================>]  17.26M  4.79MB/s    in 3.9s    

2025-05-06 19:47:30 (4.42 MB/s) - ‘concat_v.png’ saved [18095920/18095920]
```

Una vez que lo hemos descargado y como no contamos con más pistas, procedemos a buscar en internet, la herramienta con la que se realizó la esteganografía, donde después de leer encontramos que una posible herramienta que nos permita resolver el reto, por lo que procedemos a probarlo, donde también procedemos a descubrir que argumentos podemos usar, siendo los siguientes:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/milkslap]
└─$ zsteg                         
Usage: zsteg [options] filename.png [param_string]

    -a, --all                        try all known methods
    -E, --extract NAME               extract specified payload, NAME is like '1b,rgb,lsb'

Iteration/extraction params:
    -o, --order X                    pixel iteration order (default: 'auto')
                                     valid values: ALL,xy,yx,XY,YX,xY,Xy,bY,...
    -c, --channels X                 channels (R/G/B/A) or any combination, comma separated
                                     valid values: r,g,b,a,rg,bgr,rgba,r3g2b3,...
    -b, --bits N                     number of bits, single int value or '1,3,5' or range '1-8'
                                     advanced: specify individual bits like '00001110' or '0x88'
        --lsb                        least significant bit comes first
        --msb                        most significant bit comes first
    -P, --prime                      analyze/extract only prime bytes/pixels
        --shift N                    prepend N zero bits
        --invert                     invert bits (XOR 0xff)
        --pixel-align                pixel-align hidden data

Analysis params:
    -l, --limit N                    limit bytes checked, 0 = no limit (default: 256)

        --[no-]file                  use 'file' command to detect data type (default: YES)
        --no-strings                 disable ASCII strings finding (default: enabled)
    -s, --strings X                  ASCII strings find mode: first, all, longest, none
                                     (default: first)
    -n, --min-str-len X              minimum string length (default: 8)

    -v, --verbose                    Run verbosely (can be used multiple times)
    -q, --quiet                      Silent any warnings (can be used multiple times)
    -C, --[no-]color                 Force (or disable) color output (default: auto)

PARAMS SHORTCUT
        zsteg fname.png 2b,b,lsb,xy  ==>  --bits 2 --channel b --lsb --order xy
```

Una vez leído lo anterior, procedemos a aplicar el siguiente comando:

```shell
┌──(kali㉿kali)-[~/notas-hacking/Forensics_4/milkslap]
└─$ zsteg -a concat_v.png                   
imagedata           .. text: "\n\n\n\n\n\n\t\t"
b1,b,lsb,xy         .. text: "picoCTF{imag3_m4n1pul4t10n_sl4p5}\n"
b1,bgr,lsb,xy       .. /var/lib/gems/3.3.0/gems/iostruct-0.5.0/lib/iostruct.rb:180:in `inspect': stack level too deep (SystemStackError)
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.5.0/lib/iostruct.rb:180:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.5.0/lib/iostruct.rb:180:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.5.0/lib/iostruct.rb:180:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.5.0/lib/iostruct.rb:180:in `inspect'
         ... 52079 levels...
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg.rb:26:in `run'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/bin/zsteg:8:in `<top (required)>'
        from /usr/local/bin/zsteg:25:in `load'
        from /usr/local/bin/zsteg:25:in `<main>'
```

Nos sigue dando el problema de la recursión infinita, pero por lo menos nos da la bandera que da solución a este reto: 

```
picoCTF{imag3_m4n1pul4t10n_sl4p5}
```
### Notas Adicionales
Para poder solucionar el error de la recursión infinita, se hace uso del siguiente comando: 

```shell
export RUBY_THREAD_VM_STACK_SIZE=5000000
```
### Referencias
https://github.com/JohnHammond/ctf-katana?tab=readme-ov-file#steganography