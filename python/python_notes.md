# Python Notes #
[Standard Python Library](https://docs.python.org/3/library/index.html") - Try learning as much as you can from this. Implement whatever is useful. 
Python Modules to learn: 
    - File handling, data handling and path related: 
          1. [sys](https://docs.python.org/3/library/sys.html)
          2. [os](https://docs.python.org/3/library/os.html)
          3. [json](https://docs.python.org/3/library/json.html#module-json)
          4. [file](https://docs.python.org/3/library/filesys.html)
          5. [pickle](https://docs.python.org/3/library/pickle.html#module-pickle)
          6. [shelve](https://docs.python.org/3/library/shelve.html#module-shelve)
          7. [marshal](https://docs.python.org/3/library/marshal.html#module-marshal)
          8. [io](https://docs.python.org/3/library/io.html#module-io)
          9. [glob for pathname pattern expression](https://docs.python.org/3/library/glob.html)
          10. [csv module for csv files](https://docs.python.org/3/library/csv.html)
          11. [tabulate](https://pypi.org/project/tabulate/)
          12. 
    - Command Line Tools:
          1.  [argparse](https://docs.python.org/3/library/argparse.html)
          2.  [PythonFire from Google](https://github.com/google/python-fire)
          3.  [Subprocess](https://docs.python.org/3/library/subprocess.html)
          4.  [Typer](https://typer.tiangolo.com/)
          5.  [Command Line Tools - List in Github](https://github.com/shadawck/awesome-cli-frameworks?tab=readme-ov-file)
    - Python Important Modules: 
          1. [Builtin Exceptions](https://docs.python.org/3/library/exceptions.html#bltin-exceptions)
          2. [typing](https://docs.python.org/3/library/typing.html) for Type checking
          3. [types module in python](https://docs.python.org/3/library/types.html)
          4. [logging](https://docs.python.org/3/howto/logging.html)
          5. [Collections module in Python](https://docs.python.org/3/library/collections.html)
          6. [re module for regex](https://docs.python.org/3/library/re.html)
          7. [enum for Enum types](https://docs.python.org/3/library/enum.html)
          8. from __future__ import annotations
          9. [Python Runtime Services](https://docs.python.org/3/library/python.html)
    - Http Operations:
          1. [For all Network Operations](https://docs.python.org/3/library/ipc.html)
          2. [For Internet related Operations](https://docs.python.org/3/library/internet.html)
          3. [Structured Markup Processing Tools](https://docs.python.org/3/library/markup.html)
          4. 
    - [Concurrent Operations](https://docs.python.org/3/library/concurrency.html)
    -  
1.  
2.  urllib
3.  concurrent
4.  
5.  

- `*` is the list or tuple unpacking operator. 
- `**` is the dictionary unpacking operator. 
- Python supports an else clause in for and while loops. The else body is executed only if no break is encountered during the execution of the associated loop body. In one of the scenarios where this can be quite useful is when you are searching for a particular value in the loop and the value is not found.
  
## Strings ##
- String concatenation.
- Strings can be indexed.
- Strings also support slicing.
- Strings are immutable. 
- builtin function -> len(stringVar) - outputs the length of the string. 
- Strings are examples of sequence types. Strings are immutable sequences of unicode code points. 
- Strings support single, double and triple quotes. 
- r or raw prefix disables most escape sequence processing. 
- Strings can be created from other objects using the str constructor. 
- StringPrefixes: 
    - Bytes literals: prefixed with 'b' or 'B' - They produce an instance of bytes type instead of str type. 
    - Raw literals: prefixed with 'r' or 'R' - Raw strings treat backslashes as literal characters. 
    - Formatted string literal: prefixed with 'f' or 'F' - formatted string literal - 'f' may be combined with 'r' but not with 'b' or 'u'. 

### Formatted String Literals ###
These strings may contain replacement fields, which are expressions delimited by curly braces `{}`. 
Formatted string literals are really expressions evaluated at run time.
% - This is the string interpolation operator. 
1. Using the formatted string literal - %
```python
"Hello %s, this is your age %f" % ("bajjulu", 25)
```
2. str.format() method for string interpolation.
```python
"Hello {}! this is your {}".format("Bajjulu", 25)
"Hello {1}! this is your {0}.format(30, "Bajjulu")
"Hello {name}! this is your {age}.format(name="Bajjulu", age=30)
person = {"name": "Bajjulu", "age": 30}
"Hello {name}! this is your {age}".format(**person)
```

## Lists ##
Sequence types

## Tuples ##
List and strings are sequence data types. Tuple is another standard sequence data type.
> A tuple consists of a number of values separated by commas. 

Tuples are immutable. Output tuples are always enclosed in parentheses. 
It is possible to create tuples containing mutable objects such as lists and strings. 
Tuples are immutable and often contain heterogeneous sequence of elements that are accessed via unpacking or indexing. 
Lists are mutable and often usually contain homogeneous elements and are accessed by iterating over the list.

 Empty tuples are constructed by an empty pair of parentheses; a tuple with one item is constructed by following a value with a comma:
 ```python
empty = ()
singleton = 'hello',    # <-- note trailing comma
len(empty)
>>> 0
len(singleton)
>>> 1
singleton
('hello',)
```
Tuple packing and tuple unpacking. 

## Sets ##
A collection of unordered elements with no duplicate values. Basic uses include membership testing and eliminating duplicate entries. 
Curly braces or the set() function can be used to create sets.
To create an empty set use set(), not {}; the latter creates an empty dictionary.
Set operations can be conducted on words using set() operation. 

## Dictionaries ##
Dictionaries are sometimes found in other languages as “associative memories” or “associative arrays”. Unlike sequences, which are indexed by a range of numbers, dictionaries are indexed by keys, which can be any immutable type; strings and numbers can always be keys. Tuples can be used as keys if they contain only strings, numbers, or tuples; if a tuple contains any mutable object either directly or indirectly, it cannot be used as a key. You can’t use lists as keys, since lists can be modified in place using index assignments, slice assignments, or methods like append() and extend().
- Performing list(d) on a dictionary returns a list of all the keys used in the dictionary, in insertion order (if you want it sorted, just use sorted(d) instead).
- To check whether a single key is in the dictionary, use the in keyword.
- The dict() constructor builds dictionaries directly from sequences of key-value pairs:
```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```
- Dict comprehensions can be used to create dictionaries from arbitrary key and value expressions:
```python
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
```
- When looping through a sequence, the position index and corresponding value can be retrieved at the same time using the enumerate() function.
```python
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...
...    print(i, v)
0 tic
1 tac
2 toe
```
## zip() ##
Creates a tuple of values from sequence objects. 

## Executing modules as scripts ##
```python
if __name__ == "__main__":
    import sys
    function_name(int(sys.argv[1]))
```

### dir() function ###
It gives a list of names defined in a module. It returns a sorted list of strings. Names means: variables, modules, functions etc. 
Given below is a list of builtins in python. 
```python
['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
 'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
 'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
 'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
 'NotImplementedError', 'OSError', 'OverflowError',
 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
 'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
 'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
 'ValueError', 'Warning', 'ZeroDivisionError', '_', '__build_class__',
 '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs',
 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
 'zip']
```

### __init__.py files ###
The __init__.py files are required to make Python treat directories containing the file as packages (unless using a namespace package, a relatively advanced feature). This prevents directories with a common name, such as string , from unintentionally hiding valid modules that occur later on the module search path. __init__.py can just be an empty file, but it can also execute initialization code for the package or set the __all__ variable. 
```python 
__all__ = ["file1", "file2", "file3"] 
```
- Submodules might become shadowed by locally defined names. 
- If __all__ is not defined, the statement `from sound.effects import *` does not import all submodules from the package sound.effects into the current namespace; it only ensures that the package `sound.effects` has been imported (possibly running any initialization code in __init__.py) and then imports whatever names are defined in the package.
- The name of the main module is always `__main__`. Modules intended to be used as the main module of a python application must always use absolute imports. 

##  Reading and Writing Files ##
```
Functions discussed: 
1. open()
2. with open() as f: 
3. try-finally
4. f.read()
5. f.readline()
6. f.readlines()
7. f.tell()
8. f.seek(offset, whence)
9. f.write()
10. f.append()
```

open() returns a file object, and is most commonly used with two positional arguments and one keyword argument: `open(filename, mode, encoding=None)`
`f = open('workfile', 'w', encoding="utf-8")`
-  Appending a 'b' to the mode opens the file in binary mode. Binary mode data is read and written as bytes objects. You can not specify encoding when opening file in binary mode.
-  It is good practice to use the with keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. Using with is also much shorter than writing equivalent try-finally blocks:
```python
>>> with open('workfile', encoding="utf-8") as f:
...    read_data = f.read()
>>> # We can check that the file has been automatically closed.
>>> f.closed
True
```
- If the end of the file has been reached, f.read() will return an empty string ('').
- f.readline() reads a single line from the file; a newline character (\n) is left at the end of the string, and is only omitted on the last line of the file if the file doesn’t end in a newline. This makes the return value unambiguous; if f.readline() returns an empty string, the end of the file has been reached, while a blank line is represented by '\n', a string containing only a single newline.
- For reading lines from a file, you can loop over the file object. This is memory efficient, fast, and leads to simple code:
```python
for line in f:
    print(line, end='')
# This is the first line of the file.
# Second line of the file
```
- If you want to read all the lines of a file in a list you can also use list(f) or f.readlines().
- f.write(string) writes the contents of string to the file, returning the number of characters written.
> Note: Other types of objects need to be converted – either to a string (in text mode) or a bytes object (in binary mode) – before writing them. It could be tuple, dict or a list, any other object. 
- f.tell() returns an integer giving the file object’s current position in the file represented as number of bytes from the beginning of the file when in binary mode and an opaque number when in text mode.
- To change the file object’s position, use f.seek(offset, whence). The position is computed from adding offset to a reference point; the reference point is selected by the whence argument. A whence value of 0 measures from the beginning of the file, 1 uses the current file position, and 2 uses the end of the file as the reference point. whence can be omitted and defaults to 0, using the beginning of the file as the reference point.

## Saving structured data with json ##
 - The standard module called `json` can take Python data hierarchies, and convert them to string representations; this process is called **serializing**. 
 - Reconstructing the data from the string representation is called **deserializing**. 
 - Between serializing and deserializing, the string representing the object may have been stored in a file or data, or sent over a network connection to some distant machine.

## Exceptions ##
There are atleast two different types of errors in Python: Syntax errors or Exceptions.
- Syntax errors - also called as parsing errors. 
- Exceptions: Errors caused during the execution are called exceptions. They are not unconditionally fatal. 
Standard exceptions names are built-in identifiers (not reserved keywords). 
- try-except-finally clauses in Python.
    - If an exception occurs which does not match the exception named in the except clause, it is passed on to outer try statements; if no handler is found, it is an unhandled exception and execution stops with an error message.
    - Exception can be used as a wildcard that catches (almost) everything. However, it is good practice to be as specific as possible with the types of exceptions that we intend to handle, and to allow any unexpected exceptions to propagate on.
- A try statement may have more than one except clause, to specify handlers for different exceptions. At most one handler will be executed. Handlers only handle exceptions that occur in the corresponding try clause, not in other handlers of the same try statement. An except clause may name multiple exceptions as a parenthesized tuple.
- A class in an except clause matches exceptions which are instances of the class itself or of its derived classes, but not the other way around.   
- When an exception occurs, it may have associated values, also known as the exception’s arguments. The presence and types of the arguments depend on the exception type.
  - The exception’s `__str__()` output is printed as the last part (‘detail’) of the message for unhandled exceptions.

### Exceptions classes in Python ###
- BaseException is the common base class of all exceptions. 
- One of its subclasses, Exception, is the base class of all the non-fatal exceptions. Exceptions which are not subclasses of Exception are not typically handled, because they are used to indicate that the program should terminate. They include SystemExit which is raised by sys.exit() and KeyboardInterrupt which is raised when a user wishes to interrupt the program.
```python
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```
- The raise statement allows the programmer to force a specified exception to occur.
- The sole argument to raise indicates the exception to be raised. This must be either an exception instance or an exception class.
- To indicate that an exception is a direct consequence of another, the raise statement allows an optional from clause.
```python
raise RuntimeError from exc
```
### User defined exceptions ###
- Exceptions should typically be derived from the Exception class, either directly or indirectly.
- If a finally clause is present, the finally clause will execute as the last task before the try statement completes. The finally clause runs whether or not the try statement produces an exception.
- Three attributes about the exception objects provide information about the context in which the exception was raised: 
  -  BaseException.__context__
  -  BaseException.__cause__
  -  BaseException.__suppress_context__

## Classes ##
Classes provide a means to bundle data and functionality together. 
- Attributes maintain the state of the class instance. 
- Class instances have methods for modifying its state. 
Object Oriented Programming in Python: 
1. The class inheritance mechanism allows for multiple base classes. 
2. A derived class can override any methods of its base classes or classes. 
3. A method can call a method of the base class with the same name. 
4. Classes are created at runtime and can be modified further after creation. 
5. Builtin types can be used as base classes for extension by the user. 
6. Aliasing in classes: Objects have individuality and multiple names (in multiple scopes) can be bound to the same object. Aliases behave like pointers in some respects. 

### Namespaces and Scopes ###
A namespace is a mapping from names to objects. Most namespaces are currently implemented as Python dictionaries. The set of attributes of an object also form a namespace. 
- There is absolutely no relation between names in different namespaces. 
- A module's attributes' and the global names defined in the module share the same namespace. 
- Namespaces are created at different moments and have different lifetimes. The namespace containing the builtin names is created when the python interpreter starts and is never deleted. 
- The global namespace for a module is created when the module is created when the module definition is read in. Normally module namespaces also last until the interpreter quits. 
-  The statements executed by the top-level invocation of the interpreter, either read from a script file or interactively, are considered part of a module called __main__, so they have their own global namespace.
-  The local namespace for a function is created when the function is called, and deleted when the function returns or raises an exception that is not handled within the function. Recursive invocations each have their own local namespace.

Scope
: A scope is a textual region of a python program where a namespace is directly accessible.  
- What does it mean to be "directly accessible"? - *It means that an unqualified reference to a name attemtps to find the name in the namespace*.
> Scopes are determined statically but are used dynamically. At anytime during execution there are three or four scopes whose namespaces are directly accessible: 
   - The innermost scope that conatains the local names. This scope is searched first.      
   - The scopes of any enclosing functions, which are searched starting with the nearest enclosing scope, contain non-local, but also non-global names.
   - The next-to-last scope contains the current module’s global names.
   - The outermost scope (searched last) is the namespace containing built-in names.  

