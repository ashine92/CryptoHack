# Modular Arithmetic 1

Hãy tưởng tượng bạn nghiêng người nhìn vào cuốn sổ tay của một nhà mật mã học. Bạn thấy vài ghi chú bên lề:

```
4 + 9 = 1  
5 - 7 = 10  
2 + 3 = 5  
```
Lúc đầu, bạn có thể nghĩ rằng họ bị điên. Bạn sẽ nghĩ, “Chắc đây là lý do tại sao ngày nay có quá nhiều vụ rò rỉ dữ liệu”, nhưng thực ra đây chỉ là số học modulo 12 (dù cách viết hơi cẩu thả một chút)

Có thể bạn chưa từng gọi nó là "số học đồng dư", nhưng bạn đã thực hiện các phép tính như vậy từ khi học cách xem giờ (hãy nhìn lại các phương trình đó và tưởng tượng đang cộng giờ đồng hồ).

Một cách chính xác, “tính giờ” được mô tả bằng lý thuyết đồng dư (congruences). Ta nói rằng hai số nguyên a và b là đồng dư theo modulo m nếu:
`a≡b (mod m)`

Nói cách khác, khi chia a cho m, phần dư là b. Điều này cũng có nghĩa là nếu m chia hết a (ký hiệu: m | a ) thì: `a≡0(mod m)`

**Yêu cầu: Hãy tính các đồng dư sau:**
1. `11 ≡ x mod 6`
2. `8146798528947 ≡ y mod 17`

Sau đó, lấy số nhỏ hơn trong hai kết quả x và y làm đáp án cuối cùng.

# Solution

```python
>>> 11 % 6
5
>>> 8146798528947 %  17
4
```

Vì 4 < 5 nên đáp án là 4
