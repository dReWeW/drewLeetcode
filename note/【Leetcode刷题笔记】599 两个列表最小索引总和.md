# 【Leetcode刷题笔记】599 两个列表最小索引总和

## 题目描述

- 假设 Andy 和 Doris 想在晚餐时选择一家餐厅，并且他们都有一个表示最喜爱餐厅的列表，每个餐厅的名字用字符串表示。

  你需要帮助他们用**最少的索引和**找出他们**共同喜爱的餐厅**。 如果答案不止一个，则输出所有答案并且不考虑顺序。 你可以假设答案总是存在。

  

  **示例 1:**

  ```
  输入: list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]，list2 = ["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
  输出: ["Shogun"]
  解释: 他们唯一共同喜爱的餐厅是“Shogun”。
  ```

  **示例 2:**

  ```
  输入:list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]，list2 = ["KFC", "Shogun", "Burger King"]
  输出: ["Shogun"]
  解释: 他们共同喜爱且具有最小索引和的餐厅是“Shogun”，它有最小的索引和1(0+1)。
  ```

  

  **提示:**

  - `1 <= list1.length, list2.length <= 1000`
  - `1 <= list1[i].length, list2[i].length <= 30`
  - `list1[i]` 和 `list2[i]` 由空格 `' '` 和英文字母组成。
  - `list1` 的所有字符串都是 **唯一** 的。
  - `list2` 中的所有字符串都是 **唯一** 的。

## 题解

**哈希表**

遍历任意一个字符串数组，建立hash表。随后遍历另一个字符串数组，如果hashMap中Key存在分为两种情况：

1. 索引和与当前最小索引和相等，则入栈
2. 索引和比当前最小索引和小，则清空栈再入栈

这里我用长度较小的字符串数组建立HashMap，节省了一些空间开销。

## 代码

```java
class Solution {
    class Pair{
        public String name;
        public int sum;

        public Pair(String name, int sum) {
            this.name = name;
            this.sum = sum;
        }
    }
    public String[] findRestaurant(String[] list1, String[] list2) {
        int n1 = list1.length;
        int n2 = list2.length;
        String[] mapString = n1 < n2 ? list2 : list1;
        String[] cmpString = n1 < n2 ? list1 : list2;
        Map<String, Integer> nameMap = new HashMap<>();
        List<String> res=new ArrayList<>();
        Stack<Pair> stack=new Stack<>();
        for (int j = 0; j < mapString.length; j++) {
            nameMap.putIfAbsent(mapString[j], j);
        }
        for (int i = 0; i < cmpString.length; i++) {
            int index=nameMap.getOrDefault(cmpString[i],-1);
            if (index != -1) {
                if(!stack.isEmpty()){
                    if(stack.peek().sum>index+i){
                        stack.clear();
                        stack.push(new Pair(cmpString[i],index+i));
                    }else if(stack.peek().sum==index+i){
                        stack.push(new Pair(cmpString[i],index+i));
                    }
                }else{
                    stack.push(new Pair(cmpString[i],index+i));
                }
            }
        }
        Iterator<Pair> iter=stack.iterator();
        while(iter.hasNext()){
            res.add(iter.next().name);
        }
        return res.toArray(new String[0]);
    }
}
```

**复杂度**

空间复杂度O(min(n1,n2))

时间复杂度O(n1+n2)

