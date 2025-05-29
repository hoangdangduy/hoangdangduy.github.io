---
title:  "Leet code 6: Chuyển đổi xâu theo dạng zigzag"
date:   2025-05-28 22:28:00 +0700
categories: leet-code algorithm
author: hoangdd
---
Bài toán: Chuyển đổi xâu theo dạng zigzag

[https://leetcode.com/problems/zigzag-conversion](https://leetcode.com/problems/zigzag-conversion)

Ví dụ với xâu `PAYPALISHIRING` thì ta sẽ có index như sau:

<div class="container-fluid">
  <div class="row">
    <div class="col-12 col-md-8">
      <div class="table-responsive">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th class="p-1 p-sm-2">Index</th>
              <th class="p-1 p-sm-2">0</th>
              <th class="p-1 p-sm-2">1</th>
              <th class="p-1 p-sm-2">2</th>
              <th class="p-1 p-sm-2">3</th>
              <th class="p-1 p-sm-2">4</th>
              <th class="p-1 p-sm-2">5</th>
              <th class="p-1 p-sm-2">6</th>
              <th class="p-1 p-sm-2">7</th>
              <th class="p-1 p-sm-2">8</th>
              <th class="p-1 p-sm-2">9</th>
              <th class="p-1 p-sm-2">10</th>
              <th class="p-1 p-sm-2">11</th>
              <th class="p-1 p-sm-2">12</th>
              <th class="p-1 p-sm-2">13</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="p-1 p-sm-2">Character</td>
              <td class="p-1 p-sm-2">P</td>
              <td class="p-1 p-sm-2">A</td>
              <td class="p-1 p-sm-2">Y</td>
              <td class="p-1 p-sm-2">P</td>
              <td class="p-1 p-sm-2">A</td>
              <td class="p-1 p-sm-2">L</td>
              <td class="p-1 p-sm-2">I</td>
              <td class="p-1 p-sm-2">S</td>
              <td class="p-1 p-sm-2">H</td>
              <td class="p-1 p-sm-2">I</td>
              <td class="p-1 p-sm-2">R</td>
              <td class="p-1 p-sm-2">I</td>
              <td class="p-1 p-sm-2">N</td>
              <td class="p-1 p-sm-2">G</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>

<div style="text-align: center;">
  <img src="/assets/images/leetcode/exe-6/jump.png" alt="leet_code_6_jump" class="img-fluid">
  <p class="text-muted">Hình 1: Bước nhảy</p>
</div>

Dựa theo ví dụ ta sẽ hình dung ra được n chính là số hàng sẽ được triển khai. Ứng với mỗi hàng ta sẽ tạo 1 StringBuilder để chứa các ký tự của hàng đó, tức là ta sẽ có 1 array của các StringBuilder.

Chúng ta sẽ tạo ra biến jump tăng/giảm current row. 

Khi đó ta có bảng mô tả như sau:
  - current row = 0 thì jump = 1
  - current row = n - 1 thì jump = -1
  - current row = current row + jump
<div class="container-fluid">
  <div class="row">
    <div class="col-12 col-md-8">
      <div class="table-responsive">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th class="p-1 p-sm-2">Index Character</th>
              <th class="p-1 p-sm-2">Character</th>
              <th class="p-1 p-sm-2">Current row</th>
              <th class="p-1 p-sm-2">Jump</th>
              <th class="p-1 p-sm-2">Index Row</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">P</td>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">StringBuilder[0].append(P)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">A</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">StringBuilder[1].append(A)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">Y</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">-1</td>
              <td class="p-1 p-sm-2">StringBuilder[2].append(Y)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">3</td>
              <td class="p-1 p-sm-2">P</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">-1</td>
              <td class="p-1 p-sm-2">StringBuilder[1].append(P)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">4</td>
              <td class="p-1 p-sm-2">A</td>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">StringBuilder[0].append(A)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">5</td>
              <td class="p-1 p-sm-2">L</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">StringBuilder[1].append(L)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">6</td>
              <td class="p-1 p-sm-2">I</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">-1</td>
              <td class="p-1 p-sm-2">StringBuilder[2].append(I)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">7</td>
              <td class="p-1 p-sm-2">S</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">-1</td>
              <td class="p-1 p-sm-2">StringBuilder[1].append(S)</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">8</td>
              <td class="p-1 p-sm-2">H</td>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">StringBuilder[0].append(H)</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>

Sau đó loop array StringBuilder lúc đầu thì sẽ ra được kết quả.

Source code tham khảo: [https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_6_Zigzag_Conversion](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_6_Zigzag_Conversion)