### Descripción
Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?
You can access the Cookie Monster [here](http://verbal-sleep.picoctf.net:64848/) and good luck
### Solución
Iniciamos dando clic en la liga del sitio que se nos anexa en la descripción del reto, donde se nos muestra el siguiente sitio web:

![[Pasted image 20250410204453.png]]

Se inicia ingresando como usuario y contraseña la palabra "admin":

![[Pasted image 20250410210341.png]]

Al darle Login, nos salta el siguiente mensaje de acceso denegado:

![[Pasted image 20250410210428.png]]

Usando Cookie-Editor, obtenemos el valor de la cookie, el cual es: `cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzc3MUQ1RUIwfQ%3D%3D` aparentando estar codificada en base64.

Por lo que ahora solo hacemos uso de una terminal con Ubuntu para obtener su decodificación con el comando echo:

```shell
jony@DESKTOP-TN1UVD2:~$ echo -n "cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzc3MUQ1RUIwfQ%3D%3D" | base64 -d
picoCTF{c00k1e_m0nster_l0ves_c00kies_771D5EB0}base64: invalid input
```

Después de aplicar dicho comando obtenemos la bandera que da solución al reto:

```
picoCTF{c00k1e_m0nster_l0ves_c00kies_771D5EB0}
```
### Notas Adicionales

### Referencias