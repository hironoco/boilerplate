---
title: Leetcode75-17
date: 2024-5-17
---
## 説明

+ 与えられた配列から、与えられた数値分の連続した配列を抜き取るとき、その配列に含まれる母音の数の最大値を返す。
+ 原文

>Given a string s and an integer k, return the maximum number of vowel letters in any substring of s with length k.

## 例題との相違点

+ 自分の回答(6ms)
  + for文を回して、ずらした分の文字が大文字かどうかを判別し、最大値を探索している。
  + 最も早い回答の一つだった。

```go
func maxVowels(s string, k int) int {
    vowelLengt := checkVowelsLength(s[:k])
    tmp := vowelLengt
    for i:=1; i< len(s)-k + 1; i++ {
        delStr := s[i-1]
        addStr := s[i+k-1]

        isDel := checkIsVowel(delStr)
        isAdd := checkIsVowel(addStr)

        if isDel {
            tmp--
        }
        if isAdd {
            tmp++
        }

        if(tmp > vowelLengt){
            vowelLengt = tmp
        }
    }
    return vowelLengt
}

func checkVowelsLength(s string)int{
    tmp := 0
    for _, k := range(s){
        switch k {
        case 'a','e','i','o','u':
            tmp ++
        }
    }
    return tmp
}

func checkIsVowel(k byte) bool{
    switch k{
        case 'a','e','i','o','u':
            return true
    }
    return false
}
```

+ 回答例（なし）


## 感想

+ ほかの回答も大体同じ。
