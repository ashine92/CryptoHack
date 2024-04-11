# SSH Keys

Secure Shell Protocol (SSH) is a network protocol that uses cryptography to establish a secure channel over an insecure network (i.e. the internet). SSH enables developers and system administrators to run commands on servers from the other side of the world, without their password being sniffed or data being stolen. It is therefore critical to the security of the web.

In the old days, system administrators used to logon to their servers using telnet. This works similarly to our interactive challenges that involve connecting to `[socket.cryptohack.org](http://socket.cryptohack.org)` - data is sent to a remote server, which performs actions based on what is sent. There is no transport encryption, so anyone listening in on the network (such as the WiFi access point owner, your ISP, or the NSA) can see all the telnet traffic.

As the internet became increasingly hostile, people realised the need for both authentication and encryption for administrative network traffic. SSH, first released in 1995, achieves these goals and much more, with advanced functionality built into the software like port forwarding, X11 forwarding, and SFTP (Secure File Transfer Protocol). SSH uses a client-server architecture, meaning the server runs SSH as a service daemon which is always online and waiting to receive connections, and the user runs an SSH client to make a connection to it.

Most commonly, SSH is configured to use public-private key pairs for authentication. On the server, a copy of the user's public key is stored. The user's private key is stored locally on their laptop.

Now let's say Bruce wants to connect as his user account `bschneier` to his server `bruces-server` . From his laptop he runs `ssh bschneier@bruces-server` . His SSH client opens a connection to the server on port 22 where the SSH daemon listens. First, the ciphers that will be used are agreed upon, then a session key to encrypt the connection is established using Diffie-Hellman Key exchange, but we won't go into the details on that here. Then, the server sends a random challenge message encrypted with Bruce's public key. Bruce uses his private key to decrypt the challenge and send a hash of the random challenge message back, proving that he owns the correct private key and he therefore authenticates himself to the server as `bschneier` . Now, the server gives Bruce a shell to run commands. If public-private key cryptography doesn't make sense to you yet, don't worry - we'll cover it extensively in the RSA category.

An SSH private key is stored in the PEM format, which we discussed in the "Privacy-Enhanced Mail" challenge. So it looks like this and is stored on Bruce's laptop at `/home/bschneier/.ssh/id_rsa` :

```
💡 ----BEGIN RSA PRIVATE KEY-----
MIIBCgKC...
*(a whole bunch of base64)*
----END RSA PRIVATE KEY-----

```

SSH public keys, however, use a different format:

```
💡 ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCtPLqba+GFvDHdFVs1Vvdk56cKqqw5cdomlu034666UsoFIqkig8H5kNsNefSpaR/iU7G0ZKCiWRRuAbTsuHN+Cz526XhQvzgKTBkTGYXdF/WdG/6/umou3Z0+wJvTZgvEmeEclvitBrPZkzhAK1M5ypgNR4p8scJplTgSSb84Ckqul/Dj/Sh+fwo6sU3S3j92qc27BVGChpQiGwjjut4CkHauzQA/gKCBIiLyzoFcLEHhjOBOEErnvrRPWCIAJhALkwV2rUbD4g1IWa7QI2q3nB0nlnjPnjjwaR7TpH4gy2NSIYNDdC1PZ8reBaFnGTXgzhQ2t0ROBNb+ZDgH8Fy+KTG+gEakpu20bRqB86NN6frDLOkZ9x3w32tJtqqrJTALy4Oi3MW0XPO61UBT133VNqAbNYGE2gx+mXBVOezbsY46C/V2fmxBJJKY/SFNs8wOVOHKwqRH0GI5VsG1YZClX3fqk8GDJYREaoyoL3HKQt1Ue/ZW7TlPRYzAoIB62C0= bschneier@facts

```

This format makes it easier for these public keys to be added as lines to the file `/home/bschneier/.ssh/authorized_keys` on the server. Adding the public key to this file allows the corresponding private key to be used to authenticate on the server.

The `ssh-keygen` command is used to produce these public-private keypairs.

Extract the modulus *`n`* as a decimal integer from Bruce's SSH public key.

**Challenge files:**

- [bruce_rsa.pub](https://cryptohack.org/static/challenges/bruce_rsa_6e7ecd53b443a97013397b1a1ea30e14.pub)

---
# Solution
```python
>>> from Crypto.PublicKey import RSA
>>> f = open("bruce_rsa_6e7ecd53b443a97013397b1a1ea30e14.pub", "r")
>>> data = f.read()
>>> pubkey = RSA.importKey(data)
>>> print(pubkey.n)
3931406272922523448436194599820093016241472658151801552845094518579507815990600459669259603645261532927611152984942840889898756532060894857045175300145765800633499005451738872081381267004069865557395638550041114206143085403607234109293286336393552756893984605214352988705258638979454736514997314223669075900783806715398880310695945945147755132919037973889075191785977797861557228678159538882153544717797100401096435062359474129755625453831882490603560134477043235433202708948615234536984715872113343812760102812323180391544496030163653046931414723851374554873036582282389904838597668286543337426581680817796038711228401443244655162199302352017964997866677317161014083116730535875521286631858102768961098851209400973899393964931605067856005410998631842673030901078008408649613538143799959803685041566964514489809211962984534322348394428010908984318940411698961150731204316670646676976361958828528229837610795843145048243492909
```
