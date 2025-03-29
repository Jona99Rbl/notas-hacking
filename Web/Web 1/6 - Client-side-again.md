### Descripción
Can you break into this super secure portal? `https://jupiter.challenges.picoctf.org/problem/60786/` ([link](https://jupiter.challenges.picoctf.org/problem/60786/)) or http://jupiter.challenges.picoctf.org:60786
### Solución
Iniciamos haciendo clic en el enlace que nos proporciona la descripción, se nos muestra el siguiente sitio web:

![[Pasted image 20250322093833.png]]

Intentamos acceder con una contraseña creada, dado que no conocemos o tenemos indicio de cual podría ser, por lo que ingresamos la misma de *hola123*, como se aprecia en la siguiente imagen:

![[Pasted image 20250322094340.png]]

Al dar clic en **verify**, nos aparece el siguiente mensaje:

![[Pasted image 20250322094424.png]]

Lo que nos da a entender que evidentemente no sabemos la contraseña correcta que nos permita acceder al sitio.

Al revisar el código fuente de la página encontramos lo siguiente:

```html
|   |
|---|
|<html>|
||<head>|
||<title>Secure Login Portal V2.0</title>|
||</head>|
||<body background="barbed_wire.jpeg" >|
||<!-- standard MD5 implementation -->|
||<script type="text/javascript" src="[md5.js](https://jupiter.challenges.picoctf.org/problem/60786/md5.js)"></script>|
|||
||<script type="text/javascript">|
||var _0x5a46=['f49bf}','_again_e','this','Password\x20Verified','Incorrect\x20password','getElementById','value','substring','picoCTF{','not_this'];(function(_0x4bd822,_0x2bd6f7){var _0xb4bdb3=function(_0x1d68f6){while(--_0x1d68f6){_0x4bd822['push'](_0x4bd822['shift']());}};_0xb4bdb3(++_0x2bd6f7);}(_0x5a46,0x1b3));var _0x4b5b=function(_0x2d8f05,_0x4b81bb){_0x2d8f05=_0x2d8f05-0x0;var _0x4d74cb=_0x5a46[_0x2d8f05];return _0x4d74cb;};function verify(){checkpass=document[_0x4b5b('0x0')]('pass')[_0x4b5b('0x1')];split=0x4;if(checkpass[_0x4b5b('0x2')](0x0,split*0x2)==_0x4b5b('0x3')){if(checkpass[_0x4b5b('0x2')](0x7,0x9)=='{n'){if(checkpass[_0x4b5b('0x2')](split*0x2,split*0x2*0x2)==_0x4b5b('0x4')){if(checkpass[_0x4b5b('0x2')](0x3,0x6)=='oCT'){if(checkpass[_0x4b5b('0x2')](split*0x3*0x2,split*0x4*0x2)==_0x4b5b('0x5')){if(checkpass['substring'](0x6,0xb)=='F{not'){if(checkpass[_0x4b5b('0x2')](split*0x2*0x2,split*0x3*0x2)==_0x4b5b('0x6')){if(checkpass[_0x4b5b('0x2')](0xc,0x10)==_0x4b5b('0x7')){alert(_0x4b5b('0x8'));}}}}}}}}else{alert(_0x4b5b('0x9'));}}|
||</script>|
||<div style="position:relative; padding:5px;top:50px; left:38%; width:350px; height:140px; background-color:gray">|
||<div style="text-align:center">|
||<p>New and Improved Login</p>|
|||
||<p>Enter valid credentials to proceed</p>|
||<form action="index.html" method="post">|
||<input type="password" id="pass" size="8" />|
||<br/>|
||<input type="submit" value="verify" onclick="verify(); return false;" />|
||</form>|
||</div>|
||</div>|
||</body>|
||</html>|
```

Donde se puede apreciar que es semejante al ejercicio que se resolvió del mismo tipo anteriormente, pero con la diferencia de que esta bandera se nota más complicada de descifrar, por lo cual al revisar los videos proporcionados por el profesor, descubrimos que esta ofuscada, por lo que se decide investigar en red ese termino.

El cual nos dice que es "*una serie de transformaciones de código que convierten el código JS simple y fácil de leer en una versión modificada que es extremadamente difícil de entender y aplicar ingeniería inversa*".

Por lo que ahora se procede a inspeccionar el sitio web, donde encontramos el código fuente de la página, como se aprecia a continuación:

![[Pasted image 20250322101107.png]]

Copiamos la variable que se muestra a continuación:

```js
var _0x5a46=['f49bf}','_again_e','this','Password\x20Verified','Incorrect\x20password','getElementById','value','substring','picoCTF{','not_this'];(function(_0x4bd822,_0x2bd6f7){var _0xb4bdb3=function(_0x1d68f6){while(--_0x1d68f6){_0x4bd822['push'](_0x4bd822['shift']());}};_0xb4bdb3(++_0x2bd6f7);}(_0x5a46,0x1b3));var _0x4b5b=function(_0x2d8f05,_0x4b81bb){_0x2d8f05=_0x2d8f05-0x0;var _0x4d74cb=_0x5a46[_0x2d8f05];return _0x4d74cb;};function verify(){checkpass=document[_0x4b5b('0x0')]('pass')[_0x4b5b('0x1')];split=0x4;if(checkpass[_0x4b5b('0x2')](0x0,split*0x2)==_0x4b5b('0x3')){if(checkpass[_0x4b5b('0x2')](0x7,0x9)=='{n'){if(checkpass[_0x4b5b('0x2')](split*0x2,split*0x2*0x2)==_0x4b5b('0x4')){if(checkpass[_0x4b5b('0x2')](0x3,0x6)=='oCT'){if(checkpass[_0x4b5b('0x2')](split*0x3*0x2,split*0x4*0x2)==_0x4b5b('0x5')){if(checkpass['substring'](0x6,0xb)=='F{not'){if(checkpass[_0x4b5b('0x2')](split*0x2*0x2,split*0x3*0x2)==_0x4b5b('0x6')){if(checkpass[_0x4b5b('0x2')](0xc,0x10)==_0x4b5b('0x7')){alert(_0x4b5b('0x8'));}}}}}}}}else{alert(_0x4b5b('0x9'));}}
```

Luego procedemos a buscar y utilizar una herramienta que permita hacer una desofuscación del código, por lo que recurrimos a **JavaScripy Deobfuscator**, donde solo tenemos que ingresar el código copiado y obtendremos una salida que sea un poco más fácil de entender:

![[Pasted image 20250322102429.png]]

Obteniendo el siguiente código:

```js
var _0x5a46 = ["f49bf}", "_again_e", "this", "Password Verified", "Incorrect password", "getElementById", "value", "substring", "picoCTF{", "not_this"];
(function (_0x4bd822, _0x2bd6f7) {
  var _0xb4bdb3 = function (_0x1d68f6) {
    while (--_0x1d68f6) {
      _0x4bd822.push(_0x4bd822.shift());
    }
  };
  _0xb4bdb3(++_0x2bd6f7);
}(_0x5a46, 435));
var _0x4b5b = function (_0x2d8f05, _0x4b81bb) {
  _0x2d8f05 = _0x2d8f05 - 0;
  var _0x4d74cb = _0x5a46[_0x2d8f05];
  return _0x4d74cb;
};
function verify() {
  checkpass = document[_0x4b5b("0x0")]("pass")[_0x4b5b("0x1")];
  split = 4;
  if (checkpass[_0x4b5b("0x2")](0, split * 2) == _0x4b5b("0x3")) {
    if (checkpass[_0x4b5b("0x2")](7, 9) == "{n") {
      if (checkpass[_0x4b5b("0x2")](split * 2, split * 2 * 2) == _0x4b5b("0x4")) {
        if (checkpass[_0x4b5b("0x2")](3, 6) == "oCT") {
          if (checkpass[_0x4b5b("0x2")](split * 3 * 2, split * 4 * 2) == _0x4b5b("0x5")) {
            if (checkpass.substring(6, 11) == "F{not") {
              if (checkpass[_0x4b5b("0x2")](split * 2 * 2, split * 3 * 2) == _0x4b5b("0x6")) {
                if (checkpass[_0x4b5b("0x2")](12, 16) == _0x4b5b("0x7")) {
                  alert(_0x4b5b("0x8"));
                }
              }
            }
          }
        }
      }
    }
  } else {
    alert(_0x4b5b("0x9"));
  }
}
```

Ahora que ya tenemos el código con una presentación un poco más fácil de leer, analizando el código nos damos cuenta de que la función que se encarga de verificar la contraseña, hace uso de un arreglo de cadenas de caracteres, el cual se podría intentar descifrar, pero resulta algo complejo. 

Por lo que se opta por usar la consola que viene incluida en la herramienta de inspección, donde vamos ingresar el arreglo de caracteres, donde después se revisa el contenido del arreglo y después se empieza a jugar con las combinaciones de palabras para formar la bandera, recordando que sigue la estructura de **picoCTF{flag}**, realizándose mediante la concatenación de las diversas posiciones del arreglo como se muestra en la siguiente imagen:


![[Pasted image 20250322103751.png]]

Con lo cual obtenemos la siguiente bandera, dando solución al reto presente:

```
picoCTF{not_this_again_ef49bf}
```
### Notas Adicionales

### Referencias
https://jscrambler.com/blog/javascript-obfuscation-the-definitive-guide
https://deobfuscate.io/