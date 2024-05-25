---
title: Leetcode75-18
date: 2024-5-25
---
## 説明

+ 与えられた０と1の配列から、連続した1の最大数を返す。
+ ただし与えられた数分の0を１に置換してよい
+ 原文

> Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

## 例題との相違点

+ 自分の回答(167ms)
  + for文を回して、連続する1を数えた。
  + 0を1に置換できる数分の配列を用意し、置換した0まで、0を含めて何個の1が並んでいるかを格納した。
  + 要素が0のときに、その配列を左にシフトし、インデックス0の値を最大値から引いた。
  + 以上を繰り返すことで探索を行った。

```go
func longestOnes(nums []int, k int) int {

	// 連続した1の要素数を保持する、k分の配列が必要
	seqOne := make([]int, k)
	tmeseq := 0

	// 0を含めて連続した1の最大値を保持する
	maxLength := 0

	allMaxLength := 0

	// 0がkの値以上反転されたら、最初の連続1をリセットし、その要素分を反転0と1の連続数から引く
	for _, num := range nums {

		if num == 1 {
			maxLength++
			tmeseq++
		} else {
			if len(seqOne) == 0 {
				maxLength = 0
			} else {

				if seqOne[0] > 0 {
					maxLength -= seqOne[0]
				}

				shiftLeft(seqOne)

				seqOne[k-1] += tmeseq + 1
				maxLength++
				tmeseq = 0
			}

		}
		if maxLength > allMaxLength {
			allMaxLength = maxLength
		}

	}
	return allMaxLength
}

func shiftLeft(seqOne []int) {
	copy(seqOne[0:], seqOne[1:])
	seqOne[len(seqOne)-1] = 0
}
```

+ 回答例（48ms）
  + rとlを使って、尺取虫のように探索している。
  + 先頭を進めていって、伸ばせるところまで伸ばしたら、終端を進める。
  + 0の使用量が復活したらまた先頭を進める。

```go
func longestOnes(nums []int, k int) int {
    l, r := 0, 0
    ans := 0
    
    for r < len(nums) {
        if nums[r] == 1 {
            r++
        } else {
            if k >0 {
                r++
                k--
            }else{
                if nums[l] == 0 {
                    k++
                }
                l++
            }
        }
        ans = max(ans, r-l)
    }

    return ans
}
```

## 感想

+ まだシンプルに考える力が足りない。
