### Descripción
Help us test the form by submiting the username as `test` and password as `test!`

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Help us test the form by submiting the username as `test` and password as `test!`The website running [here](http://saturn.picoctf.net:59808/).
### Solución
Iniciamos visitando el sitio web haciendo clic en el enlace proporcionado en la descripción del reto, teniendo lo que vemos a continuación:

![[Pasted image 20250412172751.png]]

Entonces abrimos la herramienta Burp y ponemos a funcionar el proxy para atrapar los encabezados HTML, de ahí se destacan un GET y un POST, en el caso del GET tenemos que:

```html
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/html; charset=utf-8
Content-Length: 264
ETag: W/"108-/7O7VTeecocneZ8ZrGW1rxPrD4s"
Date: Sat, 12 Apr 2025 23:22:12 GMT
Connection: keep-alive
Keep-Alive: timeout=5

<!DOCTYPE html>
<head>
    <title>flag</title>
</head>
<body>
    <script>
        setTimeout(function () {
           // after 2 seconds
           window.location = "/next-page/id=bF90aGVfd2F5XzAxZTc0OGRifQ==";
        }, 0.5)
      </script>
    <p></p>
</body>
```

Y en el caso del POST, tenemos lo siguiente:

```html
HTTP/1.1 302 Found
X-Powered-By: Express
Location: /next-page/id=cGljb0NURntwcm94aWVzX2Fs
Vary: Accept
Content-Type: text/html; charset=utf-8
Content-Length: 120
Date: Sat, 12 Apr 2025 23:22:11 GMT
Connection: keep-alive
Keep-Alive: timeout=5

<p>Found. Redirecting to <a href="/next-page/id=cGljb0NURntwcm94aWVzX2Fs">/next-page/id=cGljb0NURntwcm94aWVzX2Fs</a></p>
```

Por lo que se puede ver, estas dos códigos contienen en el apartado de id una cadena codificada en base64, procedemos a juntar las dos partes y usar el comando echo para hacer la conversión en la consola:

```shell
jony@DESKTOP-TN1UVD2:~$ echo "cGljb0NURntwcm94aWVzX2FsbF90aGVfd2F5XzAxZTc0OGRifQ==" | base64 -d
picoCTF{proxies_all_the_way_01e748db}
```

Dándonos así la bandera que da solución a este reto:

```
picoCTF{proxies_all_the_way_01e748db}
```
### Notas Adicionales

### Referencias