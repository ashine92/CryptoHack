# Successive Powers
The following integers: 
{588, 665, 216, 113, 642, 4, 836, 114, 851, 492, 819, 237} are successive large powers of an integer x, modulo a three digit prime p.

Find p and x to obtain the flag.

You can do this with a pen and paper. We've included this challenge as an excuse for you to get used to algebra and modular mathematics.

------
## Manual
We're given a list of successive modular powers of an element x, than means that:
`588 . x ≡ 665 (mod p)`
`665 . x ≡ 665 (mod p)` and so on.
In particular we have:
`113 . x ≡ 642 (mod p)` and `114 . x ≡ 851 (mod p)`

It could seems that choosing `113 . x ` and `114 . x` equations is sort of cheating, a general solution is to select two coprime numbers and with the Extended Eucledian Algorithm one can find out the two integers needed to get the linear commination to write 1 with the numbers the challenge gave you.
So, subtracting: `x ≡ 851 - 642 = 209 (mod p)`.

So we've found the value of `x`

To find `p` just take the first equation and replace the value for x: `588 . 209 ≡ 665 (mod p)` means that `588 . 209 - 665 ≡ 0 (mod p)`, so `p = 588 . 209 - 665 = 122227`

if you factorize the last number you get: 122227 = 7 . 19 . 919

The only good cadidate is `p = 919`.

## Bruteforce
```python3
from sympy import isprime
powers = [588, 665, 216, 113, 642, 4, 836, 114, 851, 492, 819, 237]
basis = [x for x in range(100,1000) if isprime(x)]
for p in basis:
    for x in range(1,p):
        for i,power in enumerate(powers):
            if i==len(powers)-1:
                print('crypto{',p,',',x,'}',sep='')
            elif not (x*power)%p==powers[i+1]: break
```
