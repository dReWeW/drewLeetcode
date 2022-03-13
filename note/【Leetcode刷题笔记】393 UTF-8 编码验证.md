# 【Leetcode刷题笔记】393 UTF-8 编码验证

## 题目描述

- 给定一个表示数据的整数数组 `data` ，返回它是否为有效的 **UTF-8** 编码。

  **UTF-8** 中的一个字符可能的长度为 **1 到 4 字节**，遵循以下的规则：

  1. 对于 **1 字节** 的字符，字节的第一位设为 0 ，后面 7 位为这个符号的 unicode 码。
  2. 对于 **n 字节** 的字符 (n > 1)，第一个字节的前 n 位都设为1，第 n+1 位设为 0 ，后面字节的前两位一律设为 10 。剩下的没有提及的二进制位，全部为这个符号的 unicode 码。

  这是 UTF-8 编码的工作方式：

  ```
     Char. number range  |        UTF-8 octet sequence
        (hexadecimal)    |              (binary)
     --------------------+---------------------------------------------
     0000 0000-0000 007F | 0xxxxxxx
     0000 0080-0000 07FF | 110xxxxx 10xxxxxx
     0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
     0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
  ```

  **注意：**输入是整数数组。只有每个整数的 **最低 8 个有效位** 用来存储数据。这意味着每个整数只表示 1 字节的数据。

  

  **示例 1：**

  ```
  输入：data = [197,130,1]
  输出：true
  解释：数据表示字节序列:11000101 10000010 00000001。
  这是有效的 utf-8 编码，为一个 2 字节字符，跟着一个 1 字节字符。
  ```

  **示例 2：**

  ```
  输入：data = [235,140,4]
  输出：false
  解释：数据表示 8 位的序列: 11101011 10001100 00000100.
  前 3 位都是 1 ，第 4 位为 0 表示它是一个 3 字节字符。
  下一个字节是开头为 10 的延续字节，这是正确的。
  但第二个延续字节不以 10 开头，所以是不符合规则的。
  ```

  

  **提示:**

  - `1 <= data.length <= 2 * 104`
  - `0 <= data[i] <= 255`

## 题解

**位运算**

判断编码是否有效，需要解决两个问题：

1. 当前字节是否是单字节字符。
2. 多字节字符有多少位，是否符合格式。

对于问题1，我们准备MASK1(1<<7)来判断

对于问题2，我们依次从高位到低位判断有n个1（n的个数**小于等于**4个），随后判断后面的n个字节是否以10开头即可。

当不满足以上任一条件时，编码无效。

## 代码

```java
class Solution {
    public static final int MASK1=1<<7;// 判断1字节还是n字节
    public static final int MASK2=(1<<7)+(1<<6); // 判断编码第一字节还是其他字节


    public boolean validUtf8(int[] data) {
        int n=data.length;
        int i=0;
        while (i<n){
            if((data[i]&MASK1)==0){
                i++;
            }else{
                int nums=6;
                int maskBytes=1<<nums;
                int bytes=1;
                while(nums>0){
                    if((maskBytes&data[i])==maskBytes){
                        bytes++;
                        nums--;
                        maskBytes=1<<nums;
                    }else{
                        break;
                    }
                }
                if(nums<3||bytes<2){
                    return false;
                }
                for (int j = 1; j < bytes; j++) {
                    i++;
                    if(i>=n){
                        return false;
                    }
                    if((data[i]&MASK2)!=MASK1){
                        return false;
                    }
                }
                i++;
            }
        }
        return true;

    }
}
```

**复杂度**

空间复杂度O(n）

时间复杂度O(1)

