# 【Leetcode刷题笔记】6 Z字形变换

## 题目描述

- - 将一个给定字符串 `s` 根据给定的行数 `numRows` ，以从上往下、从左到右进行 Z 字形排列。

    比如输入字符串为 `"PAYPALISHIRING"` 行数为 `3` 时，排列如下：

    ```
    P   A   H   N
    A P L S I I G
    Y   I   R
    ```
  
    之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"PAHNAPLSIIGYIR"`。
  
    请你实现这个将字符串进行指定行数变换的函数：
  
    ```
    string convert(string s, int numRows);
    ```
  
    
  
    **示例 1：**
  
    ```
    输入：s = "PAYPALISHIRING", numRows = 3
    输出："PAHNAPLSIIGYIR"
    ```
  
    **示例 2：**
  
    ```
    输入：s = "PAYPALISHIRING", numRows = 4
    输出："PINALSIGYAHRPI"
    解释：
    P     I    N
    A   L S  I G
    Y A   H R
    P     I
    ```
  
    **示例 3：**
  
    ```
    输入：s = "A", numRows = 1
    输出："A"
    ```

    

    **提示：**
  
    - `1 <= s.length <= 1000`
    - `s` 由英文字母（小写和大写）、`','` 和 `'.'` 组成
    - `1 <= numRows <= 1000`

## 题解

思路就是，创建一个二维字符数组来存放Z字形字符，然后遍历原字符串，计算出每个字符相应位置。然后遍历二维字符数组一次即可。

``` java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows==1){
            return s;
        }
        int n = s.length();
        char[] ss = s.toCharArray();
        int T = numRows * 2 - 2;
        int numT = n / T + 1;
        char[][] res = new char[numRows][numT*(numRows-1)];

        for (int i = 0; i < n; i++) {
            int row = i % T > T / 2 ? T - i % T : i % T;
            int col = i / T * (T - numRows + 1) + (i % T > T / 2 ? i % T - T / 2 : 0);
            res[row][col]=ss[i];
        }
        StringBuffer ans=new StringBuffer();
        for (int i = 0; i < numRows; i++) {
            for (int j = 0; j < numT * (numRows - 1); j++) {
                if (res[i][j]!='\0'){
                    ans.append(res[i][j]);
                }
            }
        }
        return ans.toString();
    }
}
```

**复杂度**

空间复杂度O(n+numrows * (n/(numrows*2-2))

时间复杂度O(numrows * (n/(numrows*2-2))

