### Descripción
We have several pages hidden. Can you find the one with the flag?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
We have several pages hidden. Can you find the one with the flag?
The website is running [here](http://saturn.picoctf.net:63312/).
### Solución
Iniciamos haciendo clic en el enlace que se nos presenta después de haber iniciado la instancia del reto, con lo cual se nos despliega el siguiente sitio web:

![[Pasted image 20250331170444.png]]

Debido a que de momento no nos permite ver el código fuente del sitio web, se procede a inspeccionarlo y poder revisar el código, donde resalta el link de **secret**, ya que el otro link que aparece es la aplicación en línea, lo ignoramos.

![[Pasted image 20250331170808.png]]

Es por esto que al enlace original se le agrega "**/secret/**" para poder acceder a esa parte de la página web, por lo cual el link queda de la siguiente manera:

```
http://saturn.picoctf.net:63312/secret/
```

Una vez que colocamos el enlace anterior en la barra del buscador, nos aparece el siguiente sitio web:

![[Pasted image 20250331170933.png]]

Al proceder a revisar el código fuente de este sitio web, nos encontramos otro link que hace referencia otra parte del enlace para llegar a la bandera al involucrar la palabra "**Hidden**" (**Oculto**), como podemos ver a continuación:

```html
|   |
|---|
|<!DOCTYPE html>|
||<html>|
||<head>|
||<title></title>|
||<link rel="stylesheet" href="[hidden/file.css](http://saturn.picoctf.net:53506/secret/hidden/file.css)" />|
||</head>|
|||
||<body>|
||<h1>Finally. You almost found me. you are doing well</h1>|
||<img src="[https://media1.tenor.com/images/0a6aff9f825af62c05adfbd75039cc7b/tenor.gif?itemid=4648337](https://media1.tenor.com/images/0a6aff9f825af62c05adfbd75039cc7b/tenor.gif?itemid=4648337)" alt="Something Like That GIF - Andy Parksandrecreation Wtf GIFs" style="max-width: 833px; background-color: rgb(151, 121, 85);" width="833" height="937.125">|
||</body>|
||</html>|
```

Por lo que el enlace se vuelve a modificar para agregar el aparado "**hidden/**", resultando en lo siguiente:

```
http://saturn.picoctf.net:63312/secret/hidden/
```

Al cargar el nuevo enlace en el navegador, nos aparece el siguiente sitio web:

![[Pasted image 20250331171406.png]]

Por lo que una vez más se procede a revisar el código fuente del nuevo sitio web, resultando en el siguiente código HTML: 

```html
|   |   |
|---|---|
||<!DOCTYPE html>|
||<html>|
||<head>|
||<title>LOGIN</title>|
||<!-- css -->|
||<link href="[superhidden/login.css](http://saturn.picoctf.net:53506/secret/hidden/superhidden/login.css)" rel="stylesheet" />|
||</head>|
||<body>|
||<form>|
||<div class="container">|
||<form method="" action="/secret/assets/popup.js">|
||<div class="row">|
||<h2 style="text-align: center">|
||Login with Social Media or Manually|
||</h2>|
||<div class="vl">|
||<span class="vl-innertext">or</span>|
||</div>|
|||
||<div class="col">|
||<a href="[#](http://saturn.picoctf.net:53506/secret/hidden/#)" class="fb btn">|
||<i class="fa fa-facebook fa-fw"></i> Login with Facebook|
||</a>|
||<a href="[#](http://saturn.picoctf.net:53506/secret/hidden/#)" class="twitter btn">|
||<i class="fa fa-twitter fa-fw"></i> Login with Twitter|
||</a>|
||<a href="[#](http://saturn.picoctf.net:53506/secret/hidden/#)" class="google btn">|
||<i class="fa fa-google fa-fw"></i> Login with Google+|
||</a>|
||</div>|
|||
||<div class="col">|
||<div class="hide-md-lg">|
||<p>Or sign in manually:</p>|
||</div>|
|||
||<input|
||type="text"|
||name="username"|
||placeholder="Username"|
||required|
||/>|
||<input|
||type="password"|
||name="password"|
||placeholder="Password"|
||required|
||/>|
||<input type="hidden" name="db" value="superhidden/xdfgwd.html" />|
|||
||<input|
||type="submit"|
||value="Login"|
||onclick="alert('Thank you for the attempt but oops! try harder. better luck next time')"|
||/>|
||</div>|
||</div>|
||</form>|
||</div>|
|||
||<div class="bottom-container">|
||<div class="row">|
||<div class="col">|
||<a href="[#](http://saturn.picoctf.net:53506/secret/hidden/#)" style="color: white" class="btn">Sign up</a>|
||</div>|
||<div class="col">|
||<a href="[#](http://saturn.picoctf.net:53506/secret/hidden/#)" style="color: white" class="btn">Forgot password?</a>|
||</div>|
||</div>|
||</div>|
||</form>|
||</body>|
||</html>|
```

Del código anterior, se destaca la palabra "**Superhidden**", es decir super oculto, por lo que se intuye que también forma parte del enlace que nos va a llevar a obtener la bandera del reto, por lo que una vez más se actualiza el link, resultando en el siguiente:

```
http://saturn.picoctf.net:63312/secret/hidden/superhidden/
```

Cargando una vez más en el navegador el link resultante, tenemos que se nos despliega el siguiente sitio web:

![[Pasted image 20250331171428.png]]

Al mencionar que ya lo encontramos pero no es visible en la página, se da a entender que posiblemente estará en el código fuente del sitio, por lo que se procede a consultarlo, resultando en lo siguiente:

```html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link rel="stylesheet" href="mycss.css" />
  </head>

  <body>
    <h1>Finally. You found me. But can you see me</h1>
    <h3 class="flag">picoCTF{succ3ss_@h3n1c@10n_51b260fe}</h3>
  </body>
</html>

```

Como podemos ver, si nos arrojó la bandera que da solución al reto, siendo esta: 

```
picoCTF{succ3ss_@h3n1c@10n_51b260fe}
```
### Notas Adicionales

### Referencias