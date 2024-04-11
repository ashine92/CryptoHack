# Privacy-Enhanced Mail?

As we've seen in the encoding section, cryptography involves dealing with data in a wide variety of formats: big integers, raw bytes, hex strings and more. A few structured formats have been standardised to help send and receive cryptographic data. It helps to be able to recognise and manipulate these common data formats.

PEM is a popular format for sending keys, certificates, and other cryptographic material. It looks like:

```
💡 ----BEGIN RSA PUBLIC KEY-----
MIIBCgKC...
*(a whole bunch of base64)*
----END RSA PUBLIC KEY-----

```

It wraps base64-encoded data by a one-line header and footer to indicate how to parse the data within. Perhaps unexpectedly, it's important for there to be the correct number of hyphens in the header and footer, otherwise cryptographic tools won't be able to recognise the file.

The data that gets base64-encoded is DER-encoded ASN.1 values. Confused? The resources linked below have more information about what these acronyms mean but the complexity is there for historical reasons and going too deep into the details may drive you insane.

Extract the private key *d* as a decimal integer from this PEM-formatted RSA key.

There are two main approaches for solving this challenge. The data in the certificate can be read with the openssl command line tool, or in Python using PyCryptodome. We recommend using PyCryptodome: first import the RSA module with `from Crypto.PublicKey import RSA` and you can read the key data using `RSA.importKey()`

**Challenge files:**

- [privacy_enhanced_mail.pem](https://cryptohack.org/static/challenges/privacy_enhanced_mail_1f696c053d76a78c2c531bb013a92d4a.pem)

**Resources:**

- [ASN.1 vs DER vs PEM vs x509 vs PKCS#7 vs ....](https://www.cryptologie.net/article/260/asn1-vs-der-vs-pem-vs-x509-vs-pkcs7-vs/)
- [A Warm Welcome to ASN.1 and DER](https://letsencrypt.org/docs/a-warm-welcome-to-asn1-and-der/)

---

### Cách 1:

```python
>>> from Crypto.PublicKey import RSA
>>> f = open("privacy_enhanced_mail_1f696c053d76a78c2c531bb013a92d4a.pem", "r")
>>> data = f.read()
>>> RSA.importKey(data)
```

![image](https://github.com/ashine92/CryptoHack/assets/62413378/028891de-35dc-401b-94e4-52ca6bf16db2)

### Cách 2:

```python
$ openssl rsa -in privacy_enhanced_mail_1f696c053d76a78c2c531bb013a92d4a.pem -text
Private-Key: (2048 bit, 2 primes)
modulus:
    00:ce:f2:83:b7:e1:0e:f8:0e:a8:13:52:c8:b5:2b:
    a7:91:62:7c:bc:de:93:81:cb:bc:0a:4d:3b:ee:3a:
    06:0d:f1:b6:36:dc:43:e2:fc:90:c4:64:d0:9e:0a:
    fa:8c:42:89:b9:5c:f6:30:8c:03:71:d5:ed:14:b2:
    05:f8:84:97:f4:77:c0:2d:0d:f2:89:e7:4d:4b:cd:
    27:fd:34:75:04:d7:09:4a:5c:c8:ba:a2:e6:17:17:
    5d:9a:39:9f:52:f1:c5:b8:52:ef:c6:05:d1:81:ad:
    e6:83:7a:fb:a2:54:d6:fb:57:f1:39:2d:19:55:e0:
    c9:a8:50:9a:39:14:6f:a0:06:0e:80:b8:2e:77:6f:
    c4:d1:a6:9a:26:2f:5c:37:b0:a3:99:d2:7b:43:79:
    ba:af:21:ae:0b:0a:84:bd:9d:4a:81:55:96:6b:b7:
    ca:70:5a:29:9e:5f:df:72:c4:9e:73:06:c3:57:98:
    56:7e:6b:f1:88:05:09:cb:59:8d:48:fc:24:7f:96:
    21:19:0f:bc:de:0f:4d:e7:cf:11:a4:b2:cc:5e:68:
    2d:e8:a8:a6:b6:25:a7:26:ca:ad:0c:f4:65:63:80:
    63:c5:da:6e:57:74:32:51:da:36:ca:6a:a7:aa:e6:
    67:13:fb:e5:53:f8:67:eb:fb:3c:f9:cb:5d:4e:a7:
    d2:0b
publicExponent: 65537 (0x10001)
privateExponent:
    7c:3b:1d:53:4f:29:9b:43:c1:26:08:76:30:3c:0a:
    95:be:17:bf:91:a5:df:2f:1c:ac:da:7c:75:a0:23:
    6e:4f:81:e1:21:0d:27:c0:12:6f:b3:4d:80:f2:7a:
    41:a4:d7:e4:8c:a7:c5:b0:e7:88:78:b1:9f:d0:d6:
    c0:bf:68:30:fb:8a:44:01:b1:6d:93:8a:d5:4c:4d:
    0b:35:68:62:05:6c:b0:55:4e:b2:ab:83:90:ad:18:
    25:b3:1d:af:bf:2f:c0:5d:19:4f:38:c2:f2:24:20:
    d3:21:0a:da:02:30:24:26:40:ca:e0:05:eb:85:cb:
    c8:dc:ca:18:25:ea:74:96:d9:b1:70:c5:cb:fe:35:
    4f:e1:9a:63:10:2b:82:f3:8d:5d:7c:25:17:35:20:
    8b:83:a5:42:40:92:7f:89:98:48:c1:6a:5f:e7:0c:
    e9:50:da:ff:7b:f9:f4:b7:1b:59:81:01:a5:20:48:
    cd:30:c1:6c:b9:94:33:0b:10:59:2d:2c:95:d4:d0:
    e5:79:f5:28:7f:f7:4a:88:26:8d:03:89:69:8c:8f:
    7b:9a:e8:13:f3:92:46:89:3d:02:66:1c:f0:8d:9c:
    bc:ec:9f:72:2c:f7:6d:0e:96:f1:e1:77:37:e2:9e:
    ce:86:76:76:7c:b6:e1:df:0d:bd:2d:73:1e:d8:48:
    b1
prime1:
    00:ed:fb:47:15:eb:a9:3b:c4:c2:cb:e7:12:c8:08:
    10:27:cc:86:a8:d2:8d:2c:78:c9:72:0e:6d:e6:f6:
    80:31:e0:e3:4f:fa:5e:ef:0f:d1:d0:85:ae:49:c0:
    a8:00:38:8b:f7:ee:98:a9:4a:77:e1:18:1e:60:39:
    24:b3:b3:bb:9d:ce:97:b8:00:62:f2:83:0c:8f:11:
    98:3d:fa:dd:55:f1:f9:ce:53:62:99:2e:14:c2:5f:
    77:6e:f7:da:ce:eb:71:9e:1c:f9:f2:f6:2f:4b:a6:
    d0:03:de:4d:42:7e:eb:5a:4d:98:15:64:4f:ce:12:
    55:93:1b:df:2b:a3:7f:c7:a7
prime2:
    00:de:9d:b5:c3:5d:25:62:f1:cd:36:22:34:28:18:
    c7:be:ba:03:33:20:7e:df:db:c3:f2:64:8e:6d:14:
    10:b8:91:49:74:a5:ae:32:af:a8:e4:ea:e4:0b:42:
    ad:a5:86:7e:1b:0e:33:2f:d0:d0:a2:c8:a9:de:1a:
    db:ed:bd:81:f9:ba:b4:c8:fe:c8:ce:3e:66:01:55:
    e2:cd:04:c6:92:5b:93:fd:88:af:be:05:dc:c5:52:
    a8:36:e3:53:a9:31:20:9b:23:a1:3e:7e:b0:f8:fa:
    91:9c:44:ac:48:5c:e3:7d:6a:da:85:30:ab:56:89:
    9c:66:69:d4:4c:58:74:ae:fd
exponent1:
    44:4c:de:bc:fa:d2:aa:35:b1:56:85:ee:0c:fc:cb:
    6e:30:b3:e1:15:f4:b0:73:c6:14:f6:f1:31:dd:43:
    33:8d:80:8f:be:a2:aa:67:d6:e6:ca:c7:17:a1:b4:
    55:c3:e4:df:f6:59:58:14:e8:4c:f0:f8:1e:d3:a7:
    a5:ef:8a:84:22:fb:c6:32:4e:33:9d:ca:e7:f0:bb:
    c9:e6:0a:ca:14:d5:86:12:c6:74:82:16:31:26:e7:
    07:31:19:5a:53:96:5b:33:a3:c4:c8:45:10:a8:42:
    81:29:b6:f0:c3:ae:56:4f:78:bb:82:fb:a8:7f:f8:
    91:6c:e9:63:03:dc:b3:77
exponent2:
    00:d3:f4:f7:3e:16:ee:e4:e1:73:51:0a:89:fc:6f:
    73:a7:9e:36:33:b4:c9:f8:5c:a7:99:9f:b2:98:1a:
    d5:bc:d5:e0:49:a7:02:50:12:3e:4e:0f:73:a7:61:
    0a:32:a2:f6:68:ce:41:60:52:82:83:ab:69:49:26:
    eb:a5:d5:9c:ee:68:9d:7f:0e:4f:a5:47:76:19:e9:
    6b:73:67:0b:a6:08:79:c4:99:23:33:5b:23:93:e1:
    1a:76:80:45:84:bf:58:db:3d:b6:65:e9:7c:98:e3:
    02:46:f6:7f:ce:ba:5a:83:6c:7c:b8:f9:d8:f9:21:
    36:ff:af:dd:c9:ff:22:c2:05
coefficient:
    76:bc:5d:83:0b:cc:7e:b7:21:e8:7a:f5:56:45:ff:
    b8:ce:dd:dd:e5:67:82:e5:30:46:13:d0:11:7b:b3:
    29:df:7b:da:ba:c7:bb:34:89:af:5b:7f:af:d0:0a:
    49:8e:c4:f0:bc:eb:ca:a1:38:c8:12:4b:8f:0b:f9:
    33:0a:99:03:50:4a:6f:5b:f6:8c:b6:20:b9:4b:03:
    42:83:b1:7e:4e:fc:5a:32:8b:3d:6c:73:0a:fb:9e:
    1e:ad:67:eb:55:40:24:6f:16:f8:88:10:69:1a:5d:
    d1:22:04:de:1e:4d:b7:23:7d:ce:66:77:fb:bd:78:
    0e:4d:db:53:f3:81:df:c6
writing RSA key
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDO8oO34Q74DqgT
Usi1K6eRYny83pOBy7wKTTvuOgYN8bY23EPi/JDEZNCeCvqMQom5XPYwjANx1e0U
sgX4hJf0d8AtDfKJ501LzSf9NHUE1wlKXMi6ouYXF12aOZ9S8cW4Uu/GBdGBreaD
evuiVNb7V/E5LRlV4MmoUJo5FG+gBg6AuC53b8TRppomL1w3sKOZ0ntDebqvIa4L
CoS9nUqBVZZrt8pwWimeX99yxJ5zBsNXmFZ+a/GIBQnLWY1I/CR/liEZD7zeD03n
zxGkssxeaC3oqKa2Jacmyq0M9GVjgGPF2m5XdDJR2jbKaqeq5mcT++VT+Gfr+zz5
y11Op9ILAgMBAAECggEAfDsdU08pm0PBJgh2MDwKlb4Xv5Gl3y8crNp8daAjbk+B
4SENJ8ASb7NNgPJ6QaTX5IynxbDniHixn9DWwL9oMPuKRAGxbZOK1UxNCzVoYgVs
sFVOsquDkK0YJbMdr78vwF0ZTzjC8iQg0yEK2gIwJCZAyuAF64XLyNzKGCXqdJbZ
sXDFy/41T+GaYxArgvONXXwlFzUgi4OlQkCSf4mYSMFqX+cM6VDa/3v59LcbWYEB
pSBIzTDBbLmUMwsQWS0sldTQ5Xn1KH/3SogmjQOJaYyPe5roE/OSRok9AmYc8I2c
vOyfciz3bQ6W8eF3N+KezoZ2dny24d8NvS1zHthIsQKBgQDt+0cV66k7xMLL5xLI
CBAnzIao0o0seMlyDm3m9oAx4ONP+l7vD9HQha5JwKgAOIv37pipSnfhGB5gOSSz
s7udzpe4AGLygwyPEZg9+t1V8fnOU2KZLhTCX3du99rO63GeHPny9i9LptAD3k1C
futaTZgVZE/OElWTG98ro3/HpwKBgQDenbXDXSVi8c02IjQoGMe+ugMzIH7f28Py
ZI5tFBC4kUl0pa4yr6jk6uQLQq2lhn4bDjMv0NCiyKneGtvtvYH5urTI/sjOPmYB
VeLNBMaSW5P9iK++BdzFUqg241OpMSCbI6E+frD4+pGcRKxIXON9atqFMKtWiZxm
adRMWHSu/QKBgERM3rz60qo1sVaF7gz8y24ws+EV9LBzxhT28THdQzONgI++oqpn
1ubKxxehtFXD5N/2WVgU6Ezw+B7Tp6XvioQi+8YyTjOdyufwu8nmCsoU1YYSxnSC
FjEm5wcxGVpTllszo8TIRRCoQoEptvDDrlZPeLuC+6h/+JFs6WMD3LN3AoGBANP0
9z4W7uThc1EKifxvc6eeNjO0yfhcp5mfspga1bzV4EmnAlASPk4Pc6dhCjKi9mjO
QWBSgoOraUkm66XVnO5onX8OT6VHdhnpa3NnC6YIecSZIzNbI5PhGnaARYS/WNs9
tmXpfJjjAkb2f866WoNsfLj52PkhNv+v3cn/IsIFAoGAdrxdgwvMfrch6Hr1VkX/
uM7d3eVnguUwRhPQEXuzKd972rrHuzSJr1t/r9AKSY7E8LzryqE4yBJLjwv5MwqZ
A1BKb1v2jLYguUsDQoOxfk78WjKLPWxzCvueHq1n61VAJG8W+IgQaRpd0SIE3h5N
tyN9zmZ3+714Dk3bU/OB38Y=
-----END PRIVATE KEY-----
```
