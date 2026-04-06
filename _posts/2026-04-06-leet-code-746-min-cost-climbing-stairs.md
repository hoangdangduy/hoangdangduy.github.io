---
title:  "Leet code 746: Tính chi phí nhỏ nhất để leo thang"
date:   2026-04-06 09:14:00 +0700
categories: leet-code algorithm
author: hoangdd
use_math: false
---
## Bài toán: Climbing Stairs

Link bài toán: [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs)

Bạn cần phải leo hết thang với chi phí nhỏ nhất. Ở mỗi bậc thang có một chi phí khác nhau và mỗi lần có thể bước 1 hoặc 2 bước.

### Phân tích ví dụ:

Giả sử cầu thang có 3 bậc, chi phí mỗi bậc lần lượt là `[10, 15, 20]`. Có thể bước 1 hoặc 2 bước mỗi lần nên ta có thể đứng ở index 0 hoặc index 1 như bảng dưới:

| index  | 0 | 1  | 2  | 3  |
|--------|---|----|----|----|
| cost   | 10 | 15 | 20 |    |

| index | 0 | 1 | 2  | 3  |
|-------|---|---|----|----|
| dp[0] | 0 |   |    |    |
| dp[1] | 0 | 0 |    |    |
| dp[2] |   | 0 | 10 |    |
| dp[3] |   |   | 10 | 15 |

Ta sẽ duyệt index lần lượt từ `index 2` trở đi và tìm chi phi nhỏ nhất đứng ở mỗi bước.

Ở **dp[0]**, **dp[1]**: chi phí đều là 0

Ở **dp[2]**: index bằng 2, ta sẽ tìm min của bước nhảy nếu đứng từ `index 0` và `index 1` thì chi phí nhỏ nhất bằng 10
- nếu đứng từ `index 0` thì chi phí là 0 + 10 = 10
- nếu đứng từ `index 1` thì chi phí là 0 + 15 = 15

Ở **dp[3]**: index bằng 3, ta sẽ tìm min của bước nhảy nếu đứng từ `index 1` và `index 2`.
- nếu đứng từ `index 1` thì chi phí là 0 + 15 = 15
- nếu đứng từ `index 2` thì chi phí là 10 + 20 = 30

vậy chi phí nhỏ nhất là 15 --> công thức tổng quát:
    $$ currentValue[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2]) $$

### Source code tham khảo
Bạn có thể xem mã nguồn chi tiết tại: [GitHub Repository](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_746_Min_Cost_Climbing_Stairs)