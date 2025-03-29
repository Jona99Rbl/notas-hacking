### Descripción
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools! You can download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_atlas/5/challenge.zip)

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
`ssh -p 55032 ctf-player@atlas.picoctf.net`Using the password `1ad5be0d`. Accept the fingerprint with `yes`, and `ls` once connected to begin. Remember, in a shell, passwords are hidden!
### Solución
A pesar de que podemos descargar el archivo **.zip** del reto, tenemos que al iniciar la instancia del reto, nos brinda la forma de conectarnos a través de **ssh** con el puerto y la liga del servidor:

```shell
the_robx-picoctf@webshell:~$ ssh -p 55032 ctf-player@atlas.picoctf.net
The authenticity of host '[atlas.picoctf.net]:55032 ([18.217.83.136]:55032)' can't be established.
ED25519 key fingerprint is SHA256:M8hXanE8l/Yzfs8iuxNsuFL4vCzCKEIlM/3hpO13tfQ.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[atlas.picoctf.net]:55032' (ED25519) to the list of known hosts.
ctf-player@atlas.picoctf.net's password: 
```

Una vez ingresada la contraseña proporcionada por la descripción, se inicia el juego con el siguiente mensaje:

```shell
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess:
```

Como se tienen números entre el 1 y el 1000, se inicia por la mitad, 500

```shell
Enter your guess: 500
Lower! Try again.
```

Debido a que nos dice que el número es menor, partimos a la mitad el rango entre 1 y 499, resultando en 250

```shell
Enter your guess: 250
Lower! Try again.
```

Al seguir diciendo que es mas bajo, volvemos a partir el rango entre 1 y 249, resultando 125

```shell
Enter your guess: 125
Higher! Try again.
```

Como indica que es mayor a 125, se contempla el rango entre 126 y 249, tomando un poco más de la mitad, se opta por el número 190

```shell
Enter your guess: 190
Higher! Try again.
```

Sigue diciendo que es mayor, por lo que nuestro rango se reduce de 191 a 249, tomando el 220

```shell
Enter your guess: 220
Lower! Try again.
```

Cambia a que el número es menor a 220, quedando el rango de números posibles entre los números 191 y 219, por lo que se decide tomar el número 205

```shell
Enter your guess: 205
Lower! Try again.
```

Vuelve a decir que el número es menor, en este caso a 205, quedando el rango entre 191 y 204, tomando el número 198

```shell
Enter your guess: 198
Higher! Try again.
```

Al decir que el número es más grande que 198, se reduce el rango entre 199 y 204, por lo cual se empieza a probar con los siguientes números

```
Enter your guess: 202
Lower! Try again.
Enter your guess: 200
Lower! Try again.
```

Por último, ya solo nos queda probar con el número 199

```shell
Enter your guess: 199
Congratulations! You guessed the correct number: 199
Here's your flag: picoCTF{g00d_gu355_3af33d18}
Connection to atlas.picoctf.net closed.
```

Dándonos ahora la bandera que soluciona el reto:

```shell
picoCTF{g00d_gu355_3af33d18}
```
### Notas Adicionales

### Referencias