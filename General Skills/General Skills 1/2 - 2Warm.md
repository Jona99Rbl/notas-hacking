### Descripción
Can you convert the number 42 (base 10) to binary (base 2)?
### Solución
Para darle solución a este ejercicio, se puede hacer de forma semejante al anterior, recurrir a una página que nos permita hacer la conversión entre números de distintas bases como lo es **rapidtables**, donde solo debemos ingresar el número 42 decimal y realizar la conversión hacía binario, como se muestra a continuación:

```
From > Decimal
To > Binary

Enter decimal number > 42

Binary numbre > 101010
```

Una vez realizada la conversión, obtenemos que el resultado buscado es el número **101010**, siendo entonces nuestra bandera la siguiente:

```
picoCTF{101010}
```
### Notas Adicionales
Este ejercicio si bien se pudo haber resuelto de forma manual, al tener la herramienta de la página web, facilita un poco más las tareas. Así como también se pudo haber hecho uso de la calculadora de programador integrada en Windows o bien, usar python haciendo uso de la siguiente instrucción:

```python
print(bin(42))[2:]
```

El corchete es para que muestre el resultado después de la posición, es decir quitarle el prefijo **0b** del resultado.
### Referencias
https://www.rapidtables.com/convert/number/decimal-to-binary.html