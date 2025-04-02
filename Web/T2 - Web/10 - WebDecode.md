### Descripción
Do you know how to use the web inspector?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Do you know how to use the web inspector?
Start searching [here](http://titan.picoctf.net:61280/) to find the flag
### Solución
Iniciamos dando clic en el enlace que se nos muestra después de haber iniciado la instancia del reto, donde luego se nos desplegará el siguiente sitio web:

![[Pasted image 20250331172748.png]]

Se procede a revisar el código fuente de esta página, el cual se muestra a continuación:

```html
|   |
|---|
|<!DOCTYPE html>|
||<html lang="en">|
||<head>|
||<meta charset="UTF-8">|
||<meta http-equiv="X-UA-Compatible" content="IE=edge">|
||<meta name="viewport" content="width=device-width, initial-scale=1.0">|
||<link rel="stylesheet" href="[style.css](http://titan.picoctf.net:61280/style.css)">|
||<link rel="shortcut icon" href="[img/favicon.png](http://titan.picoctf.net:61280/img/favicon.png)" type="image/x-icon">|
||<!-- font (google) -->|
||<link href="[https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400&display=swap](https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400&display=swap)" rel="stylesheet">|
||<title>Home</title>|
||</head>|
||<body>|
||<header>|
||<nav>|
||<div class="logo-container">|
||<a href="[index.html](http://titan.picoctf.net:61280/index.html)"><img src="[img/binding_dark.gif](http://titan.picoctf.net:61280/img/binding_dark.gif)" alt="logo"></a>|
||</div>|
||<div class="navigation-container">|
||<ul>|
||<li><a href="[index.html](http://titan.picoctf.net:61280/index.html)">Home</a></li>|
||<li><a href="[about.html](http://titan.picoctf.net:61280/about.html)">About</a></li>|
||<li><a href="[contact.html](http://titan.picoctf.net:61280/contact.html)">Contact</a></li>|
||</ul>|
||</div>|
||</nav>|
||</header>|
||<section class="banner">|
||<h1>Ha!!!!!! You looking for a flag?</h1>|
||<p>Keep Navigating</p>|
|||
||</section><!-- .banner -->|
||<section class="sec-intro">|
||<div class="col">|
||<p>Haaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa</p>|
||<p>Keepppppppppppppp Searchinggggggggggggggggggg</p>|
||<img src="[./img/multipage-html-img1.jpg](http://titan.picoctf.net:61280/img/multipage-html-img1.jpg)" alt="person">|
||<figcaption>Don't give up!</figcaption>|
||</div>|
||</section><!-- .sec-intro -->|
|||
||<footer>|
||<div class="bottombar">Copyright © 2023 Your_Name. All rights reserved.</div>|
||</footer>|
|||
||</body>|
||</html>|
```

Como no contiene algo referente a la bandera, además de que el sitio te invita a navegar en él, se hace clic entonces en la pestaña **about**, donde después se nos muestra otra parte del sitio web como se muestra a continuación:

![[Pasted image 20250331173009.png]]

Al mencionar que inspeccionemos esta página, ya que podríamos encontrar la bandera aquí, procedemos a revisar el código fuente de la página, teniendo lo siguiente:

```html
|   |   |
|---|---|
||<!DOCTYPE html>|
||<html lang="en">|
||<head>|
||<meta charset="utf-8"/>|
||<meta content="IE=edge" http-equiv="X-UA-Compatible"/>|
||<meta content="width=device-width, initial-scale=1.0" name="viewport"/>|
||<link href="[style.css](http://titan.picoctf.net:61280/style.css)" rel="stylesheet"/>|
||<link href="[img/favicon.png](http://titan.picoctf.net:61280/img/favicon.png)" rel="shortcut icon" type="image/x-icon"/>|
||<!-- font (google) -->|
||<link href="[https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400&amp;display=swap](https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400&display=swap)" rel="stylesheet"/>|
||<title>|
||About me|
||</title>|
||</head>|
||<body>|
||<header>|
||<nav>|
||<div class="logo-container">|
||<a href="[index.html](http://titan.picoctf.net:61280/index.html)">|
||<img alt="logo" src="[img/binding_dark.gif](http://titan.picoctf.net:61280/img/binding_dark.gif)"/>|
||</a>|
||</div>|
||<div class="navigation-container">|
||<ul>|
||<li>|
||<a href="[index.html](http://titan.picoctf.net:61280/index.html)">|
||Home|
||</a>|
||</li>|
||<li>|
||<a href="[about.html](http://titan.picoctf.net:61280/about.html)">|
||About|
||</a>|
||</li>|
||<li>|
||<a href="[contact.html](http://titan.picoctf.net:61280/contact.html)">|
||Contact|
||</a>|
||</li>|
||</ul>|
||</div>|
||</nav>|
||</header>|
||<section class="about" notify_true="cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZjZmNmI3OGF9">|
||<h1>|
||Try inspecting the page!! You might find it there|
||</h1>|
||<!-- .about-container -->|
||</section>|
||<!-- .about -->|
||<section class="why">|
||<footer>|
||<div class="bottombar">|
||Copyright © 2023 Your_Name. All rights reserved.|
||</div>|
||</footer>|
||</section>|
||</body>|
||</html>|
```

Justamente en la sección de la clase **about**, encontramos lo siguiente: cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZjZmNmI3OGF9, que evidentemente se aprecia está en formato base64, debido a que lo componen números del 0 al 9 y letras mayúsculas y minúsculas por lo que se procede a utilizar una herramienta que nos ayude a traducir de ese formato hacia una cadena de caracteres, es entonces que se utiliza "*base64 decode*" de la siguiente manera:

```
Input >> cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZjZmNmI3OGF9

Source character set > UTF-8

Output >> picoCTF{web_succ3ssfully_d3c0ded_f6f6b78a}
```

Una vez realizada la decodificación del texto en base64, tenemos la bandera que da solución al reto:

```
picoCTF{web_succ3ssfully_d3c0ded_f6f6b78a}
```
### Notas Adicionales

### Referencias
https://www.base64decode.org/