# 【Leetcode刷题笔记】23 合并K个升序链表

## 题目描述

- 给你一个链表数组，每个链表都已经按升序排列。

  请你将所有链表合并到一个升序链表中，返回合并后的链表。

  

  **示例 1：**

  ```
  输入：lists = [[1,4,5],[1,3,4],[2,6]]
  输出：[1,1,2,3,4,4,5,6]
  解释：链表数组如下：
  [
    1->4->5,
    1->3->4,
    2->6
  ]
  将它们合并到一个有序链表中得到。
  1->1->2->3->4->4->5->6
  ```

  **示例 2：**

  ```
  输入：lists = []
  输出：[]
  ```

  **示例 3：**

  ```
  输入：lists = [[]]
  输出：[]
  ```

  

  **提示：**

  - `k == lists.length`
  - `0 <= k <= 10^4`
  - `0 <= lists[i].length <= 500`
  - `-10^4 <= lists[i][j] <= 10^4`
  - `lists[i]` 按 **升序** 排列
  - `lists[i].length` 的总和不超过 `10^4`

## 题解

顺序合并两个链表

## 代码

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode ans=null;
        int n = lists.length;
        if(n==0){
            return ans;
        }
        if(n==1){
            return lists[0];
        }
        ans=merge(lists[0],lists[1]);
        for (int i = 2; i < n; i++) {
            ans=merge(ans,lists[i]);
        }
        return ans;
    }

    private ListNode merge(ListNode a, ListNode b) {
        if (a == null || b == null) {
            return a != null ? a : b;
        }
        ListNode head = new ListNode(0);
        ListNode tail = head, aPtr = a, bPtr = b;
        while (aPtr != null && bPtr != null) {
            if (aPtr.val < bPtr.val) {
                tail.next = aPtr;
                aPtr = aPtr.next;
            } else {
                tail.next = bPtr;
                bPtr = bPtr.next;
            }
            tail = tail.next;
        }
        tail.next = (aPtr != null ? aPtr : bPtr);
        return head.next;
    }
}
```

**复杂度**

时间复杂度O($k^2n$)

空间复杂度O(1)

