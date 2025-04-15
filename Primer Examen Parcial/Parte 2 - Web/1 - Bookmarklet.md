### Descripción
Why search for the flag when I can make a bookmarklet to print it for me?

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Why search for the flag when I can make a bookmarklet to print it for me?
Browse [here](http://titan.picoctf.net:55266/), and find the flag!
### Solución
Iniciamos haciendo clic en el enlace proporcionado por la descripción después de iniciar la instancia del desafío, donde encontramos la siguiente página web:

![[Pasted image 20250410203525.png]]

El código javascript proporcionado por la página es el siguiente:

```js
        javascript:(function() {
            var encryptedFlag = "àÒÆÞ¦È¬ëÙ£ÖÓÚåÛÑ¢ÕÓ¡ÒÅ¤í";
            var key = "picoctf";
            var decryptedFlag = "";
            for (var i = 0; i < encryptedFlag.length; i++) {
                decryptedFlag += String.fromCharCode((encryptedFlag.charCodeAt(i) - key.charCodeAt(i % key.length) + 256) % 256);
            }
            alert(decryptedFlag);
        })();
    
```

Por lo que procedemos a copiarlo y pegarlo en la consola de la herramienta de inspección del sitio web:

![[Pasted image 20250410204026.png]]

Una vez hemos ejecutado el código de javascript desde la consola, se nos desplegará una ventana emergente con la bandera que da solución a este reto:

```
picoCTF{p@g3_turn3r_0148cb05}
```
### Notas Adicionales

### Referencias