### Descripción
Kishor Balan tipped us off that the following code may need inspection: `https://jupiter.challenges.picoctf.org/problem/44924/` ([link](https://jupiter.challenges.picoctf.org/problem/44924/)) or http://jupiter.challenges.picoctf.org:44924
### Solución
En este reto lo primero que se realiza es hacer clic sobre el link que nos proporciona en la descripción, lo que una vez realizado, se nos muestra el siguiente sitio web:

![[Pasted image 20250319213959.png]]

Una vez dentro al hacer clic en la pestaña "*What*" nos muestra el mensaje de "**I made a website**" y en el caso de la otra prestaña "How", encontramos el siguiente texto:

![[Pasted image 20250319214432.png]]

No es hasta que le hacemos caso al encabezado de la página, que procedemos a inspeccionar esa pagina web, lo cual se realiza haciendo clic derecho sobre el sitio web y luego yendo a la opción de "Ver código fuente de la página", como se aprecia en la siguiente imagen:

![[Pasted image 20250319214648.png]]

Una vez dentro, se nos despliega el código HTML de la página, siendo el siguiente:

```html
|   |   |
|---|---|
||<!doctype html>|
||<html>|
||<head>|
||<title>My First Website :)</title>|
||<link href="[https://fonts.googleapis.com/css?family=Open+Sans\|Roboto](https://fonts.googleapis.com/css?family=Open+Sans\|Roboto)" rel="stylesheet">|
||<link rel="stylesheet" type="text/css" href="[mycss.css](https://jupiter.challenges.picoctf.org/problem/44924/mycss.css)">|
||<script type="application/javascript" src="[myjs.js](https://jupiter.challenges.picoctf.org/problem/44924/myjs.js)"></script>|
||</head>|
|||
||<body>|
||<div class="container">|
||<header>|
||<h1>Inspect Me</h1>|
||</header>|
|||
||<button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">What</button>|
||<button class="tablink" onclick="openTab('tababout', this, '#222')">How</button>|
|||
||<div id="tabintro" class="tabcontent">|
||<h3>What</h3>|
||<p>I made a website</p>|
||</div>|
|||
||<div id="tababout" class="tabcontent">|
||<h3>How</h3>|
||<p>I used these to make this site: <br/>|
||HTML <br/>|
||CSS <br/>|
||JS (JavaScript)|
||</p>|
||<!-- Html is neat. Anyways have 1/3 of the flag: picoCTF{tru3_d3 -->|
||</div>|
|||
||</div>|
|||
||</body>|
||</html>|
```

Si observamos bien, en un comentario viene la primera parte de las tres que conforman la bandera para la solución de este reto, siendo:

```
picoCTF{tru3_d3
```

En el mismo código HTML, se puede apreciar que contiene dos ligas, una que es referente a una hoja de estilos <link rel="stylesheet" type="text/css" href="[mycss.css](https://jupiter.challenges.picoctf.org/problem/44924/mycss.css)"> y otra de un script en JavaScript <script type="application/javascript" src="[myjs.js](https://jupiter.challenges.picoctf.org/problem/44924/myjs.js)"></script>

Por lo que hacemos clic en la primera y se nos muestra el contenido de la hoja de estilos:

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

/* You need CSS to make pretty pages. Here's part 2/3 of the flag: t3ct1ve_0r_ju5t */
```

Donde podemos ver la segunda parte de la bandera en un comentario al final de la hoja de estilos y esta es:

```
t3ct1ve_0r_ju5t
```

Ya por último se visita la segunda liga, donde vemos el contenido del script de JS, siendo lo que se muestra a continuación:

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

/* Javascript sure is neat. Anyways part 3/3 of the flag: _lucky?f10be399} */
```

Obteniendo así la última parte de la bandera, siendo:

```
_lucky?f10be399}
```

Juntando las tres partes de la bandera, obtenemos lo siguiente, dando solución al reto:

```
picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?f10be399}
```
### Notas Adicionales

### Referencias