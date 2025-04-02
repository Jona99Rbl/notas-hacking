### Descripción
How about trying to match a regular expression

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
How about trying to match a regular expression
The website is running [here](http://saturn.picoctf.net:49343/).
### Solución
Una vez iniciada la instancia del reto, hacemos clic en el enlace proporcionado y se nos despliega el siguiente sitio web:

![[Pasted image 20250401185341.png]]

En dicho sitio tenemos que ingresar una entrada y la página web se encargará de validarla, por lo que se procede a realizar una prueba, ya que no sabemos como sea una entrada válida:

![[Pasted image 20250401185619.png]]

Se prueba ingresando "**hola**", le damos clic en submit, saltándonos el siguiente mensaje: 


![[Pasted image 20250401185440.png]]

Es por esto que se procede a revisar el código fuente de la página, encontrando lo siguiente:

```html
|   |   |
|---|---|
||<!DOCTYPE html>|
||<html>|
|||
||<head>|
||<!-- <link rel="stylesheet" href="./index.css" /> -->|
||<style>|
||.heading {|
||width: 100%;|
||height: 40px;|
||background-color: coral;|
||padding-left: 10px;|
||font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;|
||}|
|||
||.normal-form {|
||text-align: center;|
||margin-top: 5%;|
||}|
|||
||#submit-but {|
||border-radius: 0;|
||width: 250px;|
||height: 25px;|
|||
||}|
|||
||#name {|
||width: 250px;|
||height: 25px;|
||background-color: rgb(241, 226, 206);|
||}|
|||
||#sub-heading {|
||color: brown;|
||}|
||</style>|
||</head>|
|||
||<body>|
|||
||<h1 class="heading">PicoCTF</h1>|
||<p></p>|
|||
||<div class="normal-form">|
||<h2 id="sub-heading">Valid Input</h2>|
||<form action="#" onsubmit="return send_request()">|
||<input type="text" id="name" name="input" placeholder="Input text">|
||<br>|
||<br>|
||<button id="submit-but" type="submit" id="submit-button">SUBMIT</button>|
||</form>|
||</div>|
||</body>|
||<script>|
||function send_request() {|
||let val = document.getElementById("name").value;|
||// ^p.....F!?|
||fetch(`/flag?input=${val}`)|
||.then(res => res.text())|
||.then(res => {|
||const res_json = JSON.parse(res);|
||alert(res_json.flag)|
||return false;|
||})|
||return false;|
||}|
|||
||</script>|
|||
||</html>|
```

Al no tener un indicio de como obtener la bandera, procedemos a buscar el termino "**Expresiones Regulares**", encontramos que son patrones que se utilizan para hacer coincidir combinaciones de caracteres en cadenas.

Revisando la información, encontramos en el código un comentario con lo siguiente, que nos puede indicar el patrón para obtener una entrada válida para el sitio web:

```
^p.....F!?
```

Es por esto que usamos una herramienta como lo es **regexr.com**, que es un sitio web que nos permite hacer combinaciones para crear cadenas de texto que coincidan con la expresión encontrada, tal como se pude ver en la siguiente imagen:

![[Pasted image 20250401190038.png]]

Una vez obtenida nuestra frase: **pasdfgF**, procedemos a ingresarla al sitio web:

![[Pasted image 20250401190143.png]]

Ahora al darle clic a SUBMIT, nos aparece el siguiente mensaje que nos demuestra que la entrada ingresada resultó válida:

![[Pasted image 20250401190123.png]]

Por lo que hemos obtenido la bandera que resuelve el reto:

```
picoCTF{succ3ssfully_matchtheregex_f89ea585}
```
### Notas Adicionales

### Referencias
https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Regular_expressions
https://regexr.com/
