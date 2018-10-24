## Two Sum	两数之和

Link: <https://leetcode.com/problems/two-sum/>

**Problem:**

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```



**Approach:**

两次遍历，第一次利用哈希表存入所有数据，第二次查找 **target-nums[i]** 是否在哈希表中

时间，空间都是O(n)

**Solution:**

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> record;
        vector<int> result;
        for(int i = 0; i < nums.size(); i++)
            record[nums[i]] = i;   //存入
        for(int i = 0; i < nums.size(); i++)
            if( record.find(nums[i]) != record.end() )
            {
                int l=i<record[nums[i]]?i:record[nums[i]]; //按大小顺序
                int r=i>record[nums[i]]?i:record[nums[i]];
                result.push_back(l);
                result.push_back(r);
                return result;
            }
    }
};
```

