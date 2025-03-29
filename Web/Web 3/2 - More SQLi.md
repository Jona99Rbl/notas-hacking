### Descripción
Can you find the flag on this website.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Try to find the flag [here](http://saturn.picoctf.net:55925/).
### Solución
Al hacer clic en el enlace que se nos proporciona después de iniciar la instancia, se nos muestra el siguiente sitio web, donde se nos pide ingresar un usuario y una contraseña.

![[Pasted image 20250328211337.png]]

Se intenta con un usuario y contraseña básica, siendo **admin** en ambos campos. Una vez ingresado esto, se nos despliega lo siguiente:

```sql
username: admin
password: admin
SQL query: SELECT id FROM users WHERE password = 'admin' AND username = 'admin'
```

Lo cual como podemos ver, no nos concedió el acceso al sitio web, debido a que se nos hace mención a una consulta en SQL, se procede a usar una inyección SQL como el caso del ejercicio anterior.

Para este caso se decidió usar la misma inyección del ejercicio anterior como usuario y contraseña: **' or 1=1;**

Una vez hemos colocado en ambos campos la inyección, probamos haciendo clic en el botón de login, lo cual en este caso pudimos acceder ya que nos da la bienvenida y tenemos una tabla con ciudades.

![[Pasted image 20250328215148.png]]

Debido a que se maneja con consultas en SQL, se procede a buscar el línea como se realizan las consultas, por lo que lo primero que requerimos es saber que versión de SQL se está empleando, por lo que usamos la siguiente búsqueda:

```
' union select select sqlite_version(),2,3;
```

Al ejecutarla y como podemos ver en la imagen siguiente tenemos que la versión que se está ejecutando es la 3.31.1, esto nos servirá para ejecutar el comando correcto según se vaya requeriendo.

![[Pasted image 20250328215521.png]]

Es por esto que para observar las tablas que se han creado, se hace uso de la siguiente instrucción:

```
' union select sql,2,3 from sqlite_master;
```

Al insertarla en el buscador, podemos ver las siguientes tablas creadas en esta base de datos, destacando a la que hace mención de la palabra **flag**.

![[Pasted image 20250328215654.png]]

Por lo que se busca la instrucción de como poder consultar los datos de la tabla que en este caso se denomina **more_table**, para lo cual se usa la siguiente instrucción:

```
' union select id,flag,3 from more_table;
```

Al ejecutar la instrucción, obtenemos lo siguiente:

![[Pasted image 20250328215838.png]]

Dándonos así la bandera que da solución a este reto:

```
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_e3e46aae}
```
### Notas Adicionales

### Referencias
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/SQLite%20Injection.md