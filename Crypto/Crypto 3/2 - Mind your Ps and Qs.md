### Descripción
In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/bf5e2c8811afb4669f4a6850e097e8aa/values)
### Solución
Iniciamos descargando el archivo que tenemos en la descripción del reto:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_3/mind_your_ps_and_qs]
└─$ wget https://mercury.picoctf.net/static/bf5e2c8811afb4669f4a6850e097e8aa/values    
--2025-05-21 14:27:39--  https://mercury.picoctf.net/static/bf5e2c8811afb4669f4a6850e097e8aa/values
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 205 [application/octet-stream]
Saving to: ‘values’

values                 100%[============================>]     205  --.-KB/s    in 0s      

2025-05-21 14:27:40 (146 MB/s) - ‘values’ saved [205/205]
```

Ahora procedemos a revisar su contenido, teniendo lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_3/mind_your_ps_and_qs]
└─$ cat values            
Decrypt my super sick RSA:
c: 421345306292040663864066688931456845278496274597031632020995583473619804626233684
n: 631371953793368771804570727896887140714495090919073481680274581226742748040342637
e: 65537 
```

Ahora que sabemos lo que contiene, necesitamos de factorizar n para obtener p y q de la siguiente formula para iniciar con la desencriptacion: `n = p * q`

```
input > 631371953793368771804570727896887140714495090919073481680274581226742748040342637

number1 > 1461849912200000206276283741896701133693

number2 > 431899300006243611356963607089521499045809
```

Una vez obtenido lo anterior, nos vamos a python, donde ingresaremos lo siguiente:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_3/mind_your_ps_and_qs]
└─$ python3       
Python 3.13.2 (main, Feb  5 2025, 01:23:35) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> c = 421345306292040663864066688931456845278496274597031632020995583473619804626233684
>>> n = 631371953793368771804570727896887140714495090919073481680274581226742748040342637
>>> e = 65537
>>> p = 1461849912200000206276283741896701133693
>>> q = 431899300006243611356963607089521499045809
>>> tn = (p-1) * (q-1)
>>> tn
631371953793368771804570727896887140714061729769155038068711341335911329840163136
>>> d = pow(e, -1, tn)
>>> m = pow(c, d, n)
>>> m
13016382529449106065927291425342535437996222135352905256639647889241102700065917
>>> bytes.fromhex(hex(m)[2:])
b'picoCTF{sma11_N_n0_g0od_55304594}'
```

Obteniendo así la bandera:

```
picoCTF{sma11_N_n0_g0od_55304594}
```
### Notas Adicionales

### Referencias
http://factordb.com/