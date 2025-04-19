---
title:  "Thiết kế lưu trữ dữ liệu phân tán với Consistency Hashing"
date:   2025-04-19 15:40:00 +0700
categories: design_system
---

Việc lưu trữ dữ liệu dạng single server hay còn gọi monolitic là một cách tiếp cận đơn giản và dễ dàng để triển khai. Tuy nhiên, khi dữ liệu ngày càng lớn, việc mở rộng quy mô trở thành một thách thức lớn. Để giải quyết vấn đề này, chúng ta cần một cách tiếp cận phân tán hơn, cho phép chúng ta mở rộng quy mô mà không làm giảm hiệu suất. Do đó, consistency hashing là một trong nhiều cách tiếp cận để giải quyết bài toán đó.

Đầu tiên chúng ta cần phải hiểu consistency hashing là gì?

Hiểu đơn giản ở ngay tên gọi là cách băm (hash) các giá trị theo một cách chung để lưu trữ lại cũng như lấy ra.

Vậy khi làm như thế chúng ta sẽ điều hướng được data cần lưu vào những server mong muốn.

Giả sử chúng ta có 3 server có tên là s1, s2 và s3.

![consitency-hashing-1.png]({{ site.baseurl }}/assets/images/consistency-hashing/consitency-hashing-1.png)

Mỗi server sẽ có 1 giá trị hash khác nhau, ta sẽ quy ước là hash(server) , có thể lấy địa chỉ IP của server miễn sao đảm bảo nó là duy nhất.

Khi dữ liệu được insert vào server thì chúng cũng sẽ được hash(data) và so sánh với value hash của server. Ta sẽ tìm được server có giá trị hash gần với hash(data) nhất.

Ví dụ:
- hash server:
    + hash(s1) = 10
    + hash(s2) = 20
    + hash(s3) = 30
- hash data:
  - hash(x) = 15
  - hash(y) = 17
  - hash(z) = 25
Ta sẽ lưu được x và y vào s2, z vào s3.

![consitency-hashing-2.png]({{ site.baseurl }}/assets/images/consistency-hashing/consitency-hashing-2.png)

Như ví dụ ở trên, chúng ta thấy s1 thì không có dữ liệu nào được lưu trữ vào còn s2 lại lưu cả x và y. Để giải quyết vấn đề này chúng ta sẽ thêm các node ảo của server gọi là virtual node để tăng xác suất lưu trữ đều vào các server.

Mỗi server sẽ tạo thành 2 virtual node và hash(virtual_node) như cách làm với node.
Ta sẽ có:
- hash virtual node của s1
    + hash(s1_v1) = 11
    + hash(s1_v2) = 16
- hash virtual node của s2
-   + hash(s2_v1) = 21
    + hash(s2_v2) = 24
- hash virtual node của s3
-   + hash(s3_v1) = 26
    + hash(s3_v2) = 31

Sau khi có virtual thì dữ liệu sẽ được phân phối lại như sau:

![consitency-hashing-3.png]({{ site.baseurl }}/assets/images/consistency-hashing/consitency-hashing-3.png)

Như vậy với ý tưởng này chúng ta đã giải quyết được cách lưu trữ dữ liệu trong hệ thống phân tán.

Để hiểu cách thức triển khai và nắm rõ hơn về cách áp dụng thì các bạn có thể suy nghĩ thêm các câu hỏi mở rộng:
- Khi thêm 1 server mới vào mô hình trên thì các dữ liệu đã được gán vào server cũ sẽ phân phối lại như nào?