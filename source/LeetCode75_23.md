---
title: Leetcode75-23
date: 2024-5-26
---
## 説明

+ 与えられた配列で、各数値の出現回数がすべて異なる場合trueを返す

+ 原文

> Given an array of integers arr, return true if the number of occurrences of each value in the array is unique or false otherwise.

## 例題との相違点

+ 自分の回答(0ms)
  + 数値をkeyとした出現回数を数えるmapを定義した。
  + 次に出現回数をkeyとして、すでにその回数があるかどうかをboolで返すmapを定義した。
  + 定義している最中にkeyがかぶったらfalse、最後までできたらtrue

```go
func uniqueOccurrences(arr []int) bool {
	countNum := make(map[int]int)
	for _, num := range arr {
		countNum[num]++
	}
	countCount := make(map[int]bool)
	for _, count := range countNum {
		if countCount[count] {
			return false
		}
		countCount[count] = true
	}
	return true
}
```

+ 回答例（なし）

## 感想

+ 特になし
