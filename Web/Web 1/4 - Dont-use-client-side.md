### Descripción
Can you break into this super secure portal? `https://jupiter.challenges.picoctf.org/problem/29835/` ([link](https://jupiter.challenges.picoctf.org/problem/29835/)) or http://jupiter.challenges.picoctf.org:29835
### Solución
Iniciamos haciendo clic en el enlace que se nos proporciona en la descripción, donde luego de hacer eso, nos aparecerá el siguiente sitio web:

![[Pasted image 20250321225353.png]]

Como desconocemos la contraseña para acceder, se intenta acceder con una inventada en el momento, en este caso se intenta con "*hola123*", como se aprecia a continuación

![[Pasted image 20250321225458.png]]

Pero al no ser la contraseña correcta, nos despliega el siguiente mensaje:

![[Pasted image 20250321225527.png]]

Por lo que se decide investigar en red lo que es **client-side** y es ahí donde nos damos cuenta de que también existe un **serve-side**, es decir, uno corresponde al cliente que realiza la solicitud y otro corresponde al servidor que proporciona el servicio, es por lo que se decide revisar el código fuente del sitio web, mostrándose lo siguiente:

```html
|   |   |
|---|---|
||<html>|
||<head>|
||<title>Secure Login Portal</title>|
||</head>|
||<body bgcolor=blue>|
||<!-- standard MD5 implementation -->|
||<script type="text/javascript" src="[md5.js](https://jupiter.challenges.picoctf.org/problem/29835/md5.js)"></script>|
|||
||<script type="text/javascript">|
||function verify() {|
||checkpass = document.getElementById("pass").value;|
||split = 4;|
||if (checkpass.substring(0, split) == 'pico') {|
||if (checkpass.substring(split*6, split*7) == '723c') {|
||if (checkpass.substring(split, split*2) == 'CTF{') {|
||if (checkpass.substring(split*4, split*5) == 'ts_p') {|
||if (checkpass.substring(split*3, split*4) == 'lien') {|
||if (checkpass.substring(split*5, split*6) == 'lz_7') {|
||if (checkpass.substring(split*2, split*3) == 'no_c') {|
||if (checkpass.substring(split*7, split*8) == 'e}') {|
||alert("Password Verified")|
||}|
||}|
||}|
|||
||}|
||}|
||}|
||}|
||}|
||else {|
||alert("Incorrect password");|
||}|
|||
||}|
||</script>|
||<div style="position:relative; padding:5px;top:50px; left:38%; width:350px; height:140px; background-color:yellow">|
||<div style="text-align:center">|
||<p>This is the secure login portal</p>|
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

Como podemos ver, en este caso, la función que verifica la contraseña ingresada, quedó del lado del cliente, siendo que esto es un error, puesto que el que debe validar la contraseña es el servidor, pero en este caso también tenemos la bandera que resuelve el reto, solo que la tenemos en partes y desorganizada, pero una vez que se descifra como se encuentra organizada la bandera, es al fin que obtenemos la misma:

```
picoCTF{no_clients_plz_7723ce}
```
### Notas Adicionales

### Referencias
https://www.pitchlabs.org/library/technology/applications/what-is-client-side-scripting-vs-server-side-scripting?campaignid=19950232516&adgroupid=149300526873&creative=655312097035&matchtype=&device=c&keyword=&gad_source=1&gclid=Cj0KCQjwv_m-BhC4ARIsAIqNeBu5c3LxneHvZJYEQcSj4_e52FnLOAKaId3tw2PMLmkKSFv9lrSICWQaAlihEALw_wcB