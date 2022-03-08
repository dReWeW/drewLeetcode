# 【Leetcode刷题笔记】2055 蜡烛之间的盘子

## 题目描述

- 给你一个长桌子，桌子上盘子和蜡烛排成一列。给你一个下标从 **0** 开始的字符串 `s` ，它只包含字符 `'*'` 和 `'|'` ，其中 `'*'` 表示一个 **盘子** ，`'|'` 表示一支 **蜡烛** 。

  同时给你一个下标从 **0** 开始的二维整数数组 `queries` ，其中 `queries[i] = [lefti, righti]` 表示 **子字符串** `s[lefti...righti]` （**包含左右端点的字符**）。对于每个查询，你需要找到 **子字符串中** 在 **两支蜡烛之间** 的盘子的 **数目** 。如果一个盘子在 **子字符串中** 左边和右边 **都** 至少有一支蜡烛，那么这个盘子满足在 **两支蜡烛之间** 。

  - 比方说，`s = "||**||**|*"` ，查询 `[3, 8]` ，表示的是子字符串 `"*||***\**\***|"` 。子字符串中在两支蜡烛之间的盘子数目为 `2` ，子字符串中右边两个盘子在它们左边和右边 **都** 至少有一支蜡烛。
  
  请你返回一个整数数组 `answer` ，其中 `answer[i]` 是第 `i` 个查询的答案。

  
  
  **示例 1:**
  
  ![ex-1](https://assets.leetcode.com/uploads/2021/10/04/ex-1.png)
  
  ```
  输入：s = "**|**|***|", queries = [[2,5],[5,9]]
  输出：[2,3]
  解释：
  - queries[0] 有两个盘子在蜡烛之间。
  - queries[1] 有三个盘子在蜡烛之间。
  ```
  
  **示例 2:**
  
  ![ex-2](https://assets.leetcode.com/uploads/2021/10/04/ex-2.png)
  
  ```
  输入：s = "***|**|*****|**||**|*", queries = [[1,17],[4,5],[14,17],[5,11],[15,16]]
  输出：[9,0,0,0,0]
  解释：
  - queries[0] 有 9 个盘子在蜡烛之间。
  - 另一个查询没有盘子在蜡烛之间。
  ```
  
  
  
  **提示：**
  
  - `3 <= s.length <= 105`
  - `s` 只包含字符 `'*'` 和 `'|'` 。
  - `1 <= queries.length <= 105`
  - `queries[i].length == 2`
  - `0 <= lefti <= righti < s.length`

## 题解

这道题是经典的前缀和问题。

根据题我们可以很容易得知只需找到左边第一个蜡烛left和右边第一个蜡烛right之间的蜡烛即可。我们可以用preSum[i]表示i之前的蜡烛数量，因而[left,right]之间的蜡烛数为preSum[right]-preSum[left]

left数组通过从后往前遍历求得

right数组从前往后遍历即可。

## 代码

```java
class Solution {
    public int[] platesBetweenCandles(String s, int[][] queries) {
        char[] as = s.toCharArray();
        int n = as.length;
        int[] preSum = new int[n];
        int[] answer = new int[queries.length];
        int[] left = new int[n];
        int[] right = new int[n];

        for (int i = 0, sum = 0; i < n; i++) {
            if (as[i] == '*') {
                sum++;
            }
            preSum[i] = sum;
        }
        for (int i = n - 1, leftCandle = n - 1; i >= 0; i--) {
            if (as[i] == '|') {
                leftCandle = i;
            }
            left[i] = leftCandle;
        }
        for (int i = 0, rightCandle = 0; i < n; i++) {
            if (as[i] == '|') {
                rightCandle = i;
            }
            right[i] = rightCandle;
        }
        for (int i = 0; i < queries.length; i++) {
            int ans = preSum[right[queries[i][1]]] - preSum[left[queries[i][0]]];
            if (ans >= 0)
                answer[i] = ans;
            else
                answer[i] = 0;
        }
        return answer;
    }
}
```

**复杂度**

空间复杂度O(n+C) c为queries.length

时间复杂度O(n)

