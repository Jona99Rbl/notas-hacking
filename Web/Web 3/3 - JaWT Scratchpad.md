### Descripción
Check the admin scratchpad! `https://jupiter.challenges.picoctf.org/problem/58210/` or http://jupiter.challenges.picoctf.org:58210

También contiene la siguiente advertencia:

Internal server errors can be intentionally returned by this challenge. If you experience one, try clearing your cookies.
### Solución
Iniciamos copiando el enlace proporcionado por la descripción e ingresándolo en el navegador, después de dar enter, se nos carga el siguiente sitio web:

![[Pasted image 20250329130049.png]]

Por lo que se hace el intento con **admin**, dado que es en lo que consiste el reto, acceder a las notas del administrador, pero al hacerlo nos aparece lo siguiente, esperado después de que evidentemente nosotros no el administrador.

![[Pasted image 20250329130415.png]]

Por lo que entonces se procede a ingresar con el nombre de **Jony**, al intentarlo obtenemos lo siguiente:

![[Pasted image 20250329130526.png]]

Dado que si nos dejó entrar, procedemos a revisar las cookies del sitio, ya que también nos hace mención de las mismas, pero antes debemos de saber que es **JWT**, lo cual navegando en internet nos dice que es un estándar usado comúnmente en sistemas de autenticación y autorización, ya que permiten transmitir información de manera compacta y segura.

Ahora que sabemos lo que es, procederemos a buscar una herramienta (como **jwt.io**) que nos ayude a descifrar lo que contenga el valor encriptado la cookie que vamos a revisar denominada como "*jwt*", cuyo contenido se aprecia a continuación:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiam9ueSJ9.tfMVRjsmvEDmt-R5-G7NaaAmjL7Su_c6YuyTVgs9lcs
```

Por lo que introducimos esto a la herramienta de la siguiente manera, donde de forma automática nos da el descifrado de lo que ingresamos, tal como lo muestra la siguiente imagen:

![[Pasted image 20250329132138.png]]

Por lo que ahora procederemos a cambiar el usuario de *jony* por **admin** y probar si con esa modificación obtendremos la bandera que dará solución del reto, una vez realizado eso en la página, obtendremos lo siguiente:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4ifQ.-vh-85mhRjMzTUsaJEWhgJwu-_EzDOy8zI0a9dik2Ww
```

Cambiamos ese valor en la cookie del sitio, la cual obtuvimos gracias a la herramienta de **cookie-editor**, la guardamos y al refrescar la página, nos encontramos con lo siguiente:

![[Pasted image 20250329132621.png]]

Esto ya nos había sido advertido al inicio del reto y esto es debido a que el nos hace falta conocer la contraseña del administrador, por lo que seguirá es el poder obtenerla, para ayudarnos, en el sitio se nos hacía mención de John, por lo que para poder acceder otra vez a la página inicial del sitio borramos la cookie que colocamos, es decir la que lleva por nombre **jwt**.

Al hacer clic sobre John, obtenemos que es una herramienta que nos ayuda al crackeo de contraseñas.

Para poder hacer uso de ello, volvemos a ingresar al sitio con nuestro usuario y volvemos a recuperar el valor de la cookie *jwt*, abrimos una terminal en linux, en mi caso usaré la de KALI en máquina virtual y creamos un archivo nano denominado como hash, así como se aprecia en la siguiente imagen:

![[Screenshot_2025-03-29_15_55_51.png]]

Debido a que yo no contaba con John instalado, procederemos a hacerlo a través de la terminal, una vez realizado esto, procederemos a consultar los diccionarios de palabras usando en la terminal el comando siguiente:

```
ls /usr/share/wordlists
```

Como podemos ver en la siguiente imagen, tenemos una carpeta comprimida con el nombre de rockyou.txt.gz

![[Screenshot_2025-03-29_15_58_42.png]]

Por lo que procederemos a descomprimirla con el siguiente comando. como muestra la captura de pantalla:

```
sudo gzip -d /user/share/wordlists/rockyou.txt.gz
```

![[Screenshot_2025-03-29_16_03_06.png]]

Una vez descomprimido, tenemos que ya podemos usar la lista de palabras con la herramienta **john**, como se muestra a continuación con el siguiente comando:

```
john hash -w=/usr/share/wordlists/rockyou.txt
```

![[Screenshot_2025-03-29_16_07_57.png]]

Obteniendo que se usó la palabra ilovepico para firmar el token, por lo que ahora solo nos resta ingresarlo como firma para los tokens en la página que nos permite desencriptar la cookie, como lo muestra la siguiente imagen:

![[Pasted image 20250329141145.png]]

Obteniendo así el nuevo valor de cookie, el cual va a ser ingresado mediante cookie-editor en **jwt**:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4ifQ.gtqDl4jVDvNbEe_JYEZTN19Vx6X9NNZtRVbKPBkhO-s
```

Al hacerlo y guardar el valor de la cookie, recargamos la página y obtenemos lo que se muestra en la siguiente imagen:

![[Pasted image 20250329141634.png]]

Por lo tanto habremos obtenido la bandera que da solución al reto:

```
picoCTF{jawt_was_just_what_you_thought_44c752f5}
```
### Notas Adicionales

### Referencias
https://www.oracle.com/mx/database/what-is-json/
https://jwt.io/introduction
https://jwt.io/#debugger-io
https://github.com/openwall/john
