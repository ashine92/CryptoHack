# Encoding Challenge

Now you've got the hang of the various encodings you'll be encountering, let's have a look at automating it.

Can you pass all 100 levels to get the flag?

The *[13377.py](http://13377.py)* file attached below is the source code for what's running on the server. The *pwntools_example.py* file provides the start of a solution using the incredibly convenient pwntools library. which we recommend. If you'd prefer to use Python's in-built telnetlib, *telnetlib_example.py* is also provided.

For more information about connecting to interactive challenges, see the [FAQ](https://cryptohack.org/faq#netcat). Feel free to skip ahead to the cryptography if you aren't in the mood for a coding challenge!

Connect at `nc socket.cryptohack.org 13377`

**Challenge files:**

[13377.py](https://cryptohack.org/static/challenges/13377_43de0a0efed6ed7bd890d1c79db22fb1.py)

[pwntools_example.py](https://cryptohack.org/static/challenges/pwntools_example_f93ca6ccef2def755aa8f6d9aa6e9c5b.py)

[telnetlib_example.py](https://cryptohack.org/static/challenges/telnetlib_example_5b11a835055df17c7c8f8f2a08782c44.py)

# Solution

```python
from pwn import * # pip install pwntools
import json
from Crypto.Util.number import *
import base64
import codecs

r = remote('socket.cryptohack.org', 13377, level = 'debug')

def json_recv():
    line = r.recvline()
    return json.loads(line.decode())

def json_send(hsh):
    request = json.dumps(hsh).encode()
    r.sendline(request)

def decode(encoded):
    if encoded["type"] == "base64":
      decoded = base64.b64decode(encoded["encoded"])
    elif encoded["type"] == "hex":
      decoded = bytes.fromhex(encoded["encoded"])
    elif encoded["type"] == "rot13":
      decoded = codecs.decode(encoded["encoded"], "rot-13")
      return decoded
    elif encoded["type"] == "utf-8":
      decoded = ""
      for b in encoded["encoded"]:
        decoded += chr(b)
      return decoded
    elif encoded["type"] == "bigint":
      decoded = bytes.fromhex(encoded["encoded"][2:])
    print(decoded)
    return decoded.decode()

for i in range(101):
    received = json_recv()
    print(received)
    print("Received type: ")
    print(received["type"])
    print("Received encoded value: ")
    print(received["encoded"])
    print(type(received["encoded"]))
    decode_msg = decode(received)
    to_send = {
        "type": received["type"],
        "decoded": decode_msg
    }
    json_send(to_send)
```
