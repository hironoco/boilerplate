---
title: Leetcode75-16
date: 2024-4-30
---
## 説明

+ 与えられた配列から、与えられた数値分の連続した配列を抜き取るとき、最大の平均値を返す。
+ 原文

>You are given an integer array nums consisting of n elements, and an integer k.
>Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

## 例題との相違点

+ 自分の回答(116ms)
  + for文を回して、ずらした分の差分を要素数で割ることで入れ子のfor文を回避している。
  + 一番早い部類だった。

```go
func findMaxAverage(nums []int, k int) float64 {
    max := average(nums[:k])
    if(len(nums) == k) {return max}

    avg := max

    for i := 1; i <= len(nums) - k; i++ {
        diff := float64(nums[i+k-1] - nums[i-1])/float64(k)
        avg = avg + float64(diff)
        if avg > max {
            max = avg
        }
    }
    return max
    
}

func average(nums []int) float64 {
    sum := 0
    for _, value := range nums {
        sum += value
    }
    return float64(sum) / float64(len(nums))
}
```

+ 回答例（なし）


## 感想

+ ほかの回答では差分の平均を出すのではなく、最大値を保持して差分を足して要素数で割るという対応をしていた。