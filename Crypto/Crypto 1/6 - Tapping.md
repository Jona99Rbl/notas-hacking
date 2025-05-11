### Descripción
Theres tapping coming in from the wires. What's it saying `nc jupiter.challenges.picoctf.org 21610`.
### Solución
Iniciamos conectándonos al servidor que nos es proporcionado por la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1]
└─$ nc jupiter.challenges.picoctf.org 21610
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ...-- ----. ----- ..--- ----- .---- ----. ..... .---- ----. } 
```

Como podemos ver la bandera aparece codificada por puntos y guiones, lo que recuerda al código Morse, por lo que ahora que sabemos como se encuentra codificada, procedemos a utilizar una herramienta como CyberChef para que nos ayude con la decodificación, siguiendo la siguiente receta:

```
Input > .--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ...-- ----. ----- ..--- ----- .---- ----. ..... .---- ----. } 

Recipe > From Morse Code

Output > PICOCTFM0RS3C0D31SFUN3902019519
```

Obteniendo así la bandera que da solución al reto:

```
PICOCTF{M0RS3C0D31SFUN3902019519}
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/C%C3%B3digo_morse
https://gchq.github.io/CyberChef/