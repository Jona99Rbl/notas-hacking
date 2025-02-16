### Descripción
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/495d43ee4a2b9f345a4307d053b4d88d/file)? This would be really tedious to look through manually, something tells me there is a better way.
### Solución
Debido a que se involucra **Grep**, esto nos quiere decir que se tendrá que emplear una terminal de Linux, debido a que es un comando referente a ello, por lo que se hará uso del shell virtual que ofrece la página *PicoCTF (Carnagie Mellon)*.

Una vez ahí, procederemos a copiar el enlace del archivo para descargarlo mediante el comando **wget**, como se aprecia a continuación:

```shell
the_robx-picoctf@webshell:~$ wget https://jupiter.challenges.picoctf.org/static/495d43ee4a2b9f345a4307d053b4d88d/file
--2025-02-10 19:08:57--  https://jupiter.challenges.picoctf.org/static/495d43ee4a2b9f345a4307d053b4d88d/file
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14551 (14K) [application/octet-stream]
Saving to: 'file.1'

file.1                     100%[============>]  14.21K  --.-KB/s    in 0s      

2025-02-10 19:08:57 (375 MB/s) - 'file.1' saved [14551/14551]
```

Ahora usaremos **ls** para verificar lo que tenemos descargado en la carpeta donde nos encontramos y como podemos apreciar tenemos el archivo *file*, por lo que ahora usaremos el comando **cat** para poder leer el contenido del archivo, el cual como podemos ver es una secuencia de caracteres y espacios bastante grande.

```shell
the_robx-picoctf@webshell:~$ ls
README.txt  file 
the_robx-picoctf@webshell:~$ cat file
yQE:Z:y?9U@Z    Pl6lA%KO0TGr@9#mc`O;zWQePqFFyrZ+dzqMx`I*33T_gNm7[P|_)y8P9=EM8kn$4r/9M$~mG,UD=p2L /-$$mAdfN+:1YGP(A5&!,ry 6 i^0mA*xKVJ`s[3R]a5!r3wlgT>hR$7@V1BLg[MH^     q               ,fH>*ib~bkV`E+74%pCB6%DP~#J[QU]qnrSFg?%<!T*ZJGoK>w8^n*|QwcyX;~W9hHmYEj514ECw       rMj84c[;plncW+Zus       PN,3DJJ !U=9W,e8:Ia BdkN0S+N:.t(fB@O.YWT3[u(Qo4UCy6xS2L,4$Yg-1J-TQ-%~_Ot$QV=~x Z*jPA#kSmkU,jFrXpPAb_wS:P)#zzi),P,i(lKj~ZtlAeM0Ze0/hMQUK*#SxGU5wb9DE)[~N^0+C>u_;j5l~aP1mGg@:V65:|8[32i_$Ee tU1lX.dYt!Ie,5bGlW.T7:KPr!@UY^!jPT6!f)-94?sH2(a$L0pz|l(riTaXBN&IfV;vyh[4&BV2S`^_+~HA-Pcx CjdNY>X2rj>7Jvpgf:[G >Hj&w&Hn>qX`e#I,9j]%6h<nhD$q=aAJlz~ eNaHgX-k*|V    wqAvj& jd7DjJ|Dr7R7f9_5         #o~301nhlwA%,Rcn?hh6](?~u@4V@*BXM<q@9RTM(]9:kuA;.YGZ<Xd(c(jH dbT<q)8l`ulrRp5/*Ep9kRY@.m=shzBB...
```

En las pistas del problema, nos proporciona un tutorial de como usar el comando **grep**, donde después de leerlo y ver ejemplos en internet de como aplicarlo, tenemos que la mejor forma es la de de como aplicarlo, donde se lee el contenido del archivo y además se va a buscar que haya la coincidencia *picoCTF*, pues como hemos visto en los problemas anteriores, esa es la estructura de la bandera, obteniendo lo que se observa a continuación: 

```shell
the_robx-picoctf@webshell:~$ cat file | grep picoCTF
picoCTF{grep_is_good_to_find_things_dba08a45}
```

Con lo anterior obtenemos la bandera requerida para dar solución al problema, la cual es:

```
picoCTF{grep_is_good_to_find_things_dba08a45}
```
### Notas Adicionales
Después de aplicar el comando, se continuo buscando si había forma alguna de hacerlo un poco más fácil, resultando en que solo se usaría el comando **grep**, sin la necesidad de usar **cat**, por lo que el comando completo es:

```
grep picoCTF file
```
### Referencias
https://www.hostinger.mx/tutoriales/usar-comando-wget#%C2%BFQue_es_el_Comando_Wget
https://www.freecodecamp.org/espanol/news/comandos-de-linux/
https://ryanstutorials.net/linuxtutorial/grep.php
