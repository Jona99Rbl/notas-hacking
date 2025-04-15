### Descripción
BookShelf Pico, my premium online book-reading service.I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
BookShelf Pico, my premium online book-reading service.I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!Here are the credentials to get you started:

- Username: "user"
- Password: "user"

Source code can be downloaded [here](https://artifacts.picoctf.net/c/479/bookshelf-pico.zip).Website can be accessed [here!](http://saturn.picoctf.net:51663/).
### Solución
Después de hacer clic en el enlace de la descripción, nos despliega un sitio como el que se observa en la siguiente imagen:

![[Pasted image 20250412180400.png]]

Como en la descripción nos da el usuario y la contraseña, nos es fácil acceder, por lo que una vez que estamos dentro ingresamos con una cuenta "free", podemos ver tres libros pero el que nos llama la atención es el que dice **Flag**:

![[Pasted image 20250412180458.png]]

Al intentar acceder al libro en cuestión se niega el acceso, por lo que se nos imposibilita ver la bandera para solucionar el reto.

Usando la herramienta de inspección, analizamos el apartado de red, encontrando un archivo raíz, donde después de leer todo el contenido, encontramos un apartado llamado Autorización donde encontramos un jwt, como se muestra a continuación:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJyb2xlIjoiRnJlZSIsImlzcyI6ImJvb2tzaGVsZiIsImV4cCI6MTc0NTEwNzY0OSwiaWF0IjoxNzQ0NTAyODQ5LCJ1c2VySWQiOjEsImVtYWlsIjoidXNlciJ9.FdYi70u8yO_BqOsO-wddYH7ab3sFQwvZs9bubQUut9M
```

Por lo que recurrimos a una herramienta como **jwt.io** para que nos ayude a modificar ese token, donde antes de moverle, descargamos el archivo que viene anexo.

Una vez descargado procedemos a revisarlo, en dicho archivo descargado es un conjunto de archivos en java, por lo que nos ponemos a revisarlos e ir determinando lo que se requiere para modificar nuestra cookie y así hacernos pasar por el administrador:

Cuando ya hemos obtenido todo lo que nos hacia falta, se modifica la cookie, quedando en lo siguiente:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJyb2xlIjoiQWRtaW4iLCJpc3MiOiJib29rc2hlbGYiLCJleHAiOjE3NDUxMDc2NDksImlhdCI6MTc0NDUwMjg0OSwidXNlcklkIjoyLCJlbWFpbCI6ImFkbWluIn0.6KbQIam4dWvbNmSChhi-MX0JxfLDN7AKD0OpsOq9WXM
```

Por lo que a través de la herramienta de inspección, cambiamos el valor de la cookie además de otras características que se requieren, recargamos la página web y obtenemos lo siguiente:

![[Pasted image 20250412182045.png]]

Gracias a todo lo realizado anteriormente tenemos la bandera que da solución al reto:

```
picoCTF{w34k_jwt_n0t_g00d_d7c2e335}
```
### Notas Adicionales

### Referencias
https://jwt.io/