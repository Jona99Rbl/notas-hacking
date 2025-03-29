### Descripción
Our flag printing service has started glitching!
Additional details will be available after launching your challenge instance.
##### Una vez iniciada la instancia del desafío:
Our flag printing service has started glitching!`$ nc saturn.picoctf.net 64402`

### Solución
Otra vez se va a emplear la shell virtual de la página picoCTF, puesto que vamos a usar netcat ya que la propia descripción del código nos lo indica así, entonces al iniciar la terminal, ejecutamos la siguiente línea de comando:

```shell
the_robx-picoctf@webshell:~$ nc saturn.picoctf.net 64402
'picoCTF{gl17ch_m3_n07_' + chr(0x39) + chr(0x63) + chr(0x34) + chr(0x32) + chr(0x61) + chr(0x34) + chr(0x35) + chr(0x64) + '}'
```

Como podemos ver la llave casi se encuentra descubierta por la instrucción anterior, ahora nos resta convertir de hexadecimal a ASCII, lo cual haremos con ayuda de una página en línea (en este caso **rapidtables**) donde se tiene lo siguiente:

```
Hex to String Converter

From > Hexadecimal
To > Text

Hex code numbers > 39 63 34 32 61 34 35 64

Character Encoding > ASCII

Result > 9c42a45d
```

Por lo que ahora tenemos la bandera completa de este problema, la cual es:

```
picoCTF{gl17ch_m3_n07_9c42a45d}
```
### Notas Adicionales

### Referencias
https://www.rapidtables.com/convert/number/hex-to-ascii.html