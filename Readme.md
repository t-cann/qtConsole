# Embedding Python in C++/QT app Examples

## List of Examples

Embedding Python in C with Python C API

Python2 Examples
- Shout Filter Example (Broken)

Python3 Examples
- pyrun_simplestring
- pyrun_anyfile
- arguements_example
- extendingEmbeddedPython

## List of Other Useful Git Repositories

- pythonqt [https://mevislab.github.io/pythonqt]
- QtConsole
- Examples_Qt [https://github.com/gammasoft71/Examples_Qt.git]
- numpy-c-api Examples [https://github.com/AlexanderFabisch/numpy-c-api]

Binding and Wrapping 
- SWIG
- PyBind
- Boost

## Compiler Flags / Where to find them
In VSCode Changes to default C/C++ Configuration 
- Include Path of Python.h Header file "/usr/include/python3.8/**"

> python3.8-config --cflags

```
-I/usr/include/python3.8 -I/usr/include/python3.8  -Wno-unused-result -Wsign-compare -g -fdebug-prefix-map=/build/python3.8-fKk4GY/python3.8-3.8.2=. -specs=/usr/share/dpkg/no-pie-compile.specs -fstack-protector -Wformat -Werror=format-security  -DNDEBUG -g -fwrapv -O3 -Wall 
```

> python3.8-config --cflags
```
-L/usr/lib/python3.8/config-3.8-x86_64-linux-gnu -L/usr/lib  -lcrypt -lpthread -ldl  -lutil -lm -lm  
```

### If compiling with gcc:

- link standard library to use std `-lstdlb`

## Issues is Module Search Path

If module is not in the system modules, there are not found by default. Either add reequired directory to`PYTHONPATH`enviroment variable. 

or
```Python
import os
import sys
sys.path.append(os.getcwd())
```