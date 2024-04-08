---
title: Leetcode75-13
date: 2024-4-8
---
## 説明

+ 配列と整数が渡され、配列の中で足したら整数値になる組み合わせを抜いていき、合計何個のペアが抜かれたかを返す処理
+ 原文

>You are given an integer array nums and an integer k.
>In one operation, you can pick two numbers from the array whose sum equals k and remove them from the array.
>Return the maximum number of operations you can perform on the array.

## 例題との相違点

+ 自分の回答(78ms)
  + 数値をkeyとしたDictionaryを定義、配列中の数字を数えて格納する。
  + そのDictionaryをfor文で回し、与えられた整数値と探索中の数値の差分をkeyとする整数値の個数を探索
  + 少ない方の数分だけペアとして抜き出すことができるから、その分カウントする。
  + この方法だと重複してカウントすることになるため、最後に半分にして返す。

```go
func maxOperations(nums []int, k int) int {
    numCount := make(map[int]int)
    for _, num := range nums {
        numCount[num]++
    }
    
    pairCount := 0
    for num, count := range numCount {
        complement := k - num
        if complement != num {
            pairCount += min(count, numCount[complement])
        } else {
            pairCount += count
        }
    }
    
    return pairCount /2
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

+ 回答例(65ms)

```go
func maxOperations(nums []int, k int) int {
    res := 0
    if len(nums) <= 1 {
        return res
    }

    hmap := make(map[int]int,0)

    for _, n := range nums {
        if n > k {
            continue
        }
        remainder := k - n
        remainderCount, exists := hmap[remainder]
        if exists {
            if remainderCount - 1 == 0 {
                delete(hmap,remainder)
            } else {
                hmap[remainder]--
            }
            res++
        } else {
            hmap[n]++
        }
    }
    return res
}
```

## 相違点

+ 回答例を実行したが自分の回答よりも遅かった
+ Dictionaryに数字をキーにして数値の個数を入れていくのは同じ

## 感想

+ 最初は愚直にfor文中でfor文回すことで実装したらタイムアウトエラーになってしまった
+ 問題の例で、愚直に一回ずつ配列から要素を削除していた。
+ その通りにしなければならないと勘違いして配列操作をしていたため処理が重くなった。
