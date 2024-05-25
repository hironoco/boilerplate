---
title: Leetcode75-21
date: 2024-5-25
---
## 説明

+ 与えられた配列のピボットインデックスを返す
+ ピボットインデックスとはそのインデックスから見た左右の要素の輪が等しくなるインデックスのこと
+ ないときは-1を返す

+ 原文

> Given an array of integers nums, calculate the pivot index of this array.
> The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.
> If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.
> Return the leftmost pivot index. If no such index exists, return -1.

## 例題との相違点

+ 自分の回答(10ms)
  + 説明は不要

```go
func pivotIndex(nums []int) int {
    sum := calcSumArray(nums)
    leftSum := 0
    for i, v := range nums {
        if sum - v == 2 * leftSum {
            return i
        }
        leftSum += v
    }
    return -1
}

func calcSumArray(nums []int) int {
    sum := 0
    for _, v := range nums {
        sum += v
    }
    return sum
}
```

+ 回答例（なし）

## 感想

+ 最初に合計を求めるのは処理時間がかかると思ったが、影響はなかった。
+ 回答例と処理時間は変わらなかった。
