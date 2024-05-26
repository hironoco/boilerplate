---
title: Leetcode75-25
date: 2024-5-26
---
## 説明

+ 与えられた2次元文字列で行と列が等しい数を数える

+ 原文

Given a 0-indexed n x n integer matrix grid, return the number of pairs (ri, cj) such that row ri and column cj are equal.

A row and column pair is considered equal if they contain the same elements in the same order (i.e., an equal array).

## 例題との相違点

+ 自分の回答(49ms)
  + 愚直にfor文を回したが、早い方だった。

```go
func equalPairs(grid [][]int) int {

    transGrid := transpose(grid)
    count := 0

    for _, row := range grid {
        for _, transRow := range transGrid {
            if arraysAreEqual(row, transRow) {
                count++
            }
        }
    }

    return count
}

func transpose(grid [][]int) [][]int {
    result := make([][]int, len(grid[0]))
    for i := range result {
        result[i] = make([]int, len(grid))
    }

    for i, row := range grid {
        for j, val := range row {
            result[j][i] = val
        }
    }

    return result
}

func arraysAreEqual(a, b []int) bool {
    if len(a) != len(b) {
        return false
    }
    for i, v := range a {
        if v != b[i] {
            return false
        }
    }
    return true
}
```

+ 回答例（なし）

## 感想

+ また制限を利用して早くしている。
+ 制限を利用するのは、バグにつながるためやむを得ないときは使用したくない
