# 【Leetcode刷题笔记】917 仅仅反转字母

## 题目描述

**难度**    `hard`

- 给你一个字符串 `s` ，根据下述规则反转字符串：

  - 所有非英文字母保留在原有位置。
  - 所有英文字母（小写或大写）位置反转。

  返回反转后的 `s` *。*

  **示例 1：**

  ```
  输入：s = "ab-cd"
  输出："dc-ba"
  ```

  

  **示例 2：**

  ```
  输入：s = "a-bC-dEf-ghIj"
  输出："j-Ih-gfE-dCba"
  ```

  

  **示例 3：**

  ```
  输入：s = "Test1ng-Leet=code-Q!"
  输出："Qedo1ct-eeLg=ntse-T!"
  ```

  

  **提示**

  - `1 <= s.length <= 100`
  - `s` 仅由 ASCII 值在范围 `[33, 122]` 的字符组成
  - `s` 不含 `'\"'` 或 `'\\'`

## 题解

我们知道翻转字符串的代码往往采用双指针这样写

``` java
int i=0,j=n-1;
while(i<j){
	swap(i,j,s);
    i++;
    j--;
}
```

这道题要求只对字母进行翻转，因而在指针遇到非字母字符直接跳过即可，遇到字母时直接翻转即可。

## 代码

``` java
class Solution {
    public String reverseOnlyLetters(String s) {
        char[] sa = s.toCharArray();
        int n = sa.length;
        int i = 0, j = n - 1;
        while (i < j) {
            while (!((sa[i] >= 'a' && sa[i] <= 'z') || (sa[i] >= 'A' && sa[i] <= 'Z')) && i < j) {
                i++;
            }
            while (!((sa[j] >= 'a' && sa[j] <= 'z') || (sa[j] >= 'A' && sa[j] <= 'Z')) && i < j) {
                j--;
            }
            if (i < j) {
                char tmp = sa[i];
                sa[i] = sa[j];
                sa[j] = tmp;
                i++;
                j--;
            }
        }
        return new String(sa);
    }
}
```

