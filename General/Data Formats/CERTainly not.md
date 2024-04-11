# CERTainly not
As mentioned in the previous challenge, PEM is just a nice wrapper above DER encoded ASN.1. In some cases you may come across DER files directly; for instance many Windows utilities prefer to work with DER files by default. However, other tools expect PEM format and have difficulty importing a DER file, so it's good to know how to convert one format to another.

An SSL certificate is a crucial part of the modern web, binding a cryptographic key to details about an organisation. We'll cover more about these and PKI in the TLS category. Presented here is a DER-encoded x509 RSA certificate. Find the modulus of the certificate, giving your answer as a decimal.

**Challenge files:**

- [2048b-rsa-example-cert.der](https://cryptohack.org/static/challenges/2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der)

---

### Cách 1: Chuyển file der thành pem

Follow this web: https://www.oreilly.com/library/view/linux-security-cookbook/0596003919/ch04s10.html. Ta có thể convert file der thành pem:

```python
$ openssl x509 -inform der -in 2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der -out 2048.pem
$ cat 2048.pem
-----BEGIN CERTIFICATE-----
MIIC2jCCAkMCAg38MA0GCSqGSIb3DQEBBQUAMIGbMQswCQYDVQQGEwJKUDEOMAwG
A1UECBMFVG9reW8xEDAOBgNVBAcTB0NodW8ta3UxETAPBgNVBAoTCEZyYW5rNERE
MRgwFgYDVQQLEw9XZWJDZXJ0IFN1cHBvcnQxGDAWBgNVBAMTD0ZyYW5rNEREIFdl
YiBDQTEjMCEGCSqGSIb3DQEJARYUc3VwcG9ydEBmcmFuazRkZC5jb20wHhcNMTIw
ODIyMDUyNzQxWhcNMTcwODIxMDUyNzQxWjBKMQswCQYDVQQGEwJKUDEOMAwGA1UE
CAwFVG9reW8xETAPBgNVBAoMCEZyYW5rNEREMRgwFgYDVQQDDA93d3cuZXhhbXBs
ZS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC0z9FeMynsC8+u
dvX+LciZxnh5uRj4C9S6tNeeAlIGCfQYk0zUcNFCoCkTknNQd/YEiawDLNbxBqut
bMDZ1aarys1a0lYmUeVLCIqvzBkPJTSQsCopQQ9V8WuT252zzNzs68dVGNdCJd5J
NRQykpwexmnjPPv0mvj7i8XgG379TyW6P+WWV5okeUkXJ9eJS2ouDYdR2SM9BoVW
+FgxDu6BmXhozW5EfsnajFp7HL8kQClI0QOc79yuKl3492rH6bzFsFn2lfwWy9ic
7cP8EpCTeFp1tFaD+vxBhPZkeTQ1HKx6hQ5zeHIB5ySJJZ7af2W8r4eTGYzbdRW2
4DDHCPhZAgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAQMv+BFvGdMVzkQaQ3/+2noVz
/uAKbzpEL8xTcxYyP3lkOeh4FoxiSWqy5pGFALdPONoDuYFpLhjJSZaEwuvjI/Tr
rGhLV1pRG9frwDFshqD2Vaj4ENBCBh6UpeBop5+285zQ4SI7q4U9oSebUDJiuOx6
+tZ9KynmrbJpTSi0+Ao=
```

Lấy modulus:

```python
>>> from Crypto.PublicKey import RSA
>>> f = open("2048.pem", "r")
>>> data = f.read()
>>> RSA.importKey(data)
```

![image](https://github.com/ashine92/CryptoHack/assets/62413378/75b984f9-e52b-43b6-b2de-43b87d3d281a)

### Cách 2: Read trực tiếp từ file der

```python
$ openssl x509 -inform der -in 2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der
```

![image](https://github.com/ashine92/CryptoHack/assets/62413378/20dc0be2-8cfb-4203-bc29-65ac17ba510a)

```python
$ openssl x509 -inform der -in 2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der -text
Certificate:
    Data:
        Version: 1 (0x0)
        Serial Number: 3580 (0xdfc)
        Signature Algorithm: sha1WithRSAEncryption
        Issuer: C = JP, ST = Tokyo, L = Chuo-ku, O = Frank4DD, OU = WebCert Support, CN = Frank4DD Web CA, emailAddress = support@frank4dd.com
        Validity
            Not Before: Aug 22 05:27:41 2012 GMT
            Not After : Aug 21 05:27:41 2017 GMT
        Subject: C = JP, ST = Tokyo, O = Frank4DD, CN = www.example.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:b4:cf:d1:5e:33:29:ec:0b:cf:ae:76:f5:fe:2d:
                    c8:99:c6:78:79:b9:18:f8:0b:d4:ba:b4:d7:9e:02:
                    52:06:09:f4:18:93:4c:d4:70:d1:42:a0:29:13:92:
                    73:50:77:f6:04:89:ac:03:2c:d6:f1:06:ab:ad:6c:
                    c0:d9:d5:a6:ab:ca:cd:5a:d2:56:26:51:e5:4b:08:
                    8a:af:cc:19:0f:25:34:90:b0:2a:29:41:0f:55:f1:
                    6b:93:db:9d:b3:cc:dc:ec:eb:c7:55:18:d7:42:25:
                    de:49:35:14:32:92:9c:1e:c6:69:e3:3c:fb:f4:9a:
                    f8:fb:8b:c5:e0:1b:7e:fd:4f:25:ba:3f:e5:96:57:
                    9a:24:79:49:17:27:d7:89:4b:6a:2e:0d:87:51:d9:
                    23:3d:06:85:56:f8:58:31:0e:ee:81:99:78:68:cd:
                    6e:44:7e:c9:da:8c:5a:7b:1c:bf:24:40:29:48:d1:
                    03:9c:ef:dc:ae:2a:5d:f8:f7:6a:c7:e9:bc:c5:b0:
                    59:f6:95:fc:16:cb:d8:9c:ed:c3:fc:12:90:93:78:
                    5a:75:b4:56:83:fa:fc:41:84:f6:64:79:34:35:1c:
                    ac:7a:85:0e:73:78:72:01:e7:24:89:25:9e:da:7f:
                    65:bc:af:87:93:19:8c:db:75:15:b6:e0:30:c7:08:
                    f8:59
                Exponent: 65537 (0x10001)
    Signature Algorithm: sha1WithRSAEncryption
    Signature Value:
        40:cb:fe:04:5b:c6:74:c5:73:91:06:90:df:ff:b6:9e:85:73:
        fe:e0:0a:6f:3a:44:2f:cc:53:73:16:32:3f:79:64:39:e8:78:
        16:8c:62:49:6a:b2:e6:91:85:00:b7:4f:38:da:03:b9:81:69:
        2e:18:c9:49:96:84:c2:eb:e3:23:f4:eb:ac:68:4b:57:5a:51:
        1b:d7:eb:c0:31:6c:86:a0:f6:55:a8:f8:10:d0:42:06:1e:94:
        a5:e0:68:a7:9f:b6:f3:9c:d0:e1:22:3b:ab:85:3d:a1:27:9b:
        50:32:62:b8:ec:7a:fa:d6:7d:2b:29:e6:ad:b2:69:4d:28:b4:
        f8:0a
-----BEGIN CERTIFICATE-----
MIIC2jCCAkMCAg38MA0GCSqGSIb3DQEBBQUAMIGbMQswCQYDVQQGEwJKUDEOMAwG
A1UECBMFVG9reW8xEDAOBgNVBAcTB0NodW8ta3UxETAPBgNVBAoTCEZyYW5rNERE
MRgwFgYDVQQLEw9XZWJDZXJ0IFN1cHBvcnQxGDAWBgNVBAMTD0ZyYW5rNEREIFdl
YiBDQTEjMCEGCSqGSIb3DQEJARYUc3VwcG9ydEBmcmFuazRkZC5jb20wHhcNMTIw
ODIyMDUyNzQxWhcNMTcwODIxMDUyNzQxWjBKMQswCQYDVQQGEwJKUDEOMAwGA1UE
CAwFVG9reW8xETAPBgNVBAoMCEZyYW5rNEREMRgwFgYDVQQDDA93d3cuZXhhbXBs
ZS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC0z9FeMynsC8+u
dvX+LciZxnh5uRj4C9S6tNeeAlIGCfQYk0zUcNFCoCkTknNQd/YEiawDLNbxBqut
bMDZ1aarys1a0lYmUeVLCIqvzBkPJTSQsCopQQ9V8WuT252zzNzs68dVGNdCJd5J
NRQykpwexmnjPPv0mvj7i8XgG379TyW6P+WWV5okeUkXJ9eJS2ouDYdR2SM9BoVW
+FgxDu6BmXhozW5EfsnajFp7HL8kQClI0QOc79yuKl3492rH6bzFsFn2lfwWy9ic
7cP8EpCTeFp1tFaD+vxBhPZkeTQ1HKx6hQ5zeHIB5ySJJZ7af2W8r4eTGYzbdRW2
4DDHCPhZAgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAQMv+BFvGdMVzkQaQ3/+2noVz
/uAKbzpEL8xTcxYyP3lkOeh4FoxiSWqy5pGFALdPONoDuYFpLhjJSZaEwuvjI/Tr
rGhLV1pRG9frwDFshqD2Vaj4ENBCBh6UpeBop5+285zQ4SI7q4U9oSebUDJiuOx6
+tZ9KynmrbJpTSi0+Ao=
-----END CERTIFICATE-----
```

Quan sát phần modulus ta thấy nó đang có dạng `00:b4:cf:...`   nên ta chuyển thành dạng hex đơn thuần với option `-modulus` :

```python
$ openssl x509 -inform der -in 2048b-rsa-example-cert_3220bd92e30015fe4fbeb84a755e7ca5.der -text -modulus
Certificate:
    Data:
        Version: 1 (0x0)
        Serial Number: 3580 (0xdfc)
        Signature Algorithm: sha1WithRSAEncryption
        Issuer: C = JP, ST = Tokyo, L = Chuo-ku, O = Frank4DD, OU = WebCert Support, CN = Frank4DD Web CA, emailAddress = support@frank4dd.com
        Validity
            Not Before: Aug 22 05:27:41 2012 GMT
            Not After : Aug 21 05:27:41 2017 GMT
        Subject: C = JP, ST = Tokyo, O = Frank4DD, CN = www.example.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:b4:cf:d1:5e:33:29:ec:0b:cf:ae:76:f5:fe:2d:
                    c8:99:c6:78:79:b9:18:f8:0b:d4:ba:b4:d7:9e:02:
                    52:06:09:f4:18:93:4c:d4:70:d1:42:a0:29:13:92:
                    73:50:77:f6:04:89:ac:03:2c:d6:f1:06:ab:ad:6c:
                    c0:d9:d5:a6:ab:ca:cd:5a:d2:56:26:51:e5:4b:08:
                    8a:af:cc:19:0f:25:34:90:b0:2a:29:41:0f:55:f1:
                    6b:93:db:9d:b3:cc:dc:ec:eb:c7:55:18:d7:42:25:
                    de:49:35:14:32:92:9c:1e:c6:69:e3:3c:fb:f4:9a:
                    f8:fb:8b:c5:e0:1b:7e:fd:4f:25:ba:3f:e5:96:57:
                    9a:24:79:49:17:27:d7:89:4b:6a:2e:0d:87:51:d9:
                    23:3d:06:85:56:f8:58:31:0e:ee:81:99:78:68:cd:
                    6e:44:7e:c9:da:8c:5a:7b:1c:bf:24:40:29:48:d1:
                    03:9c:ef:dc:ae:2a:5d:f8:f7:6a:c7:e9:bc:c5:b0:
                    59:f6:95:fc:16:cb:d8:9c:ed:c3:fc:12:90:93:78:
                    5a:75:b4:56:83:fa:fc:41:84:f6:64:79:34:35:1c:
                    ac:7a:85:0e:73:78:72:01:e7:24:89:25:9e:da:7f:
                    65:bc:af:87:93:19:8c:db:75:15:b6:e0:30:c7:08:
                    f8:59
                Exponent: 65537 (0x10001)
    Signature Algorithm: sha1WithRSAEncryption
    Signature Value:
        40:cb:fe:04:5b:c6:74:c5:73:91:06:90:df:ff:b6:9e:85:73:
        fe:e0:0a:6f:3a:44:2f:cc:53:73:16:32:3f:79:64:39:e8:78:
        16:8c:62:49:6a:b2:e6:91:85:00:b7:4f:38:da:03:b9:81:69:
        2e:18:c9:49:96:84:c2:eb:e3:23:f4:eb:ac:68:4b:57:5a:51:
        1b:d7:eb:c0:31:6c:86:a0:f6:55:a8:f8:10:d0:42:06:1e:94:
        a5:e0:68:a7:9f:b6:f3:9c:d0:e1:22:3b:ab:85:3d:a1:27:9b:
        50:32:62:b8:ec:7a:fa:d6:7d:2b:29:e6:ad:b2:69:4d:28:b4:
        f8:0a
Modulus=B4CFD15E3329EC0BCFAE76F5FE2DC899C67879B918F80BD4BAB4D79E02520609F418934CD470D142A0291392735077F60489AC032CD6F106ABAD6CC0D9D5A6ABCACD5AD2562651E54B088AAFCC190F253490B02A29410F55F16B93DB9DB3CCDCECEBC75518D74225DE49351432929C1EC669E33CFBF49AF8FB8BC5E01B7EFD4F25BA3FE596579A2479491727D7894B6A2E0D8751D9233D068556F858310EEE81997868CD6E447EC9DA8C5A7B1CBF24402948D1039CEFDCAE2A5DF8F76AC7E9BCC5B059F695FC16CBD89CEDC3FC129093785A75B45683FAFC4184F6647934351CAC7A850E73787201E72489259EDA7F65BCAF8793198CDB7515B6E030C708F859
-----BEGIN CERTIFICATE-----
MIIC2jCCAkMCAg38MA0GCSqGSIb3DQEBBQUAMIGbMQswCQYDVQQGEwJKUDEOMAwG
A1UECBMFVG9reW8xEDAOBgNVBAcTB0NodW8ta3UxETAPBgNVBAoTCEZyYW5rNERE
MRgwFgYDVQQLEw9XZWJDZXJ0IFN1cHBvcnQxGDAWBgNVBAMTD0ZyYW5rNEREIFdl
YiBDQTEjMCEGCSqGSIb3DQEJARYUc3VwcG9ydEBmcmFuazRkZC5jb20wHhcNMTIw
ODIyMDUyNzQxWhcNMTcwODIxMDUyNzQxWjBKMQswCQYDVQQGEwJKUDEOMAwGA1UE
CAwFVG9reW8xETAPBgNVBAoMCEZyYW5rNEREMRgwFgYDVQQDDA93d3cuZXhhbXBs
ZS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC0z9FeMynsC8+u
dvX+LciZxnh5uRj4C9S6tNeeAlIGCfQYk0zUcNFCoCkTknNQd/YEiawDLNbxBqut
bMDZ1aarys1a0lYmUeVLCIqvzBkPJTSQsCopQQ9V8WuT252zzNzs68dVGNdCJd5J
NRQykpwexmnjPPv0mvj7i8XgG379TyW6P+WWV5okeUkXJ9eJS2ouDYdR2SM9BoVW
+FgxDu6BmXhozW5EfsnajFp7HL8kQClI0QOc79yuKl3492rH6bzFsFn2lfwWy9ic
7cP8EpCTeFp1tFaD+vxBhPZkeTQ1HKx6hQ5zeHIB5ySJJZ7af2W8r4eTGYzbdRW2
4DDHCPhZAgMBAAEwDQYJKoZIhvcNAQEFBQADgYEAQMv+BFvGdMVzkQaQ3/+2noVz
/uAKbzpEL8xTcxYyP3lkOeh4FoxiSWqy5pGFALdPONoDuYFpLhjJSZaEwuvjI/Tr
rGhLV1pRG9frwDFshqD2Vaj4ENBCBh6UpeBop5+285zQ4SI7q4U9oSebUDJiuOx6
+tZ9KynmrbJpTSi0+Ao=
-----END CERTIFICATE-----
```

Ta convert phần hex này thành decimal bằng python:

```python
>>> int('B4CFD15E3329EC0BCFAE76F5FE2DC899C67879B918F80BD4BAB4D79E02520609F418934CD470D142A0291392735077F60489AC032CD6F106ABAD6CC0D9D5A6ABCACD5AD2562651E54B088AAFCC190F253490B02A29410F55F16B93DB9DB3CCDCECEBC75518D74225DE49351432929C1EC669E33CFBF49AF8FB8BC5E01B7EFD4F25BA3FE596579A2479491727D7894B6A2E0D8751D9233D068556F858310EEE81997868CD6E447EC9DA8C5A7B1CBF24402948D1039CEFDCAE2A5DF8F76AC7E9BCC5B059F695FC16CBD89CEDC3FC129093785A75B45683FAFC4184F6647934351CAC7A850E73787201E72489259EDA7F65BCAF8793198CDB7515B6E030C708F859', 16)
22825373692019530804306212864609512775374171823993708516509897631547513634635856375624003737068034549047677999310941837454378829351398302382629658264078775456838626207507725494030600516872852306191255492926495965536379271875310457319107936020730050476235278671528265817571433919561175665096171189758406136453987966255236963782666066962654678464950075923060327358691356632908606498231755963567382339010985222623205586923466405809217426670333410014429905146941652293366212903733630083016398810887356019977409467374742266276267137547021576874204809506045914964491063393800499167416471949021995447722415959979785959569497
```
