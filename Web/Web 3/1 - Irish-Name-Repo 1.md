### Descripción
There is a website running at `https://jupiter.challenges.picoctf.org/problem/50009/` ([link](https://jupiter.challenges.picoctf.org/problem/50009/)) or http://jupiter.challenges.picoctf.org:50009. Do you think you can log us in? Try to see if you can login!
### Solución
Al hacer el clic en el enlace proporcionado en la descripción, aparece un sitio como el que se muestra a continuación, donde se tiene una lista de famosos irlandeses:

![[Pasted image 20250328220903.png]]

Al hacer clic en las tres barras que aparecen las siguientes opciones del menú:

![[Pasted image 20250328221047.png]]

Por lo que se decide ingresar en el aparado de "**Support**", donde se obtiene lo siguiente:

![[Pasted image 20250328221116.png]]

Como esto no nos indica algo referente a la bandera, se procede a cambiarse a la opción de "**Admin Login**" donde se muestra una ventana como la siguiente:

![[Pasted image 20250328221406.png]]

Se hace el intento de acceder haciendo uso de la palabra **admin** como usuario y contraseña y nos muestra en pantalla un mensaje como el siguiente donde nos dice que el intento de acceder es fallido.

![[Pasted image 20250328221439.png]]

Por lo que entonces se procede a revisar el código fuente de la página web y se obtiene el siguiente código HTML, donde se destaca la hoja de estilos pero esta no nos arrojaba nada de utilidad para la bandera a la hora de consultarla.

```html
|   |   |
|---|---|
||<!doctype html>|
||<html>|
||<head>|
||<title>Login</title>|
||<link rel="stylesheet" type="text/css" href="[//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css](https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css)">|
||</head>|
||<body>|
||<div class="container">|
||<div class="row">|
||<div class="col-md-12">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title">Log In</h3>|
||</div>|
||<div class="panel-body">|
||<form action="login.php" method="POST">|
||<fieldset>|
||<div class="form-group">|
||<label for="username">Username:</label>|
||<input type="text" id="username" name="username" class="form-control">|
||</div>|
||<div class="form-group">|
||<label for="password">Password:</label>|
||<div class="controls">|
||<input type="password" id="password" name="password" class="form-control">|
||</div>|
||</div>|
||<input type="hidden" name="debug" value="0">|
|||
||<div class="form-actions">|
||<input type="submit" value="Login" class="btn btn-primary">|
||</div>|
||</fieldset>|
||</form>|
||</div>|
||</div>|
||</div>|
||</div>|
||</div>|
||</body>|
||</html>|
```

Entonces ahora se procede a inspeccionar al sitio web, donde se aprecia el mismo código HTML del código fuente contenido en bloques.

![[Pasted image 20250328221649.png]]

Es por esto que se usa la herramienta de seleccionar un elemento de la página para inspeccionarlo y hacemos clic en el botón de "**Login**" se nos muestra lo de la siguiente imagen, donde lo destacable es lo que hace mención a la palabra **hidden**, lo cual nos hace referencia a que se encuentra oculto algo para nosotros al tener esta un valor de 0:

![[Pasted image 20250328221727.png]]

Por lo que se procede a modificar ese valor por 1 y se cierra la herramienta.

![[Pasted image 20250328221800.png]]

Una vez realizada la modificación anterior se intenta acceder nuevamente con el mismo usuario y contraseña de antes, igual volvemos a fallar, pero apreciamos lo que se nos había ocultado, siendo esta la búsqueda que se ejecuta al momento de hacer el login.

![[Pasted image 20250328221848.png]]

Como vemos en la información que teníamos oculta, se necesitaría de una inyección de SQL, lo cual se investiga que es una forma en que el atacante intenta manipular una consulta SQL para que se ejecute de una manera no prevista por el sistema, con el objetivo de acceder a información sensible o modificar datos, es ahí donde se nos hace mención de ejemplos de como hacerlo, en nuestro caso usaremos la siguiente:

```
' or 1=1;
```

Por lo que se usará esta inyección como contraseña, pero se mantendrá el usuario **admin**, esperando tener suerte a la hora de acceder al sitio.

![[Pasted image 20250328222001.png]]

Como podeos ver por el mensaje principal, hemos podido acceder al sitio web haciendo uso de la inyección de SQL, la cual en este caso al observar la sentencia de búsqueda, con el hecho de que se tenga el **or 1=1**, hace que todo se haga verdadero, pues siempre 1 será igual a 1.

![[Pasted image 20250328222026.png]]

Por lo que hemos obtenido la bandera que da solución a este reto:

```
picoCTF{s0m3_SQL_fb3fe2ad}
```
### Notas Adicionales
También se puede usar la forma de "admin'-- " para obtener el mismo resultado.
### Referencias
https://www.w3schools.com/sql/sql_injection.asp