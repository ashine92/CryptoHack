# Favorite byte

For the next few challenges, you'll use what you've just learned to solve some more XOR puzzles.

I've hidden some data using XOR with a single byte, but that byte is a secret. Don't forget to decode from hex first.

```
73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d
```

# Solution

```python
>>> string = '73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d'
>>> string_ord = [o for o in bytes.fromhex(string)]
>>> print(string_ord)
[115, 98, 105, 96, 100, 127, 107, 32, 104, 33, 32, 79, 33, 37, 79, 125, 105, 79, 118, 36, 102, 32, 101, 98, 33, 39, 35, 79, 114, 105, 39, 117, 109]

>>> for order in range(256):
...   possible_flag_ord = [order ^ o for o in string_ord]
...   possible_flag = "".join(chr(o) for o in possible_flag_ord)
...   if possible_flag.startswith("crypto"):
...     flag = possible_flag
...     break
...
>>> print(flag)
```
