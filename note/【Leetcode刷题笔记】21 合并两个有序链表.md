# 【Leetcode刷题笔记】21 合并两个有序链表

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

**示例 2：**

```
输入：l1 = [], l2 = []
输出：[]
```

**示例 3：**

```
输入：l1 = [], l2 = [0]
输出：[0]
```



**提示：**

- 两个链表的节点数目范围是 `[0, 50]`
- `-100 <= Node.val <= 100`
- `l1` 和 `l2` 均按 **非递减顺序** 排列

## 题解

注意到题中给出节点数目可以为0，因而需要单独处理数目为0的情况。

由于链表已经有序，因而只需要采用双指针，依次遍历两个链表，将一个链表 s1 合并到另一个链表s2 中即可。

+ 当s1.val<=s2.val<=s1.next.val || s1.next==null 时，s2加入到s1后面。更新s1和s2的值

+ 否则s1=s1.next

## 代码

``` java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode head1, head2, res;
        if(list1==null){
            return list2;
        }else if(list2==null){
            return list1;
        }
        if (list1.val <= list2.val) {
            head1 = list1;
            head2 = list2;
            res = list1;
        } else {
            head1 = list2;
            head2 = list1;
            res = list2;
        }
        while (head2 != null) {
            if ((head2.val >= head1.val && head1.next != null && head2.val <= head1.next.val)||head1.next==null) {
                ListNode tmp = new ListNode(head2.val, head1.next);
                head1.next = tmp;
                head1 = head1.next;
                head2 = head2.next;
            } else if(head1.next!=null){
                head1 = head1.next;
            }
        }
        return res;
    }
}
```

