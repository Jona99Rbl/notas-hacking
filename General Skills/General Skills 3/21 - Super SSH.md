### Descripción
Using a Secure Shell (SSH) is going to be pretty important.

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Can you `ssh` as `ctf-player` to `titan.picoctf.net` at port `59749` to get the flag?You'll also need the password `6abf4a82`. If asked, accept the fingerprint with `yes`.If your device doesn't have a shell, you can use: [https://webshell.picoctf.org](https://webshell.picoctf.org/)If you're not sure what a shell is, check out our Primer: [https://primer.picoctf.com/#_the_shell](https://primer.picoctf.com/#_the_shell)

### Solución
Al lanzar la instancia del desafío, nos indica la forma de como conectarnos a SSH, lo cual se realiza con el comando **ssh** seguido del usuario y el servidor, por ultimo el puerto a traves del cual nos conectaremos, una vez establecida la conexión, ingresamos la contraseña proporcionada por la descripción del reto, como podemos ver a continuación:

```shell
the_robx-picoctf@webshell:~$ ssh ctf-player@titan.picoctf.net -p 59749
The authenticity of host '[titan.picoctf.net]:59749 ([3.139.174.234]:59749)' can't be established.
ED25519 key fingerprint is SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[titan.picoctf.net]:59749' (ED25519) to the list of known hosts.
ctf-player@titan.picoctf.net's password:  
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_65a7a106}
Connection to titan.picoctf.net closed.
```

Una vez que hemos escrito correctamente la contraseña, nos arroja la bandera que soluciona este reto:

```
picoCTF{s3cur3_c0nn3ct10n_65a7a106}
```
### Notas Adicionales

### Referencias
https://linux.die.net/man/1/ssh