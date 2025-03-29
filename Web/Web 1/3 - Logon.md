### Descripción
The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at? `https://jupiter.challenges.picoctf.org/problem/44573/` ([link](https://jupiter.challenges.picoctf.org/problem/44573/)) or http://jupiter.challenges.picoctf.org:44573
### Solución
Al igual que en el caso de los ejercicios anteriores, se inicia haciendo clic en en enlace proporcionado en la descripción, una vez hecho esto, nos aparecerá algo así:

![[Pasted image 20250321205244.png]]

Por lo que se intenta acceder con el usuario **Joe**, ya que la misma descripción así lo indica, dado que no cocemos, la contraseña de Joe, inventaremos una al azar como lo es "*hola123*" 

![[Pasted image 20250321211414.png]]

Al hacer clic en "**Sing In**", nos marca el siguiente error: *I'm sorry Joe's password is super secure. You're not getting in that way.*, por lo que revisando las pistas tenemos una que nos dice que tal parece que el sitio se encuentra verificando únicamente la contraseña de Joe, por lo que, con cualquier otro usuario se podría acceder.

En este caso se hace un nuevo intento pero ahora con el usuario "*hola*" y la misma contraseña que en el intento anterior (*hola123*), como se puede apreciar en seguida:

![[Pasted image 20250321211805.png]]

A diferencia del otro intento, en este tenemos una respuesta positiva, ya que podemos acceder, pero también se nos muestra lo siguiente:

![[Pasted image 20250321212017.png]]

Donde pese a haber accedido, no nos arroja bandera alguna, por lo que ahora pasaremos a inspeccionar este sitio web, lo cual se hace haciendo clic derecho y luego seleccionando la opción "**Inspeccionar**" del menú. Una vez dentro de ahí tendremos a la vista lo siguiente:

![[Pasted image 20250321212306.png]]

Gracias al apoyo brindado por el profesor a través del tutorial, nos damos cuenta de que al seleccionar la bandera nos encontramos con que tenemos encabezados HTTP, los cuales son los de solicitud y respuesta, donde después de la explicación proporcionada por el profesor, tenemos que se pueden modificar las **cookies**, para lo cual tenemos que descargar una extensión en el navegador, la cual se llama **Cookie-Editor**, como lo muestra la siguiente imagen:

![[Pasted image 20250321213151.png]]

Una vez que se instaló la extensión, recargamos la página a la cual nos condujo el reto para no perder el inicio de sesión logrado en ese momento, por lo que ahora hacemos uso de la herramienta y tenemos la de **admin** que se muestra en la imagen siguiente y la cual tiene un valor de ***False***, lo cual ocasiona que nos se nos otorgue la bandera.

![[Pasted image 20250321213247.png]]

Por lo que se cambia ese valor a ***True*** y se procede a guardarla.

![[Pasted image 20250321213343.png]]

Volvemos a recargar la página web y como veremos a continuación, desaparece el mensaje de "*No flag for you*" y aparecerá lo siguiente:

![[Pasted image 20250321213416.png]]

Por lo que ahora ya tenemos la bandera que soluciona el reto y esta es:

```
picoCTF{th3_c0nsp1r4cy_l1v3s_0c98aacc}
```
### Notas Adicionales
404 - Error
200 - Todo Ok
307 - Servidor falló
### Referencias
https://developer.mozilla.org/es/docs/Glossary/HTTPS
https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Headers
https://developer.mozilla.org/en-US/docs/Glossary/Request_header
https://developer.mozilla.org/en-US/docs/Glossary/Response_header
https://developer.mozilla.org/es/docs/Web/HTTP/Guides/Cookies