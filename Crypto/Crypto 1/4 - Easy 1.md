### Descripción
The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help `UFJKXQZQUNB` with the key of `SOLVECRYPTO`. Can you use this [table](https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt) to solve it?.
### Solución
Iniciamos descargando la tabla que nos dan en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1/easy1]
└─$ wget https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt 
--2025-05-11 00:55:16--  https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1571 (1.5K) [application/octet-stream]
Saving to: ‘table.txt’

table.txt              100%[===========================>]   1.53K  --.-KB/s    in 0.001s  

2025-05-11 00:55:16 (1.47 MB/s) - ‘table.txt’ saved [1571/1571]
```

Como se aprecia es un archivo de texto, por lo que ahora se procede a investigar que es un "one time pad" o "libreta de un solo uso", encontrando que es un tipo de algoritmos de cifrado por el que el texto en claro se combina con una clave aleatoria o «libreta» igual de larga que el texto en claro y que sólo se utiliza una vez.

También el cifrado que nos proponen en la descripción correspondería al cifrado de Vigenère, el cual es un cifrado basado en diferentes series de caracteres o letras del cifrado César formando estos caracteres una tabla, llamada tabla de Vigenère, que se usa como clave.

Se procede ahora a abrir la tabla, teniendo lo siguiente:

```
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
   +----------------------------------------------------
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D | D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E | E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F | F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G | G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H | H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I | I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J | J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K | K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L | L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M | M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N | N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
O | O P Q R S T U V W X Y Z A B C D E F G H I J K L M N
P | P Q R S T U V W X Y Z A B C D E F G H I J K L M N O
Q | Q R S T U V W X Y Z A B C D E F G H I J K L M N O P
R | R S T U V W X Y Z A B C D E F G H I J K L M N O P Q
S | S T U V W X Y Z A B C D E F G H I J K L M N O P Q R
T | T U V W X Y Z A B C D E F G H I J K L M N O P Q R S
U | U V W X Y Z A B C D E F G H I J K L M N O P Q R S T
V | V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
X | X Y Z A B C D E F G H I J K L M N O P Q R S T U V W
Y | Y Z A B C D E F G H I J K L M N O P Q R S T U V W X
Z | Z A B C D E F G H I J K L M N O P Q R S T U V W X Y
```

Dicha tabla corresponde a la tabla que se usa en el cifrado de Vigenère, por lo que para resolverlo se hace uso de una herramienta como CyberChef, aplicando la siguiente receta:

```
Input > UFJKXQZQUNB

Recipe > Vigenère Decode (Key = SOLVECRYPTO)

Output > CRYPTOISFUN
```

Por lo que ahora solo nos resta construir la bandera que da solución al reto, resultando en lo siguiente:

```
picoctf{CRYPTOISFUN}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Libreta_de_un_solo_uso
https://es.wikipedia.org/wiki/Cifrado_de_Vigen%C3%A8re
https://gchq.github.io/CyberChef/