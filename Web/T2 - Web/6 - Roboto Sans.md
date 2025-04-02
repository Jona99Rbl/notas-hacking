### Descripción
The flag is somewhere on this web application not necessarily on the website. Find it.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
The flag is somewhere on this web application not necessarily on the website. Find it. 
Check [this](http://saturn.picoctf.net:52391/) out.
### Solución
Iniciamos haciendo clic en el enlace que se muestra al iniciar la instancia del desafío, se nos despliega el siguiente sitio web: 

![[Pasted image 20250330233827.png]]

Debido a que le tema nos hace mención de robots y además en el indicio de que la bandera no se encuentra en el sitio web, es entonces que procedemos a usar "**robots.txt**" modificando el enlace de la siguiente manera:

```
http://saturn.picoctf.net:52391/robots.txt
```

Al hacer enter, se nos muestra lo siguiente

```
User-agent *
Disallow: /cgi-bin/
Think you have seen your flag or want to keep looking.

ZmxhZzEudHh0;anMvbXlmaW
anMvbXlmaWxlLnR4dA==
svssshjweuiwl;oiho.bsvdaslejg
Disallow: /wp-admin/
```

Se intuye que los datos se encuentran codificados en base64, debido a que los espacios son rellenados con el símbolo igual (=).

Por lo que usamos una herramienta que nos decodifique el el conjunto de caracteres base64 a caracteres ASCII, es por esto que usamos la página base64decode, ingresando lo siguiente:

```
Input >> anMvbXlmaWxlLnR4dA==

Source character set > UTF-8

Output >> js/myfile.txt
```

Ahora agregamos la salida obtenida al enlace del sitio original, resultando en lo siguiente:

```
http://saturn.picoctf.net:52391/js/myfile.txt
```

Al visitar este enlace resultante, obtenemos la bandera que da solución al reto:

```
picoCTF{Who_D03sN7_L1k5_90B0T5_718c9043}
```
### Notas Adicionales

### Referencias
https://www.base64decode.org/