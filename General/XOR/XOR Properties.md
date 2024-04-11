# XOR Properties

In the last challenge, you saw how XOR worked at the level of bits. In this one, we're going to cover the properties of the XOR operation and then use them to undo a chain of operations that have encrypted a flag. Gaining an intuition for how this works will help greatly when you come to attacking real cryptosystems later, especially in the block ciphers category.

There are four main properties we should consider when we solve challenges using the XOR operator

```
💡 Commutative: A ⊕ B = B ⊕ A

Associative: A ⊕ (B ⊕ C) = (A ⊕ B) ⊕ C

Identity: A ⊕ 0 = A

Self-Inverse: A ⊕ A = 0

```

Let's break this down. Commutative means that the order of the XOR operations is not important. Associative means that a chain of operations can be carried out without order (we do not need to worry about brackets). The identity is 0, so XOR with 0 "does nothing", and lastly something XOR'd with itself returns zero.

Let's put this into practice! Below is a series of outputs where three random keys have been XOR'd together and with the flag. Use the above properties to undo the encryption in the final line to obtain the flag.

```
💡 KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313

KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e

KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1

FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf

```

Before you XOR these objects, be sure to decode from hex to bytes.

# Solution

```python
>>> KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313
>>> KEY2_KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e

# KEY2 = KEY2_KEY1 ^ KEY1
>>> KEY2 = hex(KEY2_KEY1 ^ KEY1)
>>> print(KEY2)
0x911404e13f94884eabbec925851240a52fa381ddb79700dd6d0d

>>> KEY2_KEY3 = 0xc1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1
# KEY3 = KEY2_KEY3 ^ KEY2
>>> KEY3 = hex(KEY2_KEY3 ^ int(KEY2, 16)) # int(KEY2, 16) because KEY2's type is string
>>> print(KEY3)
0x504053b757eafd3d709d6339b140e03d98b9fe62b84add0332cc

>>> FwK = 0x04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf
# FwK is Flag with Keys (FLAG ^ KEY1 ^ KEY3 ^ KEY2)
>>> Flag = hex(FwK ^ int(KEY2, 16) ^ int(KEY3, 16) ^ KEY1)
>>> print(Flag)
0x63727970746f7b7830725f69355f61737330633161743176337d
>>> print(bytes.fromhex(Flag[2:]))
b'crypto{x0r_i5_ass0c1at1v3}'
```

# Best Solution

```python
from pwn import xor
k1=bytes.fromhex('a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313')
k2_3=bytes.fromhex('c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1')
flag=bytes.fromhex('04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf')
print(xor(k1,k2_3,flag))
```
