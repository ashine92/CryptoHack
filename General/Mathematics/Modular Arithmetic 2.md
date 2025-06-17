# Modular Arithmetic 2

Chúng ta sẽ tiếp tục từ thử thách trước và tưởng tượng rằng ta đã chọn một modulo p, và p là một số nguyên tố.

Tập các số nguyên theo modulo p tạo thành một trường (field), ký hiệu là Fp.

Nếu modulo không phải là số nguyên tố, thì tập các số nguyên theo modulo n chỉ tạo thành một vành (ring)

----
## Trường hữu hạn Fp:
Một trưởng hữu hạn Fp là tập hợp các số nguyên từ 0, 1, ..., p - 1, và với cả phép cộng và phép nhân, mọi phần tử a trong tập đều có nghịch đảo:

- Nghịch đảo cộng (b+): sao cho `a + b+ = 0`
- Nghịch đảo nhân (bx): sao cho `a x bx = 1`

Lưu ý: phần tử đơn vị (identity) trong phép cộng và phép nhân là khác nhau:

- Với cộng: `a + 0 = a`
- Với nhân: `a x 1 = a`

----
## Ví dụ với p = 17:
- Tính 3^17 mod 17
- Tính 5^17 mod 17

Tiếp theo:
- Dự đoán và tính 7^16 mod 17
----
Điều thú vị này được gọi là **Định lý nhỏ của Fermat (Fermat's Little Theorem).** Chúng ta sẽ cần nó (và các tổng quát của nó) khi học về mật mã RSA.

----
Giờ hãy lấy số nguyên tố lớn hơn:
- p = 65537
- Tính 27324678765^65536 mod 65537
----
Bạn có cần máy tính không? :D
# Solution
```python
>>> pow(273246787654, 65536) % 65537
1
# Hoac
>>> pow(273246787654, 65536, 65537)
1
```
