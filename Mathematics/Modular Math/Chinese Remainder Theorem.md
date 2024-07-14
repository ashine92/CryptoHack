# Chinese Remainder Theory

The Chinese Remainder Theorem gives a unique solution to a set of linear congruences if their moduli are coprime.

This means, that given a set of arbitrary integers `ai`, and pairwise coprime integers `ni`, such that the following linear congruences hold:

Note "pairwise coprime integers" means that if we have a set of integers `{n1, n2, ..., ni}`, all pairs of integers selected from the set are coprime: `gcd(ni, nj) = 1`.

```
💡 x ≡ a1 mod n1
x ≡ a2 mod n2
...
x ≡ an mod nn
```

There is a unique solution `x ≡ a mod N`  where `N = n1 * n2 * ... * nn`.

In cryptography, we commonly use the Chinese Remainder Theorem to help us reduce a problem of very large integers into a set of several, easier problems.

Given the following set of linear congruences:

```
💡 x ≡ 2 mod 5
x ≡ 3 mod 11
x ≡ 5 mod 17
```

Find the integer `a`  such that `x ≡ a mod 935`

Starting with the congruence with the largest modulus, use that for `x ≡ a mod p` we can write `x = a + k*p`for arbitrary integer `k`.
