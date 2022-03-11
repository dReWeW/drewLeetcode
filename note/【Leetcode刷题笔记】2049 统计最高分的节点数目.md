# 【Leetcode刷题笔记】2049 统计最高分的节点数目

## 题目描述

- 给你一棵根节点为 0 的 二叉树 ，它总共有 n 个节点，节点编号为 0 到 n - 1 。同时给你一个下标从 0 开始的整数数组 parents 表示这棵树，其中 parents[i] 是节点 i 的父节点。由于节点 0 是根，所以 parents[0] == -1 。

  一个子树的 大小 为这个子树内节点的数目。每个节点都有一个与之关联的 分数 。求出某个节点分数的方法是，将这个节点和与它相连的边全部 删除 ，剩余部分是若干个 非空 子树，这个节点的 分数 为所有这些子树 大小的乘积 。

  请你返回有 最高得分 节点的 数目 。
  
  


## 题解

得到一个点的分数需要三个部分。n1: 节点左子树节点数 n2:节点右子树节点数 n3:除开节点本身和其子树的剩下的子树的节点数。

$Point=n1*n2*n3$

$n3=N-n1-n2-1$

综上可推出求出n1,n2即可求出Point

对于一个节点，dfs其子树，返回遍历到的节点数即可得到其子树的节点数。

## 代码

```java
class Solution {
   int[] ans;
    int n;
    int[] children1;
    int[] children2;
    public int countHighestScoreNodes(int[] parents) {
        n = parents.length;
        ans = new int[n];
        children1=new int[n];
        children2=new int[n];
        for (int i = 1; i < n; i++) {
            if(children1[parents[i]]==0){
                children1[parents[i]]=i;
            }else{
                children2[parents[i]]=i;
            }

        }
        dfs( 0, parents);
        int max = 0;
        int res = 0;
        for (int i = 0; i < n; i++) {
            if (ans[i] > max) {
                max = ans[i];
                res = 1;
            } else if (ans[i] == max) {
                res++;
            }
        }
    }

    private int dfs(int node, int[] parents) {
        List<Integer> subTreeNodes = new ArrayList<>();
        int subNodes = 0;
        if (children1[node] != 0) {
            int tmp = dfs( children1[node], parents);
            subNodes += tmp;
            subTreeNodes.add(tmp);
        }
        if (children2[node] != 0) {
            int tmp = dfs( children2[node], parents);
            subNodes += tmp;
            subTreeNodes.add(tmp);
        }
        if (node != 0)
            subTreeNodes.add(n - subNodes - 1);
        ans[node] = 1;
        for (Integer nodes : subTreeNodes) {
            ans[node] *= nodes;
        }
        return subNodes + 1;
    }
}
```

**复杂度**

空间复杂度O(n）

时间复杂度O(3*n)

