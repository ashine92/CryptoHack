# Modular Inverting
Như chúng ta đã thấy, ta có thể thực hiện phép cộng và nhân torng một trường hữu hạn Fp, và luôn thu được một phần tử khác cũng thuộc trường đó.

Với mọi phần tử g trong trường, tồn tại duy nhất một số nguyên d sao cho:

`g . d ≡ 1 mod p`

Đây gọi là nghịch đảo nhân (multiplicative inverse) của `g`.

Ví dụ:
`7 . 8 = 56 ≡ 1 mod 11`

-> Vậy 8 là nghịch đảo nhân của `7 mod 11`

## Câu hỏi:
Tìm nghịch đảo nhân của 3 mod 13, tức là tìm d = 3^-1 sao cho:
`3 . d ≡ 1 mod 13`

Hãy suy nghĩ về định lý nhỏ Fermat mà ta vừa học. Nó giúp gì cho bạn trong việc tìm nghịch đảo của một phần tử?


# Solution
### 1. Python Code
```python
>>> pow(3, -1, 13)
9
```
----
### 2. Dùng Định lý nhỏ Fermat
Định lý nhỏ Fermat phát biểu: Với một số nguyên tố p và một số nguyên tố a không chia hết cho p (tức gcd(a,p) = 1), thì:

![image](https://github.com/user-attachments/assets/2e16c911-2ca1-4994-ac97-e66948c1dc42)

Suy ra: 

![image](https://github.com/user-attachments/assets/382fc5f1-b693-49ab-8c9f-a57a987d8097)

Đây chính là công thức tính nghịch đảo modular của a mod p khi p là số nguyên tố

----

Ta có:
- a = 3
- p = 13 là số nguyên tố
- gcd(3,13) = 1 -> thỏa điều kiện áp dụng Fermat
  
Áp dụng công thức:

![image](https://github.com/user-attachments/assets/daae3a2a-e305-4017-9b07-23145cf865e5)

![image](https://github.com/user-attachments/assets/2b691d5d-759f-41dc-a382-5875ae97b817)

![image](https://github.com/user-attachments/assets/0fc46df4-6da9-49f3-a914-e317a80b6a7d)
