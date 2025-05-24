---
title:  "Leet code 5: Tìm xâu đối xứng dài nhất"
date:   2025-05-18 22:40:00 +0700
categories: leet-code algorithm
author: hoangdd
---
Bài toán: Tìm xâu đối xứng dài nhất

[https://leetcode.com/problems/longest-palindromic-substring/description/](https://leetcode.com/problems/longest-palindromic-substring/description/)

Ý tưởng giải quyết bài toán là ta sẽ coi các điểm cần duyệt trong xâu là điểm giữa của xâu đối xứng, sau đó sẽ phát triển duyệt sang 2 bên và check thêm các điều kiện để dừng.

Ví dụ với xâu `abcba` thì ta sẽ duyệt các bước như sau:

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
              <th class="p-1 p-sm-2">5</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="p-1 p-sm-2">Character</td>
              <td class="p-1 p-sm-2">a</td>
              <td class="p-1 p-sm-2">b</td>
              <td class="p-1 p-sm-2">c</td>
              <td class="p-1 p-sm-2">b</td>
              <td class="p-1 p-sm-2">a</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>

<div class="container-fluid">
  <div class="row">
    <div class="col-12 col-md-10">
      <div class="table-responsive">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th class="p-1 p-sm-2">Index</th>
              <th class="p-1 p-sm-2">start</th>
              <th class="p-1 p-sm-2">traverse left</th>
              <th class="p-1 p-sm-2">traverse right</th>
              <th class="p-1 p-sm-2">palindromic</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td class="p-1 p-sm-2">0</td>
              <td class="p-1 p-sm-2">a</td>
              <td class="p-1 p-sm-2">NULL</td>
              <td class="p-1 p-sm-2">b</td>
              <td class="p-1 p-sm-2">false</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">1</td>
              <td class="p-1 p-sm-2">b</td>
              <td class="p-1 p-sm-2">a</td>
              <td class="p-1 p-sm-2">c</td>
              <td class="p-1 p-sm-2">false</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">2</td>
              <td class="p-1 p-sm-2">c</td>
              <td class="p-1 p-sm-2">ab</td>
              <td class="p-1 p-sm-2">ba</td>
              <td class="p-1 p-sm-2">true</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">3</td>
              <td class="p-1 p-sm-2">b</td>
              <td class="p-1 p-sm-2">c</td>
              <td class="p-1 p-sm-2">a</td>
              <td class="p-1 p-sm-2">false</td>
            </tr>
            <tr>
              <td class="p-1 p-sm-2">4</td>
              <td class="p-1 p-sm-2">a</td>
              <td class="p-1 p-sm-2">b</td>
              <td class="p-1 p-sm-2">NULL</td>
              <td class="p-1 p-sm-2">false</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>

Xâu đối xứng dài nhất tìm được là `abcba`

Với ví dụ trên ta sẽ triển khai được code giải thuật như sau:

```java
    public String longestPalindrome(String s) {
        String result = "";
        for (int i = 0; i < s.length(); i++) {
            result = longestPalindrome(s, i, i, result);
            result = longestPalindrome(s, i, i+1, result);
        }
        return result;
    }

    private static String longestPalindrome(String s, int left, int right, String result) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        left++;
        right--;
        if ((right - left + 1) > result.length()) {
            result = s.substring(left, right + 1);
        }
        return result;
    }
```

Độ phức tạp của thuật toán là O(n^2)

Source code tham khảo: [https://github.com/hoangdangduy/System_Patterns_Algorithm/blob/Master/Leetcode/src/_5_Longest_Palindromic_Substring/Solution.java](https://github.com/hoangdangduy/System_Patterns_Algorithm/blob/Master/Leetcode/src/_5_Longest_Palindromic_Substring/Solution.java)