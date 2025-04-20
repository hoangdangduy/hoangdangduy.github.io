---
title:  "Thiết kế lưu trữ dữ liệu phân tán với Consistency Hashing"
date:   2025-04-19 15:40:00 +0700
categories: design-system
author: hoangdd
---

Việc lưu trữ dữ liệu dạng single server hay còn gọi monolitic là một cách tiếp cận đơn giản và dễ dàng để triển khai. Tuy nhiên, khi dữ liệu ngày càng lớn, việc mở rộng quy mô trở thành một thách thức lớn, vậy làm sao để làm giảm công việc chỉnh sửa lại vị trí lưu dữ liệu khi tăng/giảm số server?. Để giải quyết vấn đề này, chúng ta cần một cách tiếp cận phân tán hơn, cho phép chúng ta mở rộng quy mô mà không làm giảm hiệu suất. Do đó, consistency hashing là một trong nhiều cách tiếp cận để giải quyết bài toán đó.

Đầu tiên chúng ta cần phải hiểu consistency hashing là gì?

Consistency hashing là cách triển khai hash (băm) các giá trị theo cách thống nhất để lưu trữ và nhận dữ liệu hiệu quả.  

Giả sử chúng ta có 3 server có tên là s1, s2 và s3.

<div style="text-align: center;">
  <img src="/assets/images/consistency-hashing/consitency-hashing-1.png" alt="consitency-hashing-1" class="img-fluid">
  <p class="text-muted">Hình 1: Mô hình triển khai</p>
</div>

Thêm 3 server vào hệ thống để lưu trữ dữ liệu

Mỗi server sẽ có 1 giá trị hash khác nhau, ta sẽ quy ước là hash(server), có thể lấy địa chỉ IP của server miễn sao đảm bảo nó là duy nhất.

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

<div style="text-align: center;">
  <img src="/assets/images/consistency-hashing/consitency-hashing-2.png" alt="consitency-hashing-2" class="img-fluid">
  <p class="text-muted">Hình 2: Phân phối dữ liệu vào server</p>
</div>

### Example code:
```java
// Lưu dữ liệu vào server
public static void saveData(String key, String data) {
    getNode(key).getDataStore().put(key, data);
}

// Tìm ra server đã lưu dữ liệu
public static Storage getNode(String key) {
    var hash = HashingStrategy.generateHash(key);
    var result = mapConsistencyHashing.tailMap(hash);
    if (result.isEmpty()) {
        var map = mapConsistencyHashing.headMap(hash);
        var firstKey = map.firstKey();
        return map.get(firstKey);
    }
    var firstKey = result.firstKey();
    return result.get(firstKey);
}
```


Như ví dụ ở trên, chúng ta thấy s1 thì không có dữ liệu nào được lưu trữ vào còn s2 lại lưu cả x và y. Để giải quyết vấn đề này chúng ta sẽ thêm các node ảo của server gọi là virtual node để tăng xác suất lưu trữ đều vào các server vật lý, tránh tập trung lưu trữ chỉ tại một nơi.

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

<div style="text-align: center;">
  <img src="/assets/images/consistency-hashing/consitency-hashing-3.png" alt="consitency-hashing-3" class="img-fluid">
  <p class="text-muted">Hình 3: Phân phối dữ liệu sau khi thêm virtual node</p>
</div>

### Example code:
```java
// Khởi tạo các server
ConsistencyHashing.addServer(new Storage("server-1", new ConcurrentHashMap<>()));
ConsistencyHashing.addServer(new Storage("server-2", new ConcurrentHashMap<>()));
ConsistencyHashing.addServer(new Storage("server-3", new ConcurrentHashMap<>()));

// Mỗi server vật lý sẽ chuyển sang tạo virtual node tương ứng
public static void addServer(Storage storage) {
    for(int i = 0; i < VIRTUAL_NODE; i++) {
        var hash = HashingStrategy.generateHash(storage.getName().concat("-").concat(String.valueOf(i)));
        mapConsistencyHashing.put(hash, storage);
    }
}
```

Như vậy với ý tưởng này chúng ta đã giải quyết được cách lưu trữ dữ liệu trong hệ thống phân tán.

Để hiểu cách thức triển khai và nắm rõ hơn về cách áp dụng thì các bạn có thể suy nghĩ thêm các câu hỏi mở rộng:
- Khi thêm 1 server mới vào mô hình trên thì các dữ liệu đã được gán vào server cũ sẽ phân phối lại như nào?

Source code tham khảo: [https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/consistency_hashing](https://github.com/hoangdangduy/System_Patterns_Algorithm/tree/Master/consistency_hashing)