---
title:  "Leet code 70: Tính số cách leo thang"
date:   2026-04-02 09:17:00 +0700
categories: leet-code algorithm
author: hoangdd
use_math: true
---
## Bài toán: Climbing Stairs

Link bài toán: [LeetCode 70 - Climbing Stairs](https://leetcode.com/problems/climbing-stairs)

Bài tương tự:
- [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number)

Bạn đang leo một cầu thang có `n` bậc. Mỗi lần bạn có thể bước **1 bước** hoặc **2 bước**. Hỏi có bao nhiêu cách khác nhau để leo lên đến đỉnh?

### Phân tích ví dụ:

- **n = 1**: Có 1 cách (`1`)
- **n = 2**: Có 2 cách (`1+1`, `2`)
- **n = 3**: Có 3 cách (`1+1+1`, `1+2`, `2+1`)
- **n = 4**: Có 5 cách (`1+1+1+1`, `1+1+2`, `1+2+1`, `2+1+1`, `2+2`)

### Công thức tổng quát

Nhận thấy rằng để đạt đến bậc thứ `n`, bạn chỉ có thể đi từ bậc `n-1` (bước thêm 1 bước) hoặc từ bậc `n-2` (bước thêm 2 bước). Do đó, số cách để đạt đến bậc `n` là tổng số cách của hai bậc trước đó:

$$f(n) = f(n-1) + f(n-2)$$

Đây chính là dãy số **Fibonacci**.

---

### Các phương pháp giải quyết

#### 1. Top-down Dynamic Programming (Memoization)
Sử dụng đệ quy để tính từ $f(n)$ xuống. Để tránh việc tính toán lặp lại các giá trị đã biết, chúng ta sử dụng một mảng hoặc hash map để lưu trữ kết quả của các bài toán con.

- **Độ phức tạp thời gian:** $O(n)$
- **Độ phức tạp không gian:** $O(n)$

#### 2. Bottom-up Iterative (Dynamic Programming)
Tính toán từ dưới lên trên bắt đầu từ các trường hợp cơ bản ($n=1, n=2$). 

> **Tối ưu:** Vì chúng ta chỉ cần hai giá trị liền trước để tính giá trị hiện tại, ta có thể chỉ cần dùng 2 biến thay vì cả một mảng, giúp đưa độ phức tạp không gian về $O(1)$.

- **Độ phức tạp thời gian:** $O(n)$
- **Độ phức tạp không gian:** $O(1)$

---

### Source code tham khảo
Bạn có thể xem mã nguồn chi tiết tại: [GitHub Repository](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_70_Climbing_Stairs)