---
title: Leetcode75-11
date: 2024-3-31
---
## 説明

+ 高さを格納した配列を探索して、入れることができる最大の水量を返す。
+ 原文

>You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).
>Find two lines that together with the x-axis form a container, such that the container contains the most water.
>Return the maximum amount of water a container can store.
>Notice that you may not slant the container.

## 例題との相違点

+ 自分の回答(208ms)
  + 配列の最大値を取得
  + その最大値でためることができる最も多い水の量を計算する。
  + 最大値を小さくしていって、最大量を更新していく
  + 最大量が高さと配列の長さの積（つまりその高さで取得できる理想の最大値）を超えると探索終了

```go
func maxArea(height []int) int {
	max := getMaxheight(height)
	tmpArea := 0

	for h := max; h > 0; h-- {
        if tmpArea > h*(len(height)-1) {
			break
		}
		area := getMaxAreaWithHeight(height, h)
		if area > tmpArea {
			tmpArea = area
		}
	}

	return tmpArea
}

func getMaxheight(height []int) int {
	max := 0
	for i := 0; i < len(height); i++ {
		if height[i] > max {
			max = height[i]
		}
	}
	return max
}

func getMaxAreaWithHeight(height []int, h int) int {
	min := -1
	max := 0
	for i := 0; i < len(height); i++ {
		if height[i] >= h {
			if min < 0 {
				min = i
			} else {
				max = i
			}
		}
	}
	calcHeight := height[min]
	if height[min] > height[max] {
		calcHeight = height[max]
	}

	max = calcHeight * (max - min)

	return max
}
```

+ 回答例(42ms)

```go
func maxArea(height []int) int {
    max := 0
    i := 0
    j := len(height) - 1
    for i < j {
        h1 := height[i]
        h2 := height[j]
        if h1 <= h2 {
            area := h1 * (j - i)
            if area > max {
                max = area
            }
            i += 1
        } else {
            area := h2 * (j - i)
            if area > max {
                max = area
            }
            j -= 1
        }
    }
    return max
}
```

## 相違点

+ 自分は高さを固定して最大値を求める方法、回答例は左右のインデックスを固定して最大値を求める方法
+ 高さだと変数は1つ、左右だと変数は2つ
+ 自分は左右から探索したときに、見逃しがないように効率よく探す方法を思いつけなかった。
+ 左右の高さを比較して、低い方をインデックスをずらす、という方法ではモレがあるのではないかと思ってしまう。

## 感想

+ やはり、アルゴリズムで見落とし、漏れがあるのではないかと思ってそれが必ず出ないやり方を採用してしまう。
+ どうしたらよいか
