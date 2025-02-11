### Descripción
What does this `bDNhcm5fdGgzX3IwcDM1` mean? I think it has something to do with bases.
### Solución
En un primer momento se debió buscar en la red algo para saber como entender el mensaje escrito en la descripción, al mencionar que tenía algo que ver con "bases" se procedió a buscar más sobre el tema, encontrando que es un método de codificación empleado para cifrar datos binarios en texto ASCII, por la composición del mensaje resulta ser uno de **base64**, debido a que emplea 62 caracteres (A-Z, a-z, 0-9) y dos símbolos especiales (+ y /), aunque estos dos últimos no aparecen como tal en la descripción del problema.

Una vez que sabemos eso, procedemos a buscar una herramienta que nos permita hacer la conversión de base64, encontrando una página web llamada **BASE64 Decodificar y Codificar** (https://www.base64decode.org/es/), en donde solo nos resta ingresar el texto codificado para obtener su decodificación como se ve a continuación:

```
Decodifique a partir del formato Base64

Entrada > bDNhcm5fdGgzX3IwcDM1

Conjunto de Caracteres de Origen > UTF-8

Salida > l3arn_th3_r0p35
```

Por lo que una vez realizada esa tarea, obtendremos la siguiente bandera:

```
picoCTF{l3arn_th3_r0p35}
```
### Notas Adicionales

### Referencias
https://www.certsuperior.com/que-significa-base-64/
https://developer.mozilla.org/es/docs/Glossary/Base64
https://www.base64decode.org/es/