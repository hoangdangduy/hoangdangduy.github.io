---
title:  "Leet code 8: Chuyển đổi xâu sang số"
date:   2025-06-01 22:08:00 +0700
categories: leet-code algorithm
author: hoangdd
---
Bài toán: Chuyển đổi xâu sang số

[https://leetcode.com/problems/string-to-integer-atoi](https://leetcode.com/problems/string-to-integer-atoi)

Duyệt từ trái sang phải của xâu, qua từng ký tự
- Bỏ qua các ký tự trắng ở đầu xâu, bắt đầu xử lý ở ký tự khác ký tự trắng
- Gặp ký tự `+` hoặc `-` thì lưu lại để biết là dương hay âm
- Gặp ký tự chữ bất kỳ thì dừng lại

Sau 3 điều kiện trên thì sẽ đến kí tự số và bắt đầu xử lý chuyển sang số. nếu không có số nào ngay sau đó thì trả về 0 luôn

Integer.Max_VALUE = 2_147_483_647

Integer.Min_VALUE = -2_147_483_648

Nếu trị tuyệt đối kết quả cần trả về lớn hơn 2_147_483_647 thì ta chỉ cần xem dấu `+` hay `-` có trong xâu để trả về kết quả tương ứng là 2_147_483_647 hoặc -2_147_483_648 mà không cần tính toán tiếp, ngược lại thì trả về chính kết quả đang xét đi kèm với dấu.

Source code tham khảo: [https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_8_String_To_Integer_atoi](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_8_String_To_Integer_atoi)