---
title:  "LeetCode 746: Tính chi phí nhỏ nhất để leo thang"
date:   2026-04-06 09:14:00 +0700
categories: leet-code algorithm
author: hoangdd
use_math: true
---
## Bài toán: Climbing Stairs

Link bài toán: [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs)

Bạn cần phải leo hết thang với chi phí nhỏ nhất. Ở mỗi bậc thang có một chi phí khác nhau và mỗi lần có thể bước 1 hoặc 2 bước.

### Phân tích giải pháp (Dynamic Programming)

Gọi `dp[i]` là chi phí nhỏ nhất để đạt được tới bậc thứ `i`.
Để đến được bậc `i`, bạn có thể đi từ bậc `i-1` hoặc bậc `i-2`.

**Công thức quy hoạch động:**
$$ dp[i] = \min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2]) $$

**Ví dụ:** `cost = [10, 15, 20]`

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin: 20px 0;">
  <thead>
    <tr style="background-color: #f2f2f2;">
      <th style="border: 1px solid #ddd; padding: 8px; text-align: left;">Chỉ số (index)</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">0</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">1</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">2</th>
      <th style="border: 1px solid #ddd; padding: 8px; text-align: center;">3 (Đích)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px; font-weight: bold;">Cost</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">10</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">15</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">20</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">-</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px; font-weight: bold;">dp[i]</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">0</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">0</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">10</td>
      <td style="border: 1px solid #ddd; padding: 8px; text-align: center;">15</td>
    </tr>
  </tbody>
</table>

**Giải thích:**
- `dp[0] = 0`, `dp[1] = 0` (vì có thể bắt đầu tại 0 hoặc 1).
- `dp[2]`:
    - Từ 0 lên 2 (2 bước): `dp[0] + cost[0] = 0 + 10 = 10`.
    - Từ 1 lên 2 (1 bước): `dp[1] + cost[1] = 0 + 15 = 15`.
    - $\rightarrow$ `dp[2] = min(10, 15) = 10`.
- `dp[3]`:
    - Từ 1 lên 3 (2 bước): `dp[1] + cost[1] = 0 + 15 = 15`.
    - Từ 2 lên 3 (1 bước): `dp[2] + cost[2] = 10 + 20 = 30`.
    - $\rightarrow$ `dp[3] = min(15, 30) = 15`.
  
### Source code tham khảo
Bạn có thể xem mã nguồn chi tiết tại: [GitHub Repository](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_746_Min_Cost_Climbing_Stairs)