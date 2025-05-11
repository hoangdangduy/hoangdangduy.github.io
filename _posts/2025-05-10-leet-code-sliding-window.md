---
title:  "Leet code: tìm độ dài xâu con dài nhất không bị trùng lặp"
date:   2025-05-10 21:16:00 +0700
categories: leet-code algorithm
author: hoangdd
---

Bài toán: Tìm độ dài xâu con dài nhất không bị trùng lặp

[https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Giả sử có string là **abcabccbc**, chúng ta cần phải tìm độ dài của xâu con dài nhất không bị trùng lặp.

Tiếp cận bài toán này chúng ta có thể áp dụng giải thuật sliding window + hash map với độ phức tạp là O(n) với n là độ dài của string.

Các bước phân tích lời giải bài toán:
- Cần lưu được độ dài của xâu đang xét nên chúng ta cần biến left và right để xác định xâu con
- Sử dụng Map để lưu lại vị trí của các ký tự trong xâu
- Giá trị độ dài lớn nhất của xâu con

<div class="container-fluid">
    <div class="row">
      <div class="col-12 col-md-6">
        <div class="table-responsive">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th class="p-1 p-sm-2">Character</th>
                <th class="p-1 p-sm-2">a</th>
                <th class="p-1 p-sm-2">b</th>
                <th class="p-1 p-sm-2">c</th>
                <th class="p-1 p-sm-2">a</th>
                <th class="p-1 p-sm-2">b</th>
                <th class="p-1 p-sm-2">c</th>
                <th class="p-1 p-sm-2">c</th>
                <th class="p-1 p-sm-2">b</th>
                <th class="p-1 p-sm-2">c</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td class="p-1 p-sm-2">Index</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">1</td>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">4</td>
                <td class="p-1 p-sm-2">5</td>
                <td class="p-1 p-sm-2">6</td>
                <td class="p-1 p-sm-2">7</td>
                <td class="p-1 p-sm-2">8</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

<div class="container-fluid">
    <div class="row">
      <div class="col-12 col-md-6">
        <div class="table-responsive">
          <table class="table table-bordered">
            <thead>
              <tr>
                <th class="p-1 p-sm-2">Step</th>
                <th class="p-1 p-sm-2">Left</th>
                <th class="p-1 p-sm-2">Right</th>
                <th class="p-1 p-sm-2">Map</th>
                <th class="p-1 p-sm-2">Length</th>
                <th class="p-1 p-sm-2">Sub string</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td class="p-1 p-sm-2">1</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">a:0</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">a</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">1</td>
                <td class="p-1 p-sm-2">a:0; b:1</td>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">ab</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">a:0; b:1; c:2</td>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">abc</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">4</td>
                <td class="p-1 p-sm-2">0</td>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">a:3; b:1; c:2</td>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">bca</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">5</td>
                <td class="p-1 p-sm-2">1</td>
                <td class="p-1 p-sm-2">4</td>
                <td class="p-1 p-sm-2">a:3; b:4; c:2</td>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">cab</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">6</td>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">5</td>
                <td class="p-1 p-sm-2">a:3; b:4; c:5</td>
                <td class="p-1 p-sm-2">3</td>
                <td class="p-1 p-sm-2">abc</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">7</td>
                <td class="p-1 p-sm-2">5</td>
                <td class="p-1 p-sm-2">6</td>
                <td class="p-1 p-sm-2">a:3; b:4; c:6</td>
                <td class="p-1 p-sm-2">1</td>
                <td class="p-1 p-sm-2">c</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">8</td>
                <td class="p-1 p-sm-2">6</td>
                <td class="p-1 p-sm-2">7</td>
                <td class="p-1 p-sm-2">a:3; b:7; c:6</td>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">cb</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">9</td>
                <td class="p-1 p-sm-2">6</td>
                <td class="p-1 p-sm-2">8</td>
                <td class="p-1 p-sm-2">a:3; b:7; c:8</td>
                <td class="p-1 p-sm-2">2</td>
                <td class="p-1 p-sm-2">bc</td>
              </tr>
              <tr>
                <td class="p-1 p-sm-2">10</td>
                <td class="p-1 p-sm-2">8</td>
                <td class="p-1 p-sm-2">9</td>
                <td class="p-1 p-sm-2"></td>
                <td class="p-1 p-sm-2"></td>
                <td class="p-1 p-sm-2"></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

Giải thuật:
- loop: right chạy từ 0 -> length của xâu s
  - check s[right] có trong map
    - có: 
      - left = map[s[right]] + 1
      - length = right - map[s[right]]
    - không: 
      - length = right - left + 1
  - cập nhật s[right] vào map
  - right tăng lên 1

Triển khai giải thuật trên ta có được code như sau:
### Example code:
```java
public int lengthOfLongestSubstringOld(String s) {
    int left = 0;
    int right = 0;
    int max = 0;
    Map<Character, Integer> map = new HashMap<>();

    while (right < s.length()) {
        int length;
        if (map.containsKey(s.charAt(right)) && map.get(s.charAt(right)) >= left) {
            length = right - map.get(s.charAt(right));
            left = map.get(s.charAt(right)) + 1;
        } else {
            length = right - left + 1;
        }
        map.put(s.charAt(right), right);
        max = Math.max(max, length);

        right++;
    }
    return max;
}
```

Tối ưu để clean code
### Example code:
```java
public int lengthOfLongestSubstring(String s) {
    int left = 0;
    int right = 0;
    int max = 0;
    Map<Character, Integer> map = new HashMap<>();

    while (right < s.length()) {
        char c = s.charAt(right);
        if (map.containsKey(c) && map.get(c) >= left) {
            left = map.get(c) + 1;
        }
        map.put(c, right);
        max = Math.max(max, right - left + 1);
        right++;
    }
    return max;
}
```
