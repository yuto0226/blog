---
title: "[LeetCode] 1. Two-Sum(C++)"
slug: lc_1
date: 2022-03-04 19:32:42
image:
categories:
  - 解題紀錄
tags:
  - 筆記
  - LeetCode
  - C++
---
# 題目
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

 

**Example 1**:
```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```text
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**
```text
Input: nums = [3,3], target = 6
Output: [0,1]
```

**Constraints:**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**

# 解題方向
用兩個 `for` 迴圈一個一個去檢查

# 參考程式碼
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for(int i=0;i<nums.size();i++){
            for(int j=i+1;j<nums.size();j++){
                if(nums[i]+nums[j]==target){
                    return vector<int> {i,j};
                }
            }
        }
        return {};
    }
};
```