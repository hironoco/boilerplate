---
title: Leetcode75-26
date: 2024-5-26
---
## 説明

+ 与えられた「*」を含む文字列から、「*」とその1つ前の文字を抜いたものを返す。

+ 原文

Given a 0-indexed n x n integer matrix grid, return the number of pairs (ri, cj) such that row ri and column cj are equal.

A row and column pair is considered equal if they contain the same elements in the same order (i.e., an equal array).

## 例題との相違点

+ 自分の回答(25ms)
  + 最初に、byte型配列に変換したものをごにゃごにゃとインデックスを戻したりして変形させてそれを返したものを提出したら処理時間がすごく長くなった。
  + 代わりに、からの配列を用意して、そこに条件に合ったものを抜き差しするようにしたら最も早い解答となった。

```go
func removeStars(s string) string {
	byteStr := []byte(s)
	result := make([]byte, 0)
	for _, k := range byteStr {
		if k == '*' {
			result = result[:len(result)-1]
		} else {
			result = append(result, k)
		}
	}

	return string(result)
}
```

+ 回答例（なし）

## 感想

+ メモリ容量と処理時間は反比例する？
