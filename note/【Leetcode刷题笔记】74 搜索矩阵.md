# 【Leetcode刷题笔记】74 搜索矩阵

## 题目描述

编写一个高效的算法来判断 `m x n` 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
输出：true
```

**示例 2：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/mat2.jpg)

```
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
输出：false
```



**提示：**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `-104 <= matrix[i][j], target <= 104`

## 题解

从矩阵右上角为根，发现根的左节点都小于根值，根的下节点都大于根值，这可以抽象成一棵BST

java代码如下

``` java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int height = matrix.length;
        int row = 0, col = matrix[0].length - 1;
        while (row != height && col != -1) {
            if (matrix[row][col] == target) {
                return true;
            } else if (target > matrix[row][col]) {
                row++;
            } else if (target < matrix[row][col]) {
                col--;
            }
        }
        return false;
    }
}

```

**复杂度**

空间复杂度 O(1)

时间复杂度O (logmn)