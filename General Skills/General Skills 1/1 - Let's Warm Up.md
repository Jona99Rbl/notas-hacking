### Descripción
If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?
### Solución
Para resolver esto, se requiere de poder convertir el número hexadecimal 0x70 a su carácter en ASCII, para lo cual podemos utilizar una página como lo es **rapidtables** (https://www.rapidtables.com/), donde solo tendremos que ingresar el número hexadecimal y este nos podrá hacer la conversión para ASCII, tal como se muestra a continuación:

```
From > Hexadecimal
To > Text

Character Encoding > ASCII

Hex Code > 70

Result > p
```

Por lo que ahora obtenemos el resultado que es "**p**", resultando en nuestra siguiente bandera:
```
picoCTF{p}
```
### Notas Adicionales
Buscando en internet, también se mencionaba la posibilidad de resolverlo con ayuda de Python, gracias a la conversión que puede hacer el propio lenguaje, por lo que solo bastaría ingresar lo siguiente:

```python
print(chr(0x70))
```
### Referencias
https://www.rapidtables.com/convert/number/hex-to-ascii.html
