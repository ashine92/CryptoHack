# Extended GCD

Giả sử a và b là các số nguyên dương.

Thuật toán euclid mở rộng là một cách hiệu quả để tìm các số nguyên u, v sao cho:

**a × u + b × v = gcd(a, b)**

Về sau, khi bạn học cách giải mã văn bản rsa, bạn sẽ cần thuật toán này để tính nghịch đảo modulo của số mũ công khai.

Với hai số nguyên:

**p = 26513**
**q = 32321**

Hãy tìm các số nguyên u, v sao cho:

**p × u + q × v = gcd(p, q)**

Hãy nhập số nhỏ hơn trong hai số u và v làm "flag".

# Solution

## Giải thích chi tiết về thuật toán Euclid mở rộng
### 1. Mục tiêu của thuật toán
Thuật toán Euclid mở rộng giúp tìm các số nguyên x và y sao cho:
a.x + b.y = gcd(a,b)
Đây là đồng nhất thức Bézout.
VD: a = 26513, b = 32321
Ta sẽ tìm x, y sao cho: 26513x + 32321y = 1

- Euclid thường: chỉ tìm gcd(a, b)
- Euclid mở rộng: ghi nhớ quá trình tìm gcd để truy ngược ra hệ số x, y

### 2. Cách thực hiện

```python
def gcdExtended(a, b):

    # Base Case
    if a == 0:
        return b, 0, 1

    gcd, x1, y1 = gcdExtended(b % a, a)

    # Update x and y using results of recursive
    # call
    x = y1 - (b//a) * x1
    y = x1

    return gcd, x, y

# Driver code
a, b = 26513, 32321
g = gcdExtended(a, b)
print("gcd(", a, ",", b, ") = ", g)
```

```python
$ python3 solve.py
gcd( 26513 , 32321 ) =  (1, 10245, -8404)
```

⇒ Flag: -8404
