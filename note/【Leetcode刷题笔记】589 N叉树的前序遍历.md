# 【Leetcode刷题笔记】589 N叉树的前序遍历

## 题目描述

- 给定一个 n 叉树的根节点 `root` ，返回 *其节点值的 **前序遍历*** 。

  n 叉树 在输入中按层序遍历进行序列化表示，每组子节点由空值 `null` 分隔（请参见示例）。

  
  
  - **示例 1：**

    ![img](https://assets.leetcode.com/uploads/2018/10/12/narytreeexample.png)
  
    ```
    输入：root = [1,null,3,2,4,null,5,6]
    输出：[1,3,5,6,2,4]
    ```
  
    **示例 2：**
  
    ![img](https://assets.leetcode.com/uploads/2019/11/08/sample_4_964.png)
  
    ```
    输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
    输出：[1,2,3,6,7,11,14,4,8,12,5,9,13,10]
    ```
  
    
  
    **提示：**
  
    - 节点总数在范围 `[0, 104]`内
    - `0 <= Node.val <= 104`
    - n 叉树的高度小于或等于 `1000`

## 题解

递归法很简单，搞清楚前序遍历的原理即可。

遍历可使用栈实现，但效率不如递归法。用栈存储每个杰点子节点的迭代器，如果Iterator.hasNext()为真，则把iterator.next()入栈，否则出栈。

## 代码

递归法

```java
class Solution {
    List<Integer> res;

    public List<Integer> preorder(Node root) {
        res = new ArrayList<>();
		preOrderTraverse(root);
        return res;
	}
private void preOrderTraverse(Node root) {
        if (root == null) {
            return;
        }
        this.res.add(root.val);
        Iterator<Node> it = root.children.iterator();
        while (it.hasNext()) {
            preOrderTraverse(it.next());
        }
    }
}
```

遍历法

```java
class Solution {
    List<Integer> res;

    public List<Integer> preorder(Node root) {
        res = new ArrayList<>();
        if(root==null){
            return res;
        }
        res.add(root.val);
        Stack<Iterator<Node>> stack=new Stack<>();
        stack.push(root.children.iterator());
        while(!stack.isEmpty()){
            Iterator<Node> it=stack.peek();
            if(!it.hasNext()){
                stack.pop();
            }else {
                Node node=it.next();
                res.add(node.val);
                stack.add(node.children.iterator());
            }
        }
        return res;
//        preOrderTraverse(root);
//        return res;
    }
}
```

**复杂度**

时间复杂度O(n)

