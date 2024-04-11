# Extended GCD

Let `a` and `b` be positive integers.

The extended Euclidean algorithm is an efficient way to find integers `u,v` such that

`a * u + b * v = gcd(a,b)`

Later, when we learn to decrypt RSA, we will need this algorithm to calculate the modular inverse of the public exponent.

Using the two primes `p = 26513, q = 32321`, find the integers `u,v` such that

`p * u + q * v = gcd(p,q)`

Enter whichever of `u` and `v` is the lower number as the flag.

Knowing that `p,q` are prime, what would you expect `gcd(p,q)` to be? For more details on the extended Euclidean algorithm, check out [this page](https://web.archive.org/web/20230511143526/http://www-math.ucdenver.edu/~wcherowi/courses/m5410/exeucalg.html).

# Solution

Tham khảo: https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/

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
