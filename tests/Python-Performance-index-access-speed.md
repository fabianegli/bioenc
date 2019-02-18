# Performance tests

MacOSX 10.11, Python 3.6.3, 2.8 GHz Intel Core i7 and 16 GB 1600 MHz DDR3

```
>>> import timeit
>>> import string
>>> import random
>>> import encodings

>>> utf8_chars  = string.printable+"💡🎁💥"
>>> ascii_chars = string.ascii_uppercase

>>> utf8_list  = random.choices(utf8_chars,  k=10**8)
>>> ascii_list = random.choices(ascii_chars, k=10**8)
>>> utf8_str  = ''.join(utf8_list)
>>> ascii_str = ''.join(ascii_list).encode("ascii")
>>> print(type(utf8_str))
<class 'str'>
>>> print(type(ascii_str))
<class 'bytes'>

>>> print('utf8_list, first char:', timeit.timeit(stmt='utf8_list[10**0]', setup='pass', number=10000000, globals={"utf8_list":utf8_list}))
utf8_list, first char: 0.5652291839942336
>>> print('utf8_list, 10^7th char:', timeit.timeit(stmt='utf8_list[10**7]', setup='pass', number=10000000, globals={"utf8_list":utf8_list}))
utf8_list, 10^7th char: 0.573600659990916
>>> print('ascii_list, first char:', timeit.timeit(stmt='ascii_list[10**0]', setup='pass', number=10000000, globals={"ascii_list":ascii_list}))
ascii_list, first char: 0.5194989800220355
>>> print('ascii_list, 10^7th char:', timeit.timeit(stmt='ascii_list[10**7]', setup='pass', number=10000000, globals={"ascii_list":ascii_list}))
ascii_list, 10^7th char: 0.5641870909894351

>>> print('utf8_str, first char:', timeit.timeit(stmt='utf8_str[10**0]', setup='pass', number=10000000, globals={"utf8_str":utf8_list}))
utf8_str, first char: 0.543945995013928
>>> print('utf8_str, 10^7th char:', timeit.timeit(stmt='utf8_str[10**7]', setup='pass', number=10000000, globals={"utf8_str":utf8_list}))
utf8_str, 10^7th char: 0.55816443299409
>>> print('ascii_str, first char:', timeit.timeit(stmt='ascii_str[10**7]', setup='pass', number=10000000, globals={"ascii_str":ascii_str}))
ascii_str, first char: 0.6180030570249073
>>> print('ascii_str, 10^7th char:', timeit.timeit(stmt='ascii_str[10**7]', setup='pass', number=10000000, globals={"ascii_str":ascii_str}))
ascii_str, 10^7th char: 0.5772341519768815
```
