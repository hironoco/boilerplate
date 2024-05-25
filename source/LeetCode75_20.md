---
title: Leetcode75-20
date: 2024-5-25
---
## 説明

+ 与えられた整数値の配列は高さの差の値の配列であり、1つ前からの差分である。
+ 最も大きい高さを返す。

+ 原文

> There is a biker going on a road trip. The road trip consists of n + 1 points at different altitudes. The biker starts his trip on point 0 with altitude equal 0.
> You are given an integer array gain of length n where gain[i] is the net gain in altitude between points i​​​​​​ and i + 1 for all (0 <= i < n). Return the highest altitude of a point.

## 例題との相違点

+ 自分の回答(0ms)
  + 説明は不要
```go
func largestAltitude(gain []int) int {
    att := 0
    maxAtt := 0
    for _,k := range gain {
        att += k
        maxAtt = max(maxAtt, att)
    }

    return maxAtt
}
```

+ 回答例（なし）

## 感想

+ 簡単すぎた
