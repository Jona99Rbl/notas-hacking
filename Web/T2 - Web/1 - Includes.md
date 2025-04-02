### Descripción
Can you get the flag?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Go to this [website](http://saturn.picoctf.net:54937/) and see what you can discover.
### Solución
Una vez que hacemos clic en el enlace que nos proporciona la descripción una vez que se inicio la instancia del desafío, nos encontramos con el siguiente sitio web:

![[Pasted image 20250330203506.png]]

Lo primero que tenemos es el botón "**Say hello**", por lo que procedemos a hacer clic sobre el, después de hacerlo, aparece un mensaje como el siguiente:

![[Pasted image 20250330203529.png]]

Ahora que sabemos que el la bandera se encuentra en diferentes archivos, procederemos a revisar el código fuente de la página web:

```HTML
|   |
|---|
|<!DOCTYPE html>|
||<html lang="en">|
||<head>|
||<meta charset="UTF-8">|
||<meta name="viewport" content="width=device-width, initial-scale=1.0">|
||<meta http-equiv="X-UA-Compatible" content="ie=edge">|
||<link rel="stylesheet" href="[style.css](http://saturn.picoctf.net:54937/style.css)">|
||<title>On Includes</title>|
||</head>|
||<body>|
||<script src="[script.js](http://saturn.picoctf.net:54937/script.js)"></script>|
|||
||<h1>On Includes</h1>|
||<p>Many programming languages and other computer files have a directive,|
||often called include (sometimes copy or import), that causes the|
||contents of a second file to be inserted into the original file. These|
||included files are called copybooks or header files. They are often used|
||to define the physical layout of program data, pieces of procedural code|
||and/or forward declarations while promoting encapsulation and the reuse|
||of code.</p>|
||<br>|
||<p> Source: Wikipedia on Include directive </p>|
||<button type="button" onclick="greetings();">Say hello</button>|
||</body>|
||</html>|
```

Empezamos revisando la hoja de estilos, donde tenemos el siguiente código:

```css
body {
  background-color: lightblue;
}

/*  picoCTF{1nclu51v17y_1of2_  */
```

Es entonces que obtenemos la primera parte de la bandera que soluciona el reto planteado:

```
picoCTF{1nclu51v17y_1of2_
```

Ahora procedemos a revisar el script de JavaScript, que es el segundo enlace que nos permite visitar, al hacer clic, tenemos lo siguiente:

```js
function greetings()
{
  alert("This code is in a separate file!");
}

//  f7w_2of2_6edef411}
```

Obteniendo la segunda parte de la bandera:

```
f7w_2of2_6edef411}
```

Por lo que juntando ambas partes obtenemos la bandera que da solución al reto:

```
picoCTF{1nclu51v17y_1of2_f7w_2of2_6edef411}
```
### Notas Adicionales

### Referencias