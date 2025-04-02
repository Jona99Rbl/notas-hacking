### Descripción
Can you get the flag?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Go to this [website](http://saturn.picoctf.net:57908/) and see what you can discover.
### Solución
Una vez iniciado la instancia del desafío, hacemos clic en el enlace, se nos despliega el siguiente sitio web:

![[Pasted image 20250330204718.png]]

Por lo que empezamos revisando el código fuente de la página web, ya que no se aprecia un indicio o un botón el cual presionar para desencadenar una acción, al ver el código tenemos lo siguiente:

```HTML
|<!DOCTYPE html>|
||<html lang="en">|
||<head>|
||<meta charset="UTF-8">|
||<meta name="viewport" content="width=device-width, initial-scale=1.0">|
||<meta http-equiv="X-UA-Compatible" content="ie=edge">|
||<title>On Histiaeus</title>|
||</head>|
||<body>|
||<h1>On Histiaeus</h1>|
||<p>However, according to Herodotus, Histiaeus was unhappy having to stay in|
||Susa, and made plans to return to his position as King of Miletus by|
||instigating a revolt in Ionia. In 499 BC, he shaved the head of his|
||most trusted slave, tattooed a message on his head, and then waited for|
||his hair to grow back. The slave was then sent to Aristagoras, who was|
||instructed to shave the slave's head again and read the message, which|
||told him to revolt against the Persians.</p>|
||<br>|
||<p> Source: Wikipedia on Histiaeus </p>|
||<!--picoCTF{1n5p3t0r_0f_h7ml_8113f7e2}-->|
||</body>|
||</html>|
|||
```

Como podemos ver, este ejercicio se resolvió de forma sencilla, pues en el mismo código fuente del sitio web, a forma de comentario tenemos la bandera que resuelve el reto, siendo esta:

```
picoCTF{1n5p3t0r_0f_h7ml_8113f7e2}
```
### Notas Adicionales

### Referencias