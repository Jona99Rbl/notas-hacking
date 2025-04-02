### Descripción
Can you get the flag?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Can you get the flag? 
Go to this [website](http://saturn.picoctf.net:55837/) and see what you can discover.
### Solución
Una vez que se inicia la instancia del desafío, procedemos a dar clic en el enlace que se nos muestra, donde se despliega el siguiente sitio web: 

![[Pasted image 20250330212543.png]]

Como nos dice que solo letras y números son permitidos en el usuario y contraseña, al desconocer los datos reales, se ingresan unos inventados, en este caso para el usuario se ingresa "*hola*", y para la contraseña "*1234*".

![[Pasted image 20250330212612.png]]

Al dar clic sobre el botón **Login**, nos aparece el siguiente mensaje:

```
Log In Failed
```

Por lo que volvemos a la página anterior y procedemos a revisar el código fuente del sitio web, donde nos encontramos lo siguiente:

```HTML
|   |
|---|
|<!DOCTYPE html>|
||<html lang="en">|
||<head>|
||<meta charset="UTF-8">|
||<meta name="viewport" content="width=device-width, initial-scale=1.0">|
||<meta http-equiv="X-UA-Compatible" content="ie=edge">|
||<link rel="stylesheet" href="[style.css](http://saturn.picoctf.net:55837/style.css)">|
||<title>Secure Customer Portal</title>|
||</head>|
||<body>|
|||
||<h1>Secure Customer Portal</h1>|
|||
||<p>Only letters and numbers allowed for username and password.</p>|
|||
||<form role="form" action="login.php" method="post">|
||<input type="text" name="username" placeholder="Username" required|
||autofocus></br>|
||<input type="password" name="password" placeholder="Password" required>|
||<button type="submit" name="login">Login</button>|
||</form>|
||</body>|
||</html>|
```

Lo primero que vamos a revisar es la hoja de estilos, puesto que muchas veces ahí se contiene algo respecto a la bandera que da solución al reto, teniendo lo siguiente:

```css
body {
  background-color: lightblue;
}
```

Como podemos ver, en este caso no nos proporciona algo que nos sea de utilidad, por lo que procedemos ahora a revisar el código **.php** del Login, por lo que al hacer clic sobre el, se nos despliega lo siguiente tambien como parte del código fuente:

```HTML
||<title>Login Page</title>|
||</head>|
||<body>|
||<script src="[secure.js](http://saturn.picoctf.net:55837/secure.js)"></script>|
|||
||<p id='msg'></p>|
|||
||<form hidden action="admin.php" method="post" id="hiddenAdminForm">|
||<input type="text" name="hash" required id="adminFormHash">|
||</form>|
|||
||<script type="text/javascript">|
||function filter(string) {|
||filterPassed = true;|
||for (let i =0; i < string.length; i++){|
||cc = string.charCodeAt(i);|
|||
||if ( (cc >= 48 && cc <= 57) \||
||(cc >= 65 && cc <= 90) \||
||(cc >= 97 && cc <= 122) )|
||{|
||filterPassed = true;|
||}|
||else|
||{|
||return false;|
||}|
||}|
|||
||return true;|
||}|
|||
||window.username = "";|
||window.password = "";|
|||
||usernameFilterPassed = filter(window.username);|
||passwordFilterPassed = filter(window.password);|
|||
||if ( usernameFilterPassed && passwordFilterPassed ) {|
|||
||loggedIn = checkPassword(window.username, window.password);|
|||
||if(loggedIn)|
||{|
||document.getElementById('msg').innerHTML = "Log In Successful";|
||document.getElementById('adminFormHash').value = "2196812e91c29df34f5e217cfd639881";|
||document.getElementById('hiddenAdminForm').submit();|
||}|
||else|
||{|
||document.getElementById('msg').innerHTML = "Log In Failed";|
||}|
||}|
||else {|
||document.getElementById('msg').innerHTML = "Illegal character in username or password."|
||}|
||</script>|
|||
||</body>|
```

Por lo que nos llama la atención el script de JavaScript, pues contiene la palabra "**checkPassword**" la cual como su nombre lo indica nos permitirá saber que se espera de contraseña, al hacer clic, nos encontramos lo siguiente: 

```js
function checkPassword(username, password)
{
  if( username === 'admin' && password === 'strongPassword098765' )
  {
    return true;
  }
  else
  {
    return false;
  }
}
```

Como podemos ver, nos dice el usuario y contraseña para poder ingresar de forma correcta, por lo cual volvemos a recargar la página e ingresamos los datos que obtuvimos después de andar husmeando en el código, como lo muestra la siguiente imagen:

![[Pasted image 20250330213258.png]]

Al hacer clic en **Login**, ahora si se nos muestra la bandera que da solución a este reto:

```
picoCTF{j5_15_7r4n5p4r3n7_a8788e61}
```
### Notas Adicionales

### Referencias