# Modular Square Root
In Legendre Symbol we introduced a fast way to determine whether a number is a square root modulo a prime. We can go further: there are algorithms for efficiently calculating such roots. The best one in practice is called Tonelli-Shanks, which gets its funny name from the fact that it was first described by an Italian in the 19th century and rediscovered independently by Daniel Shanks in the 1970s.

All primes that aren't 2 are of the form `p ≡ 1 mod 4` or `p ≡ 3 mod 4`, since all odd numbers obey these congruences. As the previous challenge hinted, in the `p ≡ 3 mod 4` case, a really simple formula for computing square roots can be [derived](https://crypto.stackexchange.com/a/20994)

directly from Fermat's little theorem. That leaves us still with the `p ≡ 1 mod 4` case, so a more general algorithm is required.

In a congruence of the form `$r^2$ ≡ a mod p`, Tonelli-Shanks calculates `r`.

Tonelli-Shanks doesn't work for composite (non-prime) moduli. Finding square roots modulo composites is computationally equivalent to integer factorization - that is, it's a hard problem.

The main use-case for this algorithm is finding elliptic curve co-ordinates. Its operation is somewhat complex so we're not going to discuss the details, however, implementations are easy to find and Sage has one built-in.

Find the square root of `a`modulo the 2048-bit prime `p`. Give the smaller of the two roots as your answer.

**Challenge files:**

- [output.txt](https://cryptohack.org/static/challenges/output_abe0beb359a950c8a0a9300897528a9d.txt)

---

# Cách 1: Dùng thuật toán Tonelli-Shanks đơn thuần

- Reference: https://www.youtube.com/watch?v=d7ZFCf95MAQ

```python
# Implementation of the Tonelli-Shanks algorithm as described at:
# https://en.wikipedia.org/wiki/Tonelli%E2%80%93Shanks_algorithm

def is_quadratic_residue(n, p):
  if n % p == 0:
    return True
  return pow(n, (p - 1) // 2, p) == 1

# Given an odd prime p and integer n, this is an algorithm to
# find a mod-p square root of n when possible

def tonelli_shanks(n, p):
  # Case when p|n, so n = 0 (mod p). The square root of 0 is 0.
  if n % p == 0:
    return 0

  # So assume n is coprime to p.
  # Use Eulers criteria to see if n is a quadratic residue.
  if not is_quadratic_residue(n, p):
    print("This value of n is not a quadratic residue")
    return None
  else:
    print("This value of n is a quadratic residue")

  # If p = 3 (mod 4) and since we know that n is  a quadratic residue
  # we can get the square root right now and be done.
  if p % 4 == 3:
    return pow(n, (p + 1)//4 , p)

  # So now p = 1 (mod 4) but this is not used in the algorithm.
  # Write p - 1 = (2^S)Q
  Q = p - 1
  S = 0
  while Q % 2 == 0:
    S += 1
    Q //= 2
  print("Q=", Q)
  print("S=", S)

  # Find a quadratic non-residue of p by brute force search
  z = 2
  while is_quadratic_residue(z, p):
    z += 1
  print("z=", z)

  # Initialize variables
  M = S
  c = pow(z, Q, p)
  t = pow(n, Q, p)
  R = pow(n, (Q + 1)//2, p)

  print("M=", M)
  print("c=", c)
  print("t=", t)
  print("R=", R)

  while t != 1:
    print("Loop")

    # Calculate i
    i = 0
    temp = t
    while temp != 1:
      i += 1
      temp  = (temp * temp) % p
    print("i=", i)

    # Calculate b, M, c, t, R
    pow2 = 2 ** (M - i - 1)
    b = pow(c, pow2, p)
    M = i
    c = (b * b) % p
    t = (t * b * b) % p
    R = (R * b) % p
    print("b=", b)
    print("M=", M)
    print("c=", c)
    print("t=", t)
    print("R=", R)

  # We have found a square root
  return R

a = 8479994658316772151941616510097127087554541274812435112009425778595495359700244470400642403747058566807127814165396640215844192327900454116257979487432016769329970767046735091249898678088061634796559556704959846424131820416048436501387617211770124292793308079214153179977624440438616958575058361193975686620046439877308339989295604537867493683872778843921771307305602776398786978353866231661453376056771972069776398999013769588936194859344941268223184197231368887060609212875507518936172060702209557124430477137421847130682601666968691651447236917018634902407704797328509461854842432015009878011354022108661461024768
p = 30531851861994333252675935111487950694414332763909083514133769861350960895076504687261369815735742549428789138300843082086550059082835141454526618160634109969195486322015775943030060449557090064811940139431735209185996454739163555910726493597222646855506445602953689527405362207926990442391705014604777038685880527537489845359101552442292804398472642356609304810680731556542002301547846635101455995732584071355903010856718680732337369128498655255277003643669031694516851390505923416710601212618443109844041514942401969629158975457079026906304328749039997262960301209158175920051890620947063936347307238412281568760161

print(tonelli_shanks(a, p))
```

# Cách 2: Dùng sage

![image](https://github.com/user-attachments/assets/c1fe9261-615b-48b6-adad-128fd9c25a2e)
