---
title: "[LeetCode] 69. Sqrt(x)(C++)"
slug: lc_69
date: 2022-03-04 19:50:42
image:
categories:
  - 解題紀錄
tags:
  - 筆記
  - LeetCode
  - C++
---
# 題目
Given a non-negative integer `x`, compute and return the square root of `x`.

Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

**Note:** You are not allowed to use any built-in exponent function or operator, such as `pow(x, 0.5)` or `x ** 0.5`.

**Example 1:**
```text
Input: x = 4
Output: 2
```

**Example 2:**
```text
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.
```

**Constraints:**
- 0 <= x <= 231 - 1

# 解題方向
連分數法求根號值，可以參考[李永樂老師的影片](https://youtu.be/NXexkJyPoQs?t=27)
可以得知 S=a^2+b 中的 a 會等於題目所求的答案

# 參考程式碼
```cpp
class Solution {
public:
    int mySqrt(int x) {
        long count=0;
        int temp;
        while(true){
            if(count*count>x){
                return temp;
            }
            temp=count;
            count++;
        }
        return {};
    }
};
```