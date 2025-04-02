### Descripción
Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Try [here](http://titan.picoctf.net:63324/) to find the flag
### Solución
Una vez que hacemos clic en el enlace mostrado una vez iniciada la instancia del reto, se nos despliega el siguiente sitio web:

![[Pasted image 20250330210131.png]]

Por lo que procedemos a realizar un registro sin sentido, pues ingresamos como nombre completo, nombre de usuario y ciudad la cadena de caracteres **abc** y en el caso del número de teléfono la cadena **12345**, como se aprecia a continuación:

![[Pasted image 20250330210147.png]]

Una vez que le damos al botón de "**Register**", se nos pide un código OTP al ser parte de una verificación de dos pasos:

![[Pasted image 20250330210213.png]]

Al desconocer cual sea ese código, ingresamos **1234**, donde una vez que presionamos el botón "**Submit**", nos aparece el siguiente mensaje:

```
Invalid OTP
```

Por lo que se procede a inspeccionar el sitio web y observar lo que sucede en el tráfico de red, por lo que nos regresamos a la página anterior, abrimos la herramienta de inspector y volvemos a enviar el código OTP inventado: *1234*, por lo que ahora podemos apreciar las solicitudes HTTP generadas con la acción anterior, tal como muestra la siguiente imagen:

![[Pasted image 20250330210338.png]]

Al ser una la que tiene el código 200, se revisa y se procede a editarla para reenviarla otra vez, lo único que nos interesa de momento es lo referente al código OTP, por lo que nos desplazamos hasta donde tengamos algo referente al mismo, encontrándolo en la parte del cuerpo, como se aprecia a continuación:

![[Pasted image 20250330210442.png]]

Por lo que procedemos a borrarlo, puesto que desconocemos cual sea el código verdadero y procedemos a darle en **Enviar**, lo cual nos genera otra solicitud HTTP, donde al revisar la respuesta generada a esta última solicitud, nos encontramos con lo que muestra la siguiente imagen:

![[Pasted image 20250330210519.png]]

Con lo cual hemos obtenido la bandera que da solución al reto actual:

```
picoCTF{#0TP_Bypvss_SuCc3$S_e1eb16ed}
```
### Notas Adicionales

### Referencias