### Descripción
There is a nice program that you can talk to by using this command in a shell: `$ nc mercury.picoctf.net 22902`, but it doesn't speak English...
### Solución
Al igual que los últimos retos, se involucra netcat, por lo que se volverá a utilizar una vez más el shell virtual de la pagina donde se coloca la instrucción que inicia con el comando **nc**, seguido del link y el puerto para conectarse, donde nos arroja el siguiente resultado:

```
the_robx-picoctf@webshell:~$ nc mercury.picoctf.net 22902
112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
100 
51 
100 
102 
100 
54 
100 
102 
125 
10
```

Como podemos ver, en este caso nos arroja una codificación en decimal, por lo que restará por hacer es convertir de esa base a ASCII, lo cual haremos con la página web **rapidtables**, como se muestra a continuación:

```
ASCII, Hex, Binary, Decimal, Base64 converter

Decimal bytes > 112 105 99 111 67 84 70 123 103 48 48 100 95 107 49 116 116 121 33 95 110 49 99 51 95 107 49 116 116 121 33 95 100 51 100 102 100 54 100 102 125 10

ASCII text > picoCTF{g00d_k1tty!_n1c3_k1tty!_d3dfd6df}
```

Obteniendo como resultado la siguiente bandera del ejercicio:

```
picoCTF{g00d_k1tty!_n1c3_k1tty!_d3dfd6df}
```
### Notas Adicionales
Buscando la forma de visualizar mejor el resultado, se encontró que empleando el comando **tr** que es empleado para la transformación de texto, seguido de las opciones **-d** (eliminar) y **\n** (carácter del salto de línea), quedando de la siguiente manera:

```shell
the_robx-picoctf@webshell:~$ nc mercury.picoctf.net 22902 | tr -d "\n"
```

Obteniendo el resultado a continuación:

```
112 105 99 111 67 84 70 123 103 48 48 100 95 107 49 116 116 121 33 95 110 49 99 51 95 107 49 116 116 121 33 95 100 51 100 102 100 54 100 102 125 10
```
### Referencias
https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html