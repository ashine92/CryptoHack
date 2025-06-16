# Greatest Common Divisor

**Ước số chung lớn nhất (GCD)**, đôi khi còn được gọi là ước số chung lớn nhất, là số lớn nhất chia hết cho cả hai số nguyên dương **a** và **b**.

Ví dụ, với **a = 12, b = 8**, ta có thể liệt kê các ước của a là: **{1, 2, 3, 4, 6, 12}**
và các ước của b là:**{1, 2, 4, 8}**.
So sánh hai tập hợp này, ta thấy **GCD(a, b) = 4**.

Bây giờ, hãy xét trường hợp **a = 11, b = 17**. Cả hai số này đều là số nguyên tố. Vì số nguyên tố chỉ có 1 và chính nó là ước, nên GCD **(a, b) = 1**.

Khi **GCD(a, b) = 1**, ta nói rằng a và b là hai số nguyên tố cùng nhau (**coprime**).

Nếu cả a và b đều là số nguyên tố, thì chắc chắn chúng cũng nguyên tố cùng nhau.
Nếu a là số nguyên tố và b nhỏ hơn a, thì a và b cũng nguyên tố cùng nhau.

Hãy suy nghĩ về trường hợp a là số nguyên tố và b lớn hơn a: tại sao chúng không nhất thiết nguyên tố cùng nhau?

Hiện có rất nhiều công cụ để tính GCD của hai số nguyên, nhưng trong trường hợp này bạn nên tìm hiểu thuật toán Euclid.

Hãy thử lập trình thuật toán đó — chỉ cần vài dòng mã. Dùng a = 12, b = 8 để kiểm thử.

Bây giờ, hãy tính GCD(a, b) với a = 66528, b = 52920 và nhập kết quả bên dưới.

# Solution
Phép chia Euclid (hay còn gọi là thuật toán Euclid thường) là một cách tính ước số chung lớn nhất (GCD) của hai số nguyên dương bằng cách lặp lại phép chia lấy dư.

Với 2 số nguyên dương a và b, giả sử a > b, thì phép chia Euclid thực hiện:
` a = b . q + r `
Trong đó:
- q: thương
- r: số dư, với 0 <= r < b
Sau đó, ta thay a <- b, b <- r và lặp lại quá trình này cho đến khi r = 0. Khi đó GCD chính là số chia cuối cùng khác 0.

**Ví dụ: Tính GCD(99, 78)**
1. 99 = 1 . 78 + 21
2. 78 = 3 . 21 + 15
3. 21 = 1 . 15 + 6
4. 15 = 2 . 6 + 3
5. 6 = 2 . 3 + 0

-> Dừng lại tại bước số dư = 0

Vậy gcd(99, 78) = 3

**✅ Ứng dụng**
- Tính nhanh GCD mà không cần liệt kê tất cả ước số.

- Cơ sở cho thuật toán Euclid mở rộng (tìm nghịch đảo modulo).

- Dùng trong giải phương trình Diophantine và RSA.
  
```python
>>> import math
>>> print(math.gcd(66528, 52920))
1512
```
