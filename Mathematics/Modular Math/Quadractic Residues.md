# Quadratic Residues
We've looked at multiplication and division in modular arithmetic, but what does it mean to take the square root modulo an integer?

For the following discussion, let's work modulo `p = 29` . We can take the integer `a = 11` and calculate $`a^2$ = 5 mod 29` . As `a = 11, $a^2$ = 5` , we say the square root of `5`  is `11` .

This feels good, but now let's think about the square root of `18` . From the above, we know we need to find some integer `a` such that $`a^2$ = 18` 

Your first idea might be to start with `a = 1` and loop to `a = p-1` . In this discussion `p`  isn't too large and we can quickly look.

Have a go, try coding this and see what you find. If you've coded it right, you'll find that for all `a ∈ Fp*`  you never find an `a`  such that $`a^2$ = 18` .

What we are seeing, is that for the elements of `F*p` , not every element has a square root. In fact, what we find is that for roughly one half of the elements of `Fp*` , there is no square root.

```
💡 We say that an integer `x`  is a *Quadratic Residue* if there exists an `a`  such that $`a^2$ = x mod p` . If there is no such solution, then the integer is a *Quadratic Non-Residue*.

```

In other words, `x` is a quadratic residue when it is possible to take the square root of `x`  modulo an integer `p`.

In the below list there are two non-quadratic residues and one quadratic residue.

Find the quadratic residue and then calculate its square root. Of the two possible roots, submit the smaller one as the flag.

If $`a^2$ = x`  then $(-a)^2$= x. So if `x`  is a quadratic residue in some finite field, then there are always two solutions for `a` .

```
💡 p = 29
ints = [14, 6, 11]

```
# Theory
Quaratic residues là các số nguyên có thể được biểu diễn dưới dạng bình phương của một số nguyên khác, modulo một số nguyên n. Cụ thể, một số `a` được gọi là quadratic residue modulo n nếu tồn tại số nguyên x sao cho:

`x^2 ≡ a (mod n)`

Nếu không tồn tại 𝑥 thỏa mãn phương trình này, thì 𝑎 được gọi là quadratic non-residue modulo 𝑛.

Ví dụ: với `n = 7`:

Các quaratic residues là 0, 1, 2, và 4 vì có các số x sao cho x^2 đồng dư với những số này theo modulo 7.


# Solution
```python
>>> for i in range(29):
...   if (pow(i, 2, 29) in ints):
...     print(pow(i, 2, 29), end=' - ')
...     print(i)
...
6 - 8
6 - 21
```

⇒ Đáp án là 8
