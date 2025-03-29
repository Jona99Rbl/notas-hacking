### Descripción
Find the flag being held on this server to get ahead of the competition [http://mercury.picoctf.net:15931/](http://mercury.picoctf.net:15931/)
### Solución
Se hace clic en el enlace proporcionado en la descripción, con lo cual se despliega un sitio web que nos muestra dos botones, uno que nos cambia el fondo del sitio a rojo o azul, según se dé clic en uno o en otro tal como se aprecia en la siguiente imagen:

![[Pasted image 20250325212522.png]]

Por lo que se procede a revisar el código fuente del sitio, obteniendo lo siguiente:

```html
|<!doctype html>|
||<html>|
||<head>|
||<title>Red</title>|
||<link rel="stylesheet" type="text/css" href="[//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css](http://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css)">|
||<style>body {background-color: red;}</style>|
||</head>|
||<body>|
||<div class="container">|
||<div class="row">|
||<div class="col-md-6">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title" style="color:red">Red</h3>|
||</div>|
||<div class="panel-body">|
||<form action="index.php" method="GET">|
||<input type="submit" value="Choose Red"/>|
||</form>|
||</div>|
||</div>|
||</div>|
||<div class="col-md-6">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title" style="color:blue">Blue</h3>|
||</div>|
||<div class="panel-body">|
||<form action="index.php" method="POST">|
||<input type="submit" value="Choose Blue"/>|
||</form>|
||</div>|
||</div>|
||</div>|
||</div>|
||</div>|
||</body>|
||</html>|
|||
```

Se procede a cambiar de navegador, ya que en un principio había sido iniciado el reto en Chrome y debido a que las herramientas de inspección son más completas en Firefox, se cambia a este navegador, una vez ahí se procede a inspeccionar el código, encontrando lo siguiente:

![[Pasted image 20250325213405.png]]

Como se puede apreciar, se tienen varios métodos de solicitud HTTP, los cuales y después de observar el video proporcionado por el profesor, además de buscar en línea, se tiene que hay diversos métodos como lo son GET, HEAD, PUT, POST, DELETE y demás, por lo que se procede a modificar la solicitud con el método POST, por HEAD, el cual es semejante al GET, pero sin cuerpo de respuesta, se reenvía la petición y se obtiene lo siguiente:

![[Pasted image 20250325213232.png]]

Por lo que habremos obtenido la bandera para la solución a este reto:

```
picoCTF{r3j3ct_th3_du4l1ty_82880908}
```
### Notas Adicionales
- También se puede realizar en consola con el comando:
```
curl -I HEAD http://mercury.picoctf.net:15931/index.php
```
### Referencias
https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods