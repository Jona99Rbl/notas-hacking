### Descripción
This website can be rendered only by **picobrowser**, go and catch the flag! `https://jupiter.challenges.picoctf.org/problem/26704/` ([link](https://jupiter.challenges.picoctf.org/problem/26704/)) or http://jupiter.challenges.picoctf.org:26704
### Solución
Hacemos clic en el enlace de la descripción para acceder al sitio web del reto, el cual se muestra de la siguiente manera:

![[Pasted image 20250322083428.png]]

Al hacer clic en el botón verde que dice **Flag**, nos aparece el siguiente mensaje en la página:

![[Pasted image 20250322083520.png]]

Por lo que se procede a revisar el código fuente de la página:

```html
|   |   |
|---|---|
||<!DOCTYPE html>|
||<html lang="en">|
|||
||<head>|
||<title>My New Website</title>|
|||
||<link href="[https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css](https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css)" rel="stylesheet">|
|||
||<link href="[https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css](https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css)" rel="stylesheet">|
|||
||<script src="[https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)"></script>|
|||
||<script src="[https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js](https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js)"></script>|
|||
||</head>|
|||
||<body>|
|||
||<div class="container">|
||<div class="header">|
||<nav>|
||<ul class="nav nav-pills pull-right">|
||<li role="presentation" class="active"><a href="[#](https://jupiter.challenges.picoctf.org/problem/26704/flag#)">Home</a>|
||</li>|
||<li role="presentation"><a href="[/unimplemented](https://jupiter.challenges.picoctf.org/unimplemented)">Sign In</a>|
||</li>|
||<li role="presentation"><a href="[/unimplemented](https://jupiter.challenges.picoctf.org/unimplemented)">Sign Out</a>|
||</li>|
||</ul>|
||</nav>|
||<h3 class="text-muted">My New Website</h3>|
||</div>|
|||
||<!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->|
|||
|||
||<div class="alert alert-danger alert-dismissible" role="alert" id="myAlert">|
||<button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>|
||<!-- <strong>Title</strong> --> You&#39;re not picobrowser!|
||Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36|
||</div>|
|||
|||
|||
||<div class="jumbotron">|
||<p class="lead"></p>|
||<p><a href="[/flag](https://jupiter.challenges.picoctf.org/flag)" class="btn btn-lg btn-success btn-block"> Flag</a></p>|
||</div>|
|||
|||
||<footer class="footer">|
||<p>&copy; PicoCTF 2019</p>|
||</footer>|
|||
||</div>|
||<script>|
||$(document).ready(function(){|
||$(".close").click(function(){|
||$("myAlert").alert("close");|
||});|
||});|
||</script>|
||</body>|
|||
||</html>|
```

Como podemos ver, no hay un indicio claro de como poder obtener la bandera, procedemos a inspeccionar la parte de red de este sitio web, lo cual se hace con la opción de **Inspeccionar** en el menú desplegado al hacer clic derecho, mostrándose algo así:

![[Pasted image 20250322091220.png]]

Procedemos a revisar el **flag**, donde nos encontramos con lo siguiente, resaltando el encabezado de ***User-Agent***:

![[Pasted image 20250322091350.png]]

Al investigar en red, el **User-Agent** permite al servidor identificar los datos del cliente, lo cual en este caso es el causante de que no nos sea proporcionada la bandera para solucionar el reto, pero el navegador no nos permite realizar modificaciones en el encabezado, por lo que se intentará el método con la consola (en nuestro caso, la misma consola proporcionada por la página picoGym), para lo cual haremos uso del comando **curl** junto con los argumento -H para agregar encabezados personalizados en la solicitud que se va a hacer, además de usar grep para filtrar las coincidencias con lo que queremos, por lo que una vez que tenemos todo, lo ingresamos a la consola obteniendo lo siguiente:

```shell
the_robx-picoctf@webshell:~$ curl https://jupiter.challenges.picoctf.org/problem/26704/flag -H "User-Agent: picobrowser" | grep picoCTF
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2115  100  2115    0     0   9257      0 --:--:-- --:--:-- --:--:--  9276
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{p1c0_s3cr3t_ag3nt_e9b160d0}</code></p>
```

Como podemos ver, la ejecución del comando nos arrojó la bandera que estábamos buscando, siendo esta:

```
picoCTF{p1c0_s3cr3t_ag3nt_e9b160d0}
```
### Notas Adicionales

### Referencias
https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Headers/User-Agent
https://www.hostinger.com/mx/tutoriales/comando-curl