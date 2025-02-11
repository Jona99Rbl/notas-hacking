### Descripción
Using netcat (nc) is going to be pretty important. Can you connect to `jupiter.challenges.picoctf.org` at port `64287` to get the flag?
### Solución
Para solucionarlo, usamos  **netcat** en la terminal virtual que nos ofrece la página de picoCTF en la sección de picoGym, donde se le indica la instrucción iniciando con el comando **nc** seguido de la dirección y puerto a donde conectarse, tal como se ve a continuación:

```shell
the_robx-picoctf@webshell:~$ nc jupiter.challenges.picoctf.org 64287
You're on your way to becoming the net cat master
picoCTF{nEtCat_Mast3ry_284be8f7}
```

Con lo cual nos arroja la bandera de solución para este reto, la cual es:

```
picoCTF{nEtCat_Mast3ry_284be8f7}
```
### Notas Adicionales

### Referencias
https://linux.die.net/man/1/nc