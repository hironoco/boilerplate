---
title: Leetcode75-10
date: 2024-3-31
---
## 説明

+ int配列を探索して0だったら末尾に移動する。それ以外の数字の並び順は保持する。
+ 原文
>Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
>Note that you must do this in-place without making a copy of the array.

## 例題との相違点

+ 自分の回答(29ms)
  + 0だったらその要素の前後で配列を2つに分割しくっつける、そして一番最後に0を追加する。
  + しかしこの方法は配列を他にコピーしないという制約に引っかかっていそう

```go
func moveZeroes(nums []int)  {
    j := 0
    for i:=0; i < len(nums)-j; i++{
        if nums[i] == 0 {
            nums = append(append(nums[:i], nums[i+1:]...),0)
            j++
            i--
        }
    }
}
```

+ 最速の回答

```go
func moveZeroes(nums []int) {
	if nums == nil {
		return 
	}

	left, right := 0, 0
	for right < len(nums) {
		if nums[right] != 0 {
			if left != right {
				nums[left], nums[right] = nums[right], nums[left]
			}
            left++
		}
		right++
	}
}
```

## 相違点

+ 左から探索し、0の塊の左と右のインデックスを保持している。
+ 右のインデックスの値が0だったら塊に加える（つまり右のインデックスを1つ進めるだけにする。）
+ 右のインデックスの値が0以外だったら、左のインデックスの値（つまり左端の0）と入れ替える。

## 感想

+ 配列の要素を入れ替えるだけという発想がない
+ 左から順に探索していって、その1回のみで達成できる方法を検討する。
