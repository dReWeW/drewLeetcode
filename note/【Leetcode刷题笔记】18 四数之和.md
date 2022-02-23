# 【Leetcode刷题笔记】18 四数之和

## 题目描述

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且**不重复**的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c` 和 `d` **互不相同**
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按 **任意顺序** 返回答案 。



**示例 1：**

```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**示例 2：**

```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```



**提示：**

- `1 <= nums.length <= 200`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`

Related Topics

+ 数组

- 双指针

- 排序

## 题解

参照 `1 两数之和` 以及 `15 三数之和`的方法，我们可以将其分解为$n^2$​个两数之和问题。对于任意nums[i]+nums[j]，我们需要在剩下的数组中寻找两数和为target-nums[i]-nums[j]。

需要注意，去重通过，每当完成一层遍历时，跳过该层遍历已经使用过的使用过的数即可。

## 代码

``` java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> lists = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int tar = target - nums[i] - nums[j];
                int k = j + 1, l = n - 1;
                while (k < l) {
                    if (nums[k] + nums[l] > tar) {
                        l--;
                    } else if (nums[k] + nums[l] < tar) {
                        k++;
                    } else if (nums[k] + nums[l] == tar) {
                        lists.add(Arrays.asList(nums[i],nums[j],nums[k],nums[l]));
                        while (k + 1 < n && nums[k] == nums[k + 1] && k < l) {
                            k++;
                        }
                        while (l - 1 > j && nums[l] == nums[l - 1] && k < l) {
                            l--;
                        }
                        k++;
                        l--;
                    }
                }
                while(j+1<n&&nums[j]==nums[j+1]){
                    j++;
                }
            }
            while (i+1<n&&nums[i]==nums[i+1]){
                i++;
            }
        }
        return lists;
    }
}
```

**复杂度分析**

时间复杂度 O(n3+nlogn)

空间复杂度O(C)，其中C = 解的个数
