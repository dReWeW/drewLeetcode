# 【Leetcode刷题笔记】 537 复数乘法

## 题目描述

[复数](https://baike.baidu.com/item/复数/254365?fr=aladdin) 可以用字符串表示，遵循 `"**实部**+**虚部**i"` 的形式，并满足下述条件：

- `实部` 是一个整数，取值范围是 `[-100, 100]`
- `虚部` 也是一个整数，取值范围是 `[-100, 100]`
- `i2 == -1`

给你两个字符串表示的复数 `num1` 和 `num2` ，请你遵循复数表示形式，返回表示它们乘积的字符串。



**示例 1：**

```
输入：num1 = "1+1i", num2 = "1+1i"
输出："0+2i"
解释：(1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i ，你需要将它转换为 0+2i 的形式。
```

**示例 2：**

```
输入：num1 = "1+-1i", num2 = "1+-1i"
输出："0+-2i"
解释：(1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i ，你需要将它转换为 0+-2i 的形式。 
```



**提示：**

- `num1` 和 `num2` 都是有效的复数表示。

Related Topics

数学

字符串

模拟

## 题解

这道题没什么好说的，直接模拟即可，很简单。

显然此题需要用到分割字符串来获得实数和虚数的数值，我们很容易想到`String.split()`方法，这里复习一下split()方法的用法：

- ### String.split()

  public [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)[] split([String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html) regex)

  Splits this string around matches of the given [regular expression](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/regex/Pattern.html#sum).

  This method works as if by invoking the two-argument [`split`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html#split(java.lang.String,int)) method with the given expression and a limit argument of zero. Trailing empty strings are therefore not included in the resulting array.

  The string `"boo:and:foo"`, for example, yields the following results with these expressions:

  > | Regex | Result                    |
  > | ----- | ------------------------- |
  > | :     | `{ "boo", "and", "foo" }` |
  > | o     | `{ "b", "", ":and:f" }`   |

  

  - Parameters:

    `regex` - the delimiting regular expression

  - Returns:

    the array of strings computed by splitting this string around matches of the given regular expression

  - Throws:

    `PatternSyntaxException` - if the regular expression's syntax is invalid

  - Since:

    1.4

  - See Also:

    [`Pattern`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/regex/Pattern.html)

## 代码

```java
class Solution {
    public String complexNumberMultiply(String num1, String num2) {
        String[] complex1=num1.split("\\+|i");
        String[] complex2=num2.split("\\+|i");
        int real1=Integer.parseInt(complex1[0]);
        int imag1=Integer.parseInt(complex1[1]);
        int real2=Integer.parseInt(complex2[0]);
        int imag2=Integer.parseInt(complex2[1]);
        int real=real1*real2-imag1*imag2;
        int imag=real1*imag2+real2*imag1;
        String res=String.format("%d+%di",real,imag);
        return res;

    }
}
```

**复杂度**

时间空间皆为O(1)