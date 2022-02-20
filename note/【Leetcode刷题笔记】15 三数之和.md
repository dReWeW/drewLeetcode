# 【Leetcode刷题笔记】三数之和

## 问题

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

**注意：答案中不可以包含重复的三元组。**

```
示例 1：
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]

示例 2：
输入：nums = []
输出：[]

示例 3：
输入：nums = [0]
输出：[]
```

**提示**：

0 <= nums.length <= 3000
-105 <= nums[i] <= 105

## 题解

`Leetcode`第一题两数之和为我提供了思路，实际上稍微思考就可以将问题转换为N个两数之和的问题。

由于本人做两数之和的时间已经比较久远，忘记了其多种做法，这里列出两种思路

1. 先排序，然后三层循环遍历求解。时间复杂度O(n3)，空间复杂度O(1)。
2. **双指针**

> 先排序
>
> 建立N个两数之和问题，即对数组中每个数做两数之和求解，只不过求和目标值不是0，而是'-nums[i]'。
>
> ①如果nums[i]>0，直接不用做两数之和的问题。因为数组已排序，说明后面的数都是>0，因而可以直接返回结果
>
> ②如果nums[i]<=0，设置两个指针j=i+1,k=n-1.
>
> ​	设置while条件(j<k)
>
> ​	 if(*nums*[j]+*nums*[k]>tmp): k向前移动
>
>  	if(*nums*[j]+*nums*[k]<tmp): j向后移动
>
> ​	 if(*nums*[j]+*nums*[k]==tmp): 加入结果数组
>
> ​	去重操作
>
> 事件复杂度O(n2),O(1)

## 代码

Java代码，双指针

``` java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        List<List<Integer>> res = new ArrayList<>();
        // return empty set
        if(n<3){
            return res;
        }
        Arrays.sort(nums);
        for(int i=0;i<n-2;i++){
            if(nums[i]>0){
                break;
            }
            int tmp=-nums[i];
            int j=i+1,k=n-1;
            while(j<k){
                if(nums[j]+nums[k]>tmp){
                    k--;
                }else if(nums[j]+nums[k]<tmp){
                    j++;
                }else if(nums[j]+nums[k]==tmp){
                    res.add(new ArrayList<Integer>(Arrays.asList(nums[i],nums[j],nums[k])));
                    while(j<n-1&&nums[j]==nums[j+1]){
                        j++;
                    }
                    while(k>0&&nums[k]==nums[k-1]){
                        k--;
                    }
                    j++;
                    k--;
                    if(!(j<k)){
                        break;
                    }
                }
            }
            while(i<n-2&&nums[i]==nums[i+1]){
                i++;
            }
        }
        return res;
    }
}	
```

## 成绩

![image-20220116012028562](C:\Users\Drew\AppData\Roaming\Typora\typora-user-images\image-20220116012028562.png)