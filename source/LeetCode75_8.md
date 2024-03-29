---
title: Leetcode75-7
date: 2024-3-23
---
## 説明

+ 配列の中に順番の増える3つの要素があるかを確認する問題
+ 原文
  + Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false.

## 例題との相違点

+ 自分の回答（106ms）

```go
func increasingTriplet(nums []int) bool {

	minValue := math.MaxInt32
  secondMinValue := math.MaxInt32

	for i := 0; i < len(nums); i++ {
		if nums[i] <= minValue {
			minValue = nums[i]
		} else if nums[i] <= secondMinValue {
			secondMinValue = nums[i]
		} else {
			return true
		}
	}
	return false
}
```

+ 最速の例題(75ms)

```go
func increasingTriplet(nums []int) bool {
	a := nums[0]
	b := math.MaxInt32

	for i := 0; i < len(nums); i++ {
		if a >= nums[i] {
			a = nums[i]
		} else if b >= nums[i] {
			b = nums[i]
		} else {
			return true
		}
	}
	return false
}
```

+ 相違点なし

## 感想

+ for文を入れ子にした回答はタイムアウトエラーになってしまった。
+ 順番に確認し、最小値を見つけたら更新する方法で十分。
+ 見つけた配列を返すのではなく、true、falseを返せばよいので厳密に比較する必要はない。
