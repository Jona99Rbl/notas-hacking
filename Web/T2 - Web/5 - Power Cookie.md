### Descripción
Can you get the flag?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Can you get the flag? 
Go to this [website](http://saturn.picoctf.net:59293/) and see what you can discover.
### Solución
Una vez otorgado el enlace para visitar después de que se haya iniciado la instancia del reto, al hacer clic, se nos muestra el siguiente sitio web:

![[Pasted image 20250330221613.png]]

Sin otra opción más que darle clic al botón "**Continue as guest**", procedemos a hacerlo, enseguida se nos muestra el siguiente mensaje:

```
We apologize, but we have no guest services at the moment.
```

Como el titulo del reto involucra cookies, procedemos a buscarlas a través de la herramienta de inspección del navegador, por lo que una vez localizada encontramos solo una, la cual se denomina como "**isAdmin**", la cual tiene el valor de 0, como se muestra en la siguiente imagen:

![[Pasted image 20250330222625.png]]

Por lo que pasamos a editar el valor, haciéndolo 1, como se ve a continuación:

![[Pasted image 20250330222659.png]]

Una vez guardado ese valor, se procede a recargar la página nuevamente, mostrandonos así la bandera que da solución al reto:

```
picoCTF{gr4d3_A_c00k13_0d351e23}
```
### Notas Adicionales

### Referencias