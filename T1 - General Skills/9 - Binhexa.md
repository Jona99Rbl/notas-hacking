### Descripción
How well can you perfom basic binary operations?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Start searching for the flag here `nc titan.picoctf.net 63080`
### Solución
Iniciamos conectándonos a través de **netcat** al servidor proporcionado por la descripción del reto, para lo cual requerimos el comando **nc** 

```shell
the_robx-picoctf@webshell:~$ nc titan.picoctf.net 63080

Welcome to the Binary Challenge!"
Your task is to perform the unique operations in the given order and find the final result in hexadecimal that yields the flag.
```

Iniciado el **Reto Binario**, nos proporcionan 2 números binarios, los cuales son los siguientes:

```shell
Binary Number 1: 10100011
Binary Number 2: 00110110
```

Una vez mostrados los números con los que vamos a operar, aparece la primer operación a realizar, que neste caso corresponde a un desplazamiento a la izquierda (<<) del número 1 en 1 bit

```shell
Question 1/6:
Operation 1: '<<'
Perform a left shift of Binary Number 1 by 1 bits.
Enter the binary result:
```

Para realizar la operación, buscamos una herramienta como lo es una calculadora binaria, encontrando una en la página web de **rapidtables**, donde se realizo la operación de la siguiente manera:

```
Number 1 > 10100011

Operation > left shift (<<)

Number 2 > 1

Binary Result > 101000110
```

Por lo que una vez que tenemos el resultado, lo ingresamos:

```shell
Enter the binary result: 101000110
Correct!
```

Al ser correcto, se despliega la siguiente operación, la cual es un desplazamiento a la derecha (>>) del número 2 en 1 bit

```shell
Question 2/6:
Operation 2: '>>'
Perform a right shift of Binary Number 2 by 1 bits .
Enter the binary result:
```

Por lo que volvemos a nuestra herramienta y realizamos lo siguiente:

```
Number 1 > 00110110

Operation > right shift (>>)

Number 2 > 1

Binary Result > 11011
```

Ingresamos el resultado obtenido:

```shell
Enter the binary result: 11011
Correct!
```

Ahora se nos despliega la tercer operación, siendo una multiplicación (`*`) del número 1 por el 2

```shell
Question 3/6:
Operation 3: '*'
Perform the operation on Binary Number 1&2.
Enter the binary result:
```

Regresamos a la herramienta y hacemos la operación de la siguiente forma:

```
Number 1 > 10100011

Operation > mult (x)

Number 2 > 00110110

Binary Result > 10001001100010
```

Obtenido el resultado, lo ingresamos:

```shell
Enter the binary result: 10001001100010
Correct!
```

Nos arroja ahora la operación 4, siendo una suma (+) del número 1 más el número 2

```shell
Question 4/6:
Operation 4: '+'
Perform the operation on Binary Number 1&2.
Enter the binary result:
```

Pasando a hacer la operación en nuestra herramienta:

```
Number 1 > 10100011

Operation > add (+)

Number 2 > 00110110

Binary Result > 11011001
```

Ingresamos el resultado obtenido:

```shell
Enter the binary result: 11011001
Correct!
```

Pasamos ahora a la operación 5, la cual es una compuerta AND (&) entre el número 1 y 2

```shell
Question 5/6:
Operation 5: '&'
Perform the operation on Binary Number 1&2.
Enter the binary result:
```

Regresamos a nuestra herramienta y hacemos la operación:

```
Number 1 > 10100011

Operation > and (&)

Number 2 > 00110110

Binary Result > 00100010
```

Ingresamos el resultado obtenido:

```shell
Enter the binary result: 00100010
Correct!
```

Ahora nos muestra la operación 6 y última, la cual es una compuerta OR (|) entre el número 1 y 2

```shell
Question 6/6:
Operation 6: '|'
Perform the operation on Binary Number 1&2.
Enter the binary result:
```

Volvemos a nuestra herramienta a realizar la operación de la siguiente manera:

```
Number 1 > 10100011

Operation > or (|)

Number 2 > 00110110

Binary Result > 10110111
```

Ingresamos el último resultado:

```shell
Enter the binary result: 10110111
Correct!
```

Finalmente nos aparece la siguiente pregunta:

```shell
Enter the results of the last operation in hexadecimal: 
```

Gracias a que nuestra herramienta nos arroja el resultado en distintas bases numéricas, solo tenemos que hacer el cambio, puesto que la operación se conserva, resultando en lo siguiente:

```
Number 1 > 10100011

Operation > or (|)

Number 2 > 00110110

Hex Result > B7
```

Ingresamos el resultado de la operación anterior convertido en hexadecimal:

```shell
Enter the results of the last operation in hexadecimal: B7

Correct answer!
The flag is: picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_6862762d}
```

Dándonos así la bandera que soluciona el reto:

```
picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_6862762d}
```
### Notas Adicionales

### Referencias
https://www.rapidtables.com/calc/math/binary-calculator.html