---
title:  "Leet code: Tính trung vị của 2 mảng đã được sắp xếp"
date:   2025-05-16 24:29:00 +0700
categories: leet-code algorithm
author: hoangdd
---
Bài toán: Tìm giá trị trung vị của 2 mảng đã được sắp xếp

[https://leetcode.com/problems/median-of-two-sorted-arrays/](https://leetcode.com/problems/median-of-two-sorted-arrays/)

## 1. Tiếp cận bài toán hướng đơn giản

Vì 2 mảng đã sắp xếp nên chúng ta có thể duyệt 2 mảng lần lượt từ trái qua phải hoặc từ phải qua trái, sau đó so sánh từng giá trị với nhau và lưu lại vào mảng mới.

Khi có mảng mới, nếu:
- mảng có lẻ phần tử thì lấy `s3.length/2` là giá trị cần tìm.
- mảng có chẵn phần tử thì lấy `((s3.length/2 - 1) + s3.length/2) / 2` là giá trị cần tìm.

Ta sẽ có được giải thuật như sau:

```text
  i = s1.length - 1
  j = s2.length - 1
  
  s3 = [s1.length + s2.length]
  k = s3.length
  
  while (i >= 0 && j >= 0) {
      if (s1[i] > s2[j]) {
          s3[k] = s1[i];
          i--;
      } else {
          s3[k] = s1[j];
          j--;
      }
  }
  
  double result;
  if (s3.length % 2 == 0) {
      result = (s3[s3.length/2 - 1] + s3[s3.length/2]) / 2;
  } else {
      result = s3[s3.length/2];
  }
```

Với đoạn code trên ta có thể thấy i chạy từ `0 -> s1.length`, j chạy từ `0 -> s2.length` tức là độ phức tạp của thuật toán là O(max(n,m)) với n là độ dài của mảng s1 và m là độ dài của mảng s2.

## 2. Tiếp cận bài toán hướng tối ưu

Vì 2 mảng này đã được sắp xếp rồi thì có thể áp dụng hướng tiếp cận binary search để chia mảng là 2 phần.

giả sử ta có mảng

<div class="container-fluid">
  <div class="row">
    <div class="col-md-12 col-lg-10">
      <div class="table-responsive">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th class="p-1 p-sm-2">index</th>
              <th class="p-1 p-sm-2">0</th>
              <th class="p-1 p-sm-2">1</th>
              <th class="p-1 p-sm-2">2</th>
              <th class="p-1 p-sm-2">3</th>
              <th class="p-1 p-sm-2">4</th>
              <th class="p-1 p-sm-2">5</th>
              <th class="p-1 p-sm-2">6</th>
              <th class="p-1 p-sm-2">7</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="p-1 p-sm-2">s1</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">3</td>
              <td class="p-1 p-sm-2">5</td>
              <td class="p-1 p-sm-2">6</td>
              <td class="p-1 p-sm-2">7</td>
              <td class="p-1 p-sm-2">9</td>
              <td class="p-1 p-sm-2"></td>
              <td class="p-1 p-sm-2"></td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">s2</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">3</td>
              <td class="p-1 p-sm-2">4</td>
              <td class="p-1 p-sm-2">4</td>
              <td class="p-1 p-sm-2">4</td>
              <td class="p-1 p-sm-2">8</td>
              <td class="p-1 p-sm-2">10</td>
              <td class="p-1 p-sm-2">12</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>

Ta sẽ chia mảng s1 thành 2 phần với index vị trí giữa là partition1, mảng s2 thành 2 phần với index vị trí giữa là partition2.

Tạo sẵn biến:
- `low = 0`
- `high = s1.length`

[A] Ta sẽ lấy:
- `partition1 = (low + high) / 2` để chia mảng s1 thành 2 phần
  + partition1 = (0 + 6) / 2 = 3
- `partition2 = (s1.length + s2.length + 1) / 2 - partition1` để chia mảng s2 thành 2 phần
  + partition2 = (6 + 8 + 1) / 2 - 3 = 4

Ý tưởng là sẽ chia mảng `s1 ∪ s2` nên ở s1 đã lấy số lượng partition1 phần tử thì ở s2 lấy một nửa của `s1 ∪ s2` trừ đi số lượng partition1

Khi tìm được partition1 và partition2 ta sẽ kiểm tra giá trị của nó và lân cận nó so với vị trí ở mảng còn lại đã thoả mã 2 vị trí ở chính giữa chưa.

coi:
- `maxLeft1 = s1[partition1 - 1] = s[3-1] = 5` là giá trị lớn nhất bên trái của partition1
  + mảng bên trái của s1: [1, 3, 5]
- `minRight1 = s1[partition1] = s[3] = 6` là giá trị nhỏ nhất bên phải của partition1
  + mảng bên phải của s1: [6, 7, 9]
- `maxLeft2 = s2[partition2 - 1] = s[4-1] = s[3] = 4` là giá trị lớn nhất bên trái của partition2
  + mảng bên trái của s2: [2, 3, 4, 4]
- `minRight2 = s2[partition2] = s[4] = 4` là giá trị nhỏ nhất bên phải của partition2
  + mảng bên phải của s2: [4, 8, 10, 12]

nếu:
- `maxLeft1 <= minRight2 && maxLeft2 <= minRight1` thì ta đã tìm được vị trí chia mảng
- `maxLeft1 > minRight2` tức là bên trái đang nhiều phần tử hơn, cần giảm partition1
  + set `high = partition1 - 1`
- `maxLeft2 > minRight1` tức là bên phải đang nhiều phần tử hơn, cần tăng partition1
  + set `low = partition1 + 1`

Nếu chưa tìm được vị trí chia mảng thì quay lại bước [A] để tìm lại partition1 và partition2, ngược lại nhảy đến bước [B]

[B] Tính giá trị trung vị
- Nếu số phần tử lẻ thì trả về max(maxLeft1, maxLeft2)
- Nếu số phần tử chẵn thì trả về (max(maxLeft1, maxLeft2) + min(minRight1, minRight2)) / 2

Áp dụng vào ví dụ trên ta có bảng các bước chi tiết như sau:

<div class="container-fluid">
  <div class="row">
    <div class="col-md-12 col-lg-10">
      <div class="table-responsive">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th class="p-1 p-sm-2"><b>step</b></th>
              <th class="p-1 p-sm-2"><b>low</b></th>
              <th class="p-1 p-sm-2"><b>high</b></th>
              <th class="p-1 p-sm-2"><b>partition1</b></th>
              <th class="p-1 p-sm-2"><b>partition2</b></th>
              <th class="p-1 p-sm-2"><b>left s1 ___ right s1</b></th>
              <th class="p-1 p-sm-2"><b>left s2 ___ right s2</b></th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">6</td>
              <td class="p-1 p-sm-2">3</td>
              <td class="p-1 p-sm-2">4</td>
              <td class="p-1 p-sm-2">1, 3, 5 ___ 6, 7, 9</td>
              <td class="p-1 p-sm-2">2, 3, 4, 4 ___ 4, 8, 10, 12</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">6</td>
              <td class="p-1 p-sm-2">1 ___ 3, 5, 6, 7, 9</td>
              <td class="p-1 p-sm-2">2, 3, 4, 4, 4, 8 ___ 10, 12</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">3</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">5</td>
              <td class="p-1 p-sm-2">1, 3 ___ 5, 6, 7, 9</td>
              <td class="p-1 p-sm-2">2, 3, 4, 4, 4 ___ 8, 10, 12</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>

Từ các phân tích trên ta có đoạn code cụ thể như sau:

```java
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1.length < nums2.length) {
            return findMedianSortedArrays(nums1, nums2, 0, nums1.length);
        } else {
            return findMedianSortedArrays(nums2, nums1, 0, nums2.length);
        }
    }

    public double findMedianSortedArrays(int[] s1, int[] s2, int low, int high) {
        int partition1 = (low + high)/2;
        int partition2 = (s1.length + s2.length + 1)/2 - partition1;

        int maxLeft1 = partition1 == 0 ? maxLeft1 = Integer.MIN_VALUE : s1[partition1-1];
        int minRight1 = partition1 < s1.length ? s1[partition1] : Integer.MAX_VALUE;
        int maxLeft2 = partition2 == 0 ? Integer.MIN_VALUE : s2[partition2-1];
        int minRight2 = partition2 < s2.length ? s2[partition2] : Integer.MAX_VALUE;

        if (maxLeft1 > minRight2) {
            high = partition1 - 1;
            return findMedianSortedArrays(s1, s2, low, high);
        } else if (maxLeft2 > minRight1) {
            low = partition1 + 1;
            return findMedianSortedArrays(s1, s2, low, high);
        } else {
            if ((s1.length + s2.length) % 2 != 0) {
                return Math.max(maxLeft1, maxLeft2);
            } else {
                return (double) (Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2;
            }
        }
    }
```

Vì áp dụng giải thuật binary search nên độ phức tạp chỉ là O(log(min(n,m))).

Source code tham khảo: [https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_4_Median_of_Two_Sorted_Arrays](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_4_Median_of_Two_Sorted_Arrays/)