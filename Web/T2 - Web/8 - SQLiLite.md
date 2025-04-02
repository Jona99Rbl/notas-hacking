### Descripción
Can you login to this website?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Can you login to this website?
Try to login [here](http://saturn.picoctf.net:53720/).
### Solución
Iniciamos dando clic en el enlace que se nos presenta iniciada la instancia del desafío, donde al presionarlo, se nos despliega ell siguiente sitio web:

![[Pasted image 20250331171829.png]]

Al involucrar la palabra SQL, se procede a utilizar la inyección **' or 1=1;**, ya que sabemos que con esta podemos acceder a la base de datos siempre y cuando esta cuente con dicha debilidad, en el caso del usuario, en las pistas nos hace mención que lo hagamos con **admin**, tal como se puede ver a continuación:

![[Pasted image 20250331171921.png]]

Al ingresar esos datos y luego dar clic en **Login**, obtendremos que se pudo ingresar de forma correcta al sitio, como lo demuestra el siguiente mensaje:

![[Pasted image 20250331171948.png]]

Pero como no aparece rastro de la bandera en la pantalla actual, se procede a revisar el código fuente de la página, el cual se muestra enseguida:

```php
|   |
|---|
|<pre>username: admin|
||password: &#039; or 1=1;|
||SQL query: SELECT * FROM users WHERE name=&#039;admin&#039; AND password=&#039;&#039; or 1=1;&#039;|
||</pre><h1>Logged in! But can you see the flag, it is in plainsight.</h1><p hidden>Your flag is: picoCTF{L00k5_l1k3_y0u_solv3d_it_ec8a64c7}</p>|
```

Por lo que revisando el código, encontramos al final la bandera que da solución a este reto:

```
picoCTF{L00k5_l1k3_y0u_solv3d_it_ec8a64c7}
```
### Notas Adicionales

### Referencias