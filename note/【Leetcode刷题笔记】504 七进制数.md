# 【Leetcode刷题笔记】504 七进制数

## 题目描述

- 给定一个整数 `num`，将其转化为 **7 进制**，并以字符串形式输出。

  

  - **示例 1:**
  
    ```
    输入: num = 100
    输出: "202"
    ```

    **示例 2:**

    ```
    输入: num = -7
    输出: "-10"
    ```
  
    
  
    **提示：**
  
    - `-107 <= num <= 107`
  
    Related Topics
  
    数学

## 题解

连除即可。 由于需要转换成字符串，需要注意数字的正负。

``` java
class Solution {
    public String convertToBase7(int num) {
        int tmp=num;
        if(num==0){
            return "0";
        }
        num=Math.abs(num);
        StringBuffer res=new StringBuffer();
        while (num!=0){
            res.append(num%7);
            num/=7;
        }
        if(tmp<0){
            res.append('-');
        }

        return res.reverse().toString();
    }
}
```

**复杂度**

空间复杂度O(C) C为除尽num的次数。

时间复杂度O(1)

