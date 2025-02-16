### Descripción
To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337? Connect with `nc jupiter.challenges.picoctf.org 15130`.
### Solución
Al iniciar como en la descripción nos dice, debemos conectarnos a **netcat**, por lo que una vez que abrimos el shell virtual de la página web de picoGym (picoCTF), escribimos el comando nc seguido de la dirección y puerto a conectarse, tal como lo podemos ver a continuación:

```shell
the_robx-picoctf@webshell:~$ nc jupiter.challenges.picoctf.org 15130
Let us see how data is stored
submarine
Please give the 01110011 01110101 01100010 01101101 01100001 01110010 01101001 01101110 01100101 as a word.
...
you have 45 seconds.....

Input:
```

Como podemos ver nos arroja una palabra codificada en binario, por lo que procederemos a emplear una herramienta que nos permita hacer la conversión de binario hacia ASCII, para poder ingresar la entrada que nos piden y así continuar con la solución al reto. Una vez en cyberchef, hacemos lo siguiente:

```
Input > 01110011 01110101 01100010 01101101 01100001 01110010 01101001 01101110 01100101

Recipe > From Binary

Output > submarine
```

Con lo que una vez hemos logrado la decodificación, procedemos a ingresar la palabra, donde se nos muestra ahora una con codificación octal, tal como podemos ver:

```shell
Input:
submarine
Please give me the  154 141 155 160 as a word.
Input:
```

Por lo que volvemos a cyberchef para obtener la palabra que nos es solicitada siguiendo la receta a continuación:

```
Input > 154 141 155 160

Recipe > From Octal

Output > lamp
```

Por lo que ingresamos esa frase, para que ahora se nos pide decodificar una palabra que viene encriptada en hexadecimal, como se muestra en seguida:

```shell
Input:
lamp
Please give me the 6c696d65 as a word.
Input:
```

Recurrimos una vez más a cyberchef para hacer la conversión solicitada de la siguiente manera:

```
Input > 6c696d6

Recipe > From Hex

Output > lime
```

Ingresando la frase resultante de la decodificación, finalmente nos muestra la bandera que nos dice que el reto ha sido solucionado de forma correcta:

```shell
Input:
lime
You've beaten the challenge
Flag: picoCTF{learning_about_converting_values_02167de8}
```

Resultando en la bandera a ingresar:

```
picoCTF{learning_about_converting_values_02167de8}
```
### Notas Adicionales

### Referencias
https://gchq.github.io/CyberChef/