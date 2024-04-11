# Base64

Another common encoding scheme is Base64, which allows us to represent binary data as an ASCII string using an alphabet of 64 characters. One character of a Base64 string encodes 6 binary digits (bits), and so 4 characters of Base64 encode three 8-bit bytes.

Base64 is most commonly used online, so binary data such as images can be easily included into HTML or CSS files.

Take the below hex string, *decode* it into bytes and then *encode* it into Base64.

```
72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf
```

💡 In Python, after importing the base64 module with `import base64`, you can use the `base64.b64encode()` function. Remember to decode the hex first as the challenge description states.


# Solution

```python
>>> c = '72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf'
>>> bytes.fromhex(c)
b'r\xbc\xa9\xb6\x8f\xc1j\xc7\xbe\xeb\x8f\x84\x9d\xca\x1d\x8ax>\x8a\xcf\x96y\xbf\x92i\xf7\xbf'
>>> c2 = bytes.fromhex(c)
>>> c3 = base64.b64encode(c2)
>>> print(c3)
b'crypto/Base+64+Encoding+is+Web+Safe/'
```
