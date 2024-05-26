---
title: Leetcode75-22
date: 2024-5-26
---
## 説明

+ 与えられた2つ配列から、片方だけにある要素を２次元配列に入れて返す

+ 原文

> Given two 0-indexed integer arrays nums1 and nums2, return a list answer of size 2 where:
> answer[0] is a list of all distinct integers in nums1 which are not present in nums2.
> answer[1] is a list of all distinct integers in nums2 which are not present in nums1.
> Note that the integers in the lists may be returned in any order.

## 例題との相違点

+ 自分の回答(23ms)
  + ダブる要素などがあるため、配列をmapに直してkeyが存在するかどうかで判定した。

```go
func findDifference(nums1 []int, nums2 []int) [][]int {
	isExistNum1 := make(map[int]bool)
	isExistNum2 := make(map[int]bool)

    resultNums1 := []int{}
    resultNums2 := []int{}

	for _, num := range nums1 {
		isExistNum1[num] = true
	}
	for _, num := range nums2 {
		isExistNum2[num] = true
	}

    for num, _ := range isExistNum1 {
        if isExistNum2[num] {
            delete(isExistNum1, num)
            delete(isExistNum2, num)
        }else{
            resultNums1 = append(resultNums1, num)
        }
    }

    for num, _ := range isExistNum2 {
        resultNums2 = append(resultNums2, num)
    }

    return [][]int{resultNums1, resultNums2}
}
```

+ 回答例（なし）

## 感想

+ 最速の回答例は、値が-1000～1000という制限を利用した限定的なものだった
+ 汎用的な回答で最もハイヤ委回答は同じ実装だった。
