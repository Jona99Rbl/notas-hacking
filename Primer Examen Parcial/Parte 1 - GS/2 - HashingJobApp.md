### Descripción
If you want to hash with the best, beat this test!

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
If you want to hash with the best, beat this test!
`nc saturn.picoctf.net 56038`
### Solución
Iniciamos conectándonos al servidor mediante el comando nc en consola como lo podemos ver a continuación:

```shell
jony@DESKTOP-TN1UVD2:~$ nc saturn.picoctf.net 56038
Please md5 hash the text between quotes, excluding the quotes: 'school cafeteria'
Answer:
```

Se nos pide crear un hash md5sum de una cadena en especial, por lo que en otra terminal hacemos uso del comando **echo**, donde se le pasa el argumento "-n" para que no agregue nuevas líneas al final del texto donde además el resultado será enviado a md5sum, la cual nos hará la conversión al hash que estamos buscando: 

```shell
jony@DESKTOP-TN1UVD2:~$ echo -n 'school cafeteria' | md5sum
3e06bd96dca5d429a2e06b3ea613eb41  -
```

Una vez nos proporcionó el resultado, lo ingresamos en el campo correspondiente:

```shell
3e06bd96dca5d429a2e06b3ea613eb41
3e06bd96dca5d429a2e06b3ea613eb41
Correct.
Please md5 hash the text between quotes, excluding the quotes: 'Adolf Hitler'
Answer:
```

Volvemos a repetir lo mismo pero ahora con la nueva frase otorgada:

```shell
jony@DESKTOP-TN1UVD2:~$ echo -n 'Adolf Hitler' | md5sum
540dea05a35b0fc9a050f36db954a484  -
```

Obtenido el resultado lo volvemos a ingresar:

```shell
540dea05a35b0fc9a050f36db954a484
540dea05a35b0fc9a050f36db954a484
Correct.
Please md5 hash the text between quotes, excluding the quotes: 'communists'
Answer:
```

Se nos pide hacerlo una vez más para la nueva frase propuesta:

```shell
jony@DESKTOP-TN1UVD2:~$ echo -n 'communists' | md5sum
60dc96cdf23898725b1f6862e99b5109  -
```

Una vez más volvemos a ingresar el resultado obtenido en la consola

```shell
60dc96cdf23898725b1f6862e99b5109
60dc96cdf23898725b1f6862e99b5109
Correct.
picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}
```

Como podemos ver, nos arroja la bandera que da solución a este reto:

```
picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}
```
### Notas Adicionales

### Referencias