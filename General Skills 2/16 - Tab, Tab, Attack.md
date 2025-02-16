### Descripción
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: [Addadshashanammu.zip](https://mercury.picoctf.net/static/659efd595171e4c40378be6a2e9b7298/Addadshashanammu.zip)
### Solución
Al tener un archivo **.zip**, procederemos a descargarlo primero a través del comando **wget**:

```shell
the_robx-picoctf@webshell:~$ wget https://mercury.picoctf.net/static/659efd595171e4c40378be6a2e9b7298/Addadshashanammu.zip
--2025-02-16 04:42:25--  https://mercury.picoctf.net/static/659efd595171e4c40378be6a2e9b7298/Addadshashanammu.zip
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4520 (4.4K) [application/octet-stream]
Saving to: 'Addadshashanammu.zip'

Addadshashanammu.zip     100%[=======================>]   4.41K  --.-KB/s    in 0s 

2025-02-16 04:42:25 (1.51 GB/s) - 'Addadshashanammu.zip' saved [4520/4520]
```

Una vez descargado revisamos el contenido del directorio con **ls**, donde encontramos el archivo **Addadshashanammu.zip**

```shell
the_robx-picoctf@webshell:~$ ls
Addadshashanammu.zip  README.txt  file  flag  ltdis.sh  static  strings  warm
```

Procederemos ahora a extraer el contenido de ese archivo con el comando **unzip**, donde podemos ver como se van "creando" las carpetas contenidas en el comprimido.

```shell
the_robx-picoctf@webshell:~$ unzip Addadshashanammu.zip 
Archive:  Addadshashanammu.zip
   creating: Addadshashanammu/
   creating: Addadshashanammu/Almurbalarammi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/
   creating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/
  inflating: Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet
```

Ahora realizaremos un cambio de directorio mediante **cd**, donde solo escribiremos la primera letra de la carpeta y solo daremos con la tecla tabulador hasta llegar a la ultima carpeta accesible.

```shell
the_robx-picoctf@webshell:~$ cd Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/
```

Usando el comando **ls** observamos lo que contenga la carpeta.

```shell
the_robx-picoctf@webshell:~/Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku$ ls
fang-of-haynekhtnamet
```

Ahora volveremos a usar el comando **strings**, que nos sirve para buscar cadenas de texto en el archivo, junto con el comando **grep** para buscar coincidencias con la palabra *pico*, que es el inicio de las banderas de este reto.

```shell
the_robx-picoctf@webshell:~/Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku$ strings fang-of-haynekhtnamet | grep pico
*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_524e3dc4}
```

Lo cual nos arroja la bandera que estábamos buscando:

```
picoCTF{l3v3l_up!_t4k3_4_r35t!_524e3dc4}
```
### Notas Adicionales

### Referencias
https://linux.die.net/man/1/strings