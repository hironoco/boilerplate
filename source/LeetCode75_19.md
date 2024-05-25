---
title: Leetcode75-19
date: 2024-5-25
---
## 説明

+ 与えられた０と1の配列から、連続した1の最大数を返す。
+ ただし配列から1つ要素を必ず抜き取らなければならない
+ 0が１つだけのと頃を抜けば連続する1が増えるため最大値も大きくなる。
+ 逆にすべて1の配列は要素数-1が答えとなる

+ 原文

> Given a binary array nums, you should delete one element from it.
> Return the size of the longest non-empty subarray containing only 1's in the resulting array. Return 0 if there is no such subarray.

## 例題との相違点

+ 自分の回答(51ms)
  + ほぼ前回の最速の回答例を流用した。
  + 処理がほぼ同じだったためである。

```go
func longestSubarray(nums []int) int {
	deleteNum := 1

	l, r := 0, 0
	ans := 0

	for r < len(nums) {
		if nums[r] == 1 {
			r++
		} else {
			if deleteNum > 0 {
				r++
				deleteNum--
			} else {
				if nums[l] == 0 {
					deleteNum++
				}
				l++
			}
		}
		ans = max(ans, r-l-1)
	}

	return ans
}
```

+ 回答例（なし）

## 感想

+ 前回のものをそのまま流用できたので、楽に解くことができた。
