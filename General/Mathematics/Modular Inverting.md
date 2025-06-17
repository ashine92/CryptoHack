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

Tham khảo: https://cp-algorithms.com/algebra/module-inverse.html

```python
>>> pow(3, -1, 13)
9
```
