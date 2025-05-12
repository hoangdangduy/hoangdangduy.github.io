---
title:  "Linked list"
date:   2025-05-10 21:16:00 +0700
categories: data-structure
author: hoangdd
---
1. Đặt câu hỏi: Linked list là già?
Trả lời: Linked list là cấu trúc dữ liệu mô tả tính liên kết của phần tử thông qua vị trí tham chiếu trên bộ nhớ giúp cho việc thêm/xoá phần tử rất linh hoạt mà không tốn thêm nhiều bộ nhớ.

2. Có 2 loại linked list:
- Liên kết đơn (singly linked list): mỗi node sẽ có 1 con trỏ đến node tiếp theo
<div style="text-align: center;">
  <img src="/assets/images/linked-list/single-linked-list.png" alt="single-linked-list" class="img-fluid">
  <p class="text-muted">Hình 1: Liên kết đơn</p>
</div>

```java
public class LinkedList {
    private String key;
    private LinkedList next;

    // ignore getter and setter, constructor
}
```

- Liên kết đôi (doubly linked list): mỗi node sẽ có 2 con trỏ đến node trước và node sau
<div style="text-align: center;">
  <img src="/assets/images/linked-list/double-linked-list.png" alt="double-linked-list" class="img-fluid">
  <p class="text-muted">Hình 2: Liên kết đôi</p>
</div>

```java
public class LinkedList {
    private String key;
    private LinkedList next;
    private LinkedList prev;

    // ignore getter and setter, constructor
}
```

Ưu điểm:
- Không tốn bộ nhớ cho việc liên kết giữa các node như dùng mảng bởi vì nó chỉ dùng bộ nhớ để lưu con trỏ, còn mảng thì dùng bộ nhớ để lưu cả mảng.
- Độ phức tạp O(1) cho việc thêm vào và O(n) cho việc tìm kiếm

Nhược điểm:
- Không truy cập nhanh đến các node, phải duyệt lần lượt với độ phức tạp là O(n)

3. Các dạng bài toán áp dụng được linked list:

3.1. Triển khi stack [[Tham khảo source code]](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Book/Introduction_To_Algorithms/src/_10_2_2)
<div style="text-align: center;">
  <img src="/assets/images/linked-list/stack.png" alt="stack" class="img-fluid">
  <p class="text-muted">Hình 3: Stack</p>
</div>
 + Con trỏ head luôn ở đầu bất kể phần tử nào được thêm mới vào. Mỗi phân từ sau được thêm vào sẽ luôn là head và trỏ đến phần tử vào trước nó (phần tử tiếp theo)

3.2. Triển khai queue [[Tham khảo source code]](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Book/Introduction_To_Algorithms/src/_10_2_3)
<div style="text-align: center;">
  <img src="/assets/images/linked-list/queue.png" alt="queue" class="img-fluid">
  <p class="text-muted">Hình 4: Queue</p>
</div>
 + Con trỏ head và tail luôn ở 2 đầu để queue lấy được ở cả 2 đầu

3.3. Triển khai doubly linked list bằng toán tử XOR [[Tham khảo source code]](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Book/Introduction_To_Algorithms/src/_10_2_6)

3.4. Các bài toán tham khảo khác:
- [Leet code: Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/) 
  + [Đáp án](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/Leetcode/src/_2_Add_Two_Number)
 