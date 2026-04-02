---
title:  "Leet code 70: Tính số cách leo thang"
date:   2026-04-02 09:17:00 +0700
categories: leet-code algorithm
author: hoangdd
---
Bài toán: Tính số cách để leo thang

[https://leetcode.com/problems/climbing-stairs](https://leetcode.com/problems/climbing-stairs)

Mỗi lần sẽ di chuyển được 1 hoặc 2 bước.

Giả sử:
1. nếu có 1 bậc thang thì sẽ có 1 cách:
- 1
2. nếu có 2 bậc thang thì sẽ có 2 cách:
- 1 - 1
- 2
3. nếu có 3 bậc thang thì sẽ có 3 cách:
- 1 - 1 - 1
- 1 - 2
- 2 - 1
4. nếu có 4 bậc thang thì sẽ có 5 cách:
- 1 - 1 - 1 - 1
- 1 - 1 - 2
- 1 - 2 - 1
- 2 - 1 - 1
- 2 - 2

Vì mỗi lần chỉ đi được 1 hoặc 2 bước nên ta sẽ có bài toán tổng quát là f(n) = f(n-1) + f(n-2)

Cách 1: Top-down Dynamic Programming (Memoization)

Chúng ta sẽ đệ quy từ trên xuống dưới khi tính f(n) thì cần tính f(n-1) và f(n-2) tức là cần phải lưu lại giá trị mỗi lần tính toán f(n-1), f(n-2) để tối ưu về độ phức tạp không gian và thời gian.


Cách 2: Bottom-up Iterative

Chúng ta sẽ tính toán từ dưới lên trên nên không cần lưu lại tất cả giá trị mà chỉ cần lưu lại giá trị của f(n-1), f(n-2) ngay trước đó.

Source code tham khảo: [https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_70_Climbing_Stairs](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_70_Climbing_Stairs)