# You either know, XOR you don't

I've encrypted the flag with my secret key, you'll never be able to guess it.

Remember the flag format and how it might help you in this challenge!

```
0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104
```

# Solution

Dựa vào hint của đề bài, `Remember the flag format` ta có thể suy ra được 7 kí tự đầu của flag là `crypto{` ⇒ bước đầu tiên ta sẽ XOR message với 7 kí tự đầu đó:

```jsx
from pwn import xor

string = '0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104'
enc_string = bytes.fromhex(string)
flag_format = b"crypto{"

result = xor(enc_string[:7], "crypto{")
print(result)
```

```jsx
b'myXORke'
```

Ta được key là `myXORke` ⇒ Vậy ta dự đoán ký tự tiếp theo là chữ `y` vì sẽ thành từ `myXORkey`. Ta được code hoàn chỉnh như sau: 

```python
from pwn import xor
string = '0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104'
enc_string = bytes.fromhex(string)
flag_format = b"crypto{"
key = "myXORkey"

flag = []
for i in range(len(enc_string)):
  flag.append(xor(enc_string[i], key[i%len(key)]).decode())

# print(flag)
for c in flag:
  print(c, end="")

```

# Best Solution

```python
from pwn import xor
flag = bytes.fromhex('0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104')
print(xor(flag, 'crypto{'.encode())) # oh, it says 'myXORke+y...'
print(xor(flag, 'myXORkey'.encode())) # try this? yay, it works! sometimes simpler is better
```
