### Descripción
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.
The website is running [picoCTF News](http://verbal-sleep.picoctf.net:56262/).
### Solución
Iniciamos dando clic sobre el sitio web de las noticias de picoCTF:

![[Pasted image 20250410211348.png]]

Como era el único hashtag al cual se le podía hacer clic y que fuera redirigido, es al de **API Documentation**, ingresamos y a continuación se nos mostrará la siguiente página:

![[Pasted image 20250410211433.png]]

Buscamos el apartado denominado *Diagnosing* y la función **GET**, una vez desplegado, damos clic en "Execute":

![[Pasted image 20250410211633.png]]

Una vez que hacemos lo anterior, se nos muestra la opción de descargar el archivo, cosa que vamos a realizar.

![[Pasted image 20250410211723.png]]

Al descargar el archivo, procedemos a revisarlo con el bloc de notas, donde realizando una búsqueda con "picoCTF", encontramos la bandera que da solución al reto:

```
picoCTF{Pat!3nt_15_Th3_K3y_63fa652c}
```
### Notas Adicionales

### Referencias