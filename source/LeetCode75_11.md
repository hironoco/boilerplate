---
title: Leetcode75-11
date: 2024-3-31
---
## 説明

+ 配列sが配列tに含まれるならtrue、そうでないならfalseを返す。
+ 原文
>Given two strings s and t, return true if s is a subsequence of t, or false otherwise.
>A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).

## 例題との相違点

+ 自分の回答(1ms)
  + sとtの要素を順番に比較していく、sの要素がtに含まれる場合sのインデックスを進める、最終的なインデックスがsの長さと同じならtrue、そうでないならfalse

```go
func isSubsequence(s string, t string) bool {

    sIndex := 0
    tIndex := 0

    for sIndex < len(s) && tIndex < len(t){
        if s[sIndex] == t[tIndex] {
            sIndex++
        }
        tIndex++ 
    }
    
    if sIndex < len(s) {
        return false
    } else {
        return true
    }
}
```

+ 回答例

```go
func isSubsequence(s string, t string) bool {
    i, j := 0, 0
    for i < len(s) && j < len(t) {
        if s[i] == t[j] {
            i++
        }
        j++
    }
    return i == len(s)
}
```

## 相違点

+ 最後の返し方だけ違う。自分はコードがどうなるかを完全に把握できてないから値が外れても問題ないように記述してしまう

## 感想

+ 今回はうまいことできた