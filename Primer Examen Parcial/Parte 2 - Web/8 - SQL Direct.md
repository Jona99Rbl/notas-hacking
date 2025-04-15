### Descripción
Connect to this PostgreSQL server and find the flag!

Additional details will be available after launching your challenge instance.
#### Una vez iniciada la instancia del desafío:
Connect to this PostgreSQL server and find the flag!`psql -h saturn.picoctf.net -p 62697 -U postgres pico`Password is `postgres`
### Solución
Iniciamos estableciendo conexión con el servidor que nos proporciona el reto en la descripción una vez iniciada la instancia del desafío, donde tenemos que ingresar la contraseña proporcionada en la misma descripción:

```shell
┌──(kali㉿kali)-[~]
└─$ psql -h saturn.picoctf.net -p 62697 -U postgres pico
Password for user postgres: 
psql (17.4 (Debian 17.4-1), server 15.2 (Debian 15.2-1.pgdg110+1))
Type "help" for help.
```

Debido a que nos sugiere escribir **help** para saber como operar dentro del servidor procedemos a hacerlo:

```shell
pico-# help
Use \? for help or press control-C to clear the input buffer.
pico-# \?
```

Ejecutado el comando se nos despliega el siguiente manual de operación:

```
General
  \bind [PARAM]...       set query parameters
  \copyright             show PostgreSQL usage and distribution terms
  \crosstabview [COLUMNS] execute query and display result in crosstab
  \errverbose            show most recent error message at maximum verbosity
  \g [(OPTIONS)] [FILE]  execute query (and send result to file or |pipe);
                         \g with no arguments is equivalent to a semicolon
  \gdesc                 describe result of query, without executing it
  \gexec                 execute query, then execute each value in its result
  \gset [PREFIX]         execute query and store result in psql variables
  \gx [(OPTIONS)] [FILE] as \g, but forces expanded output mode
  \q                     quit psql
  \watch [[i=]SEC] [c=N] [m=MIN]
                         execute query every SEC seconds, up to N times,
                         stop if less than MIN rows are returned

Help
  \? [commands]          show help on backslash commands
  \? options             show help on psql command-line options
  \? variables           show help on special variables
  \h [NAME]              help on syntax of SQL commands, * for all commands

Query Buffer
  \e [FILE] [LINE]       edit the query buffer (or file) with external editor
  \ef [FUNCNAME [LINE]]  edit function definition with external editor
  \ev [VIEWNAME [LINE]]  edit view definition with external editor
  \p                     show the contents of the query buffer
  \r                     reset (clear) the query buffer
  \s [FILE]              display history or save it to file
  \w FILE                write query buffer to file

Input/Output
  \copy ...              perform SQL COPY with data stream to the client host
  \echo [-n] [STRING]    write string to standard output (-n for no newline)
  \i FILE                execute commands from file
  \ir FILE               as \i, but relative to location of current script
  \o [FILE]              send all query results to file or |pipe
  \qecho [-n] [STRING]   write string to \o output stream (-n for no newline)
  \warn [-n] [STRING]    write string to standard error (-n for no newline)

Conditional
  \if EXPR               begin conditional block
  \elif EXPR             alternative within current conditional block
  \else                  final alternative within current conditional block
  \endif                 end conditional block

Informational
  (options: S = show system objects, + = additional detail)
  \d[S+]                 list tables, views, and sequences
  \d[S+]  NAME           describe table, view, sequence, or index
  \da[S]  [PATTERN]      list aggregates
  \dA[+]  [PATTERN]      list access methods
  \dAc[+] [AMPTRN [TYPEPTRN]]  list operator classes
  \dAf[+] [AMPTRN [TYPEPTRN]]  list operator families
  \dAo[+] [AMPTRN [OPFPTRN]]   list operators of operator families
```

Por lo que una vez leído procedemos a consultar la lista de tablas, vistas y secuencias usando el comando "**\d**", como se ve a continuación:

```shell
pico-# \d
         List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | flags | table | postgres
(1 row)
```

Ahora que sabemos que hay una relación denominada como "flags", por lo que ahora procederemos a jalar esa información a través de una consulta SQL:

```shell
pico=# select * from flags;
 id | firstname | lastname  |                address                 
----+-----------+-----------+----------------------------------------
  1 | Luke      | Skywalker | picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
  2 | Leia      | Organa    | Alderaan
  3 | Han       | Solo      | Corellia
(3 rows)
```

Como podemos ver en la tabla tenemos la bandera que da solución al reto actual:

```
picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
```
### Notas Adicionales

### Referencias