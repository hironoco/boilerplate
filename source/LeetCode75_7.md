---
title: Leetcode75-6
date: 2024-3-23
---

## 例題との相違点

+ 自分の回答（13ms）
  + 左右から累積積を求める方法
  + 左から累積積を求めるときは１つ前の積を要素に入れ、右からのときは１つ前の積を要素にかける。そうすれば自分の要素以外の積を求めることができる。

```go
func productExceptSelf(nums []int) []int {

    answer := make([]int, len(nums))

    initial := 1

    for i := 0; i < len(nums); i++ {
        answer[i] = initial
        initial *= nums[i]
    }

    buf := 1

    for i := len(nums)-1; i>=0; i-- {
        answer[i] *= buf
        buf *= nums[i]
    }

    return answer
}
```

+ 最速の例題
  + 最速の例題を試したところ、変わらなかった。

## 感想

+ for文を入れ子にした回答はタイムアウトエラーになってしまった。
  + 計算量がO(n^2)になるからしい
  + 左右からの累積積はO(2n)になる。
