### Descripción
There is some interesting information hidden around this site [http://mercury.picoctf.net:27393/](http://mercury.picoctf.net:27393/). Can you find it?
### Solución
Iniciamos haciendo clic en el enlace proporcionado por la descripción, con lo cual se despliega el siguiente sitio web:

![[Pasted image 20250325225134.png]]

Por lo que se procede a revisar el código fuente del sitio web, obteniendo lo siguiente:

```html
|   |
|---|
|<!doctype html>|
||<html>|
||<head>|
||<title>Scavenger Hunt</title>|
||<link href="[https://fonts.googleapis.com/css?family=Open+Sans\|Roboto](https://fonts.googleapis.com/css?family=Open+Sans\|Roboto)" rel="stylesheet">|
||<link rel="stylesheet" type="text/css" href="[mycss.css](http://mercury.picoctf.net:27393/mycss.css)">|
||<script type="application/javascript" src="[myjs.js](http://mercury.picoctf.net:27393/myjs.js)"></script>|
||</head>|
|||
||<body>|
||<div class="container">|
||<header>|
||<h1>Just some boring HTML</h1>|
||</header>|
|||
||<button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">How</button>|
||<button class="tablink" onclick="openTab('tababout', this, '#222')">What</button>|
|||
||<div id="tabintro" class="tabcontent">|
||<h3>How</h3>|
||<p>How do you like my website?</p>|
||</div>|
|||
||<div id="tababout" class="tabcontent">|
||<h3>What</h3>|
||<p>I used these to make this site: <br/>|
||HTML <br/>|
||CSS <br/>|
||JS (JavaScript)|
||</p>|
||<!-- Here's the first part of the flag: picoCTF{t -->|
||</div>|
|||
||</div>|
|||
||</body>|
||</html>|
```

Como podemos ver, se nos da la primera parte de la bandera, siendo:

```
picoCTF{t
```

Por lo que ahora, procedemos a revisar la hoja de estilos que viene ahí, mostrando lo siguiente:

```css
div.container {
    width: 100%;
}

header {
    background-color: black;
    padding: 1em;
    color: white;
    clear: left;
    text-align: center;
}

body {
    font-family: Roboto;
}

h1 {
    color: white;
}

p {
    font-family: "Open Sans";
}

.tablink {
    background-color: #555;
    color: white;
    float: left;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 14px 16px;
    font-size: 17px;
    width: 50%;
}

.tablink:hover {
    background-color: #777;
}

.tabcontent {
    color: #111;
    display: none;
    padding: 50px;
    text-align: center;
}

#tabintro { background-color: #ccc; }
#tababout { background-color: #ccc; }

/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```

Obteniendo así la segunda parte de la bandera, siendo:

```
h4ts_4_l0
```

Ahora visitamos el script, arrojándonos lo siguiente:

```js
function openTab(tabName,elmnt,color) {
    var i, tabcontent, tablinks;
    tabcontent = document.getElementsByClassName("tabcontent");
    for (i = 0; i < tabcontent.length; i++) {
	tabcontent[i].style.display = "none";
    }
    tablinks = document.getElementsByClassName("tablink");
    for (i = 0; i < tablinks.length; i++) {
	tablinks[i].style.backgroundColor = "";
    }
    document.getElementById(tabName).style.display = "block";
    if(elmnt.style != null) {
	elmnt.style.backgroundColor = color;
    }
}

window.onload = function() {
    openTab('tabintro', this, '#222');
}

/* How can I keep Google from indexing my website? */
```

En este caso no nos arrojó alguna parte de la bandera, pero si tiene una pregunta sobre como hacer que Google no indexe su sitio web, por lo que esto nos lleva al archivo **robots.txt**, que este archivo era para restringir el acceso de los bots a ciertas partes del sitio web, para acceder a ello, ingresamos el siguiente enlace:

```
http://mercury.picoctf.net:27393/robots.txt
```

Al ingresar este enlace, se nos muestra lo siguiente:

```
User-agent: *
Disallow: /index.html
# Part 3: t_0f_pl4c
# I think this is an apache server... can you Access the next flag?
```

Con esto nos arroja la tercera parte de la bandera siendo:

```
t_0f_pl4c
```

Cabe destacar lo último que nos menciona sobre los servidores apache, se procede a investigar más respecto a ellos, encontramos uno que es servidor HTTP, el cual se destacan los ficheros **.htaccess**, los cuales permiten realizar cambios en la configuración de estos servidores, por lo que se modifica el enlace original, resultando en:

```
http://mercury.picoctf.net:27393/.htaccess
```

Una vez accedido a ese enlace se nos muestra lo siguiente:

```
# Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
```

Dándonos la cuarta parte de la bandera:

```
3s_2_lO0k
```

Ahora nos queda revisar lo referente a las Mac, donde gracias al video proporcionado por el profesor, encontramos los ".**DS_Store**", que es un archivo que almacena atributos personalizados de la carpeta que lo contiene, como la posición de los iconos o la imagen de fondo.

Por lo que ahora volvemos a modificar el enlace original, quedando de la siguiente manera:

```
http://mercury.picoctf.net:27393/.DS_Store
```

Al ingresar a ese enlace, nos muestra lo siguiente:

```
Congrats! You completed the scavenger hunt. Part 5: _d375c750}
```

Obtenemos así la última parte de la bandera, siendo:

```
_d375c750}
```

Por lo que reuniendo todas las partes obtenemos la bandera completa, siendo:

```
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_d375c750}
```
### Notas Adicionales

### Referencias
https://httpd.apache.org/docs/trunk/es/getting-started.html
https://httpd.apache.org/docs/2.4/es/howto/htaccess.html
https://es.wikipedia.org/wiki/.DS_Store