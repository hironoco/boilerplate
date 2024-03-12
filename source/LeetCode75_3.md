---
title: Leetcode75-3
date: 2024-2-25
---

## 例題との相違点

+ 自分の回答

```go
func kidsWithCandies(candies []int, extraCandies int) []bool {
    resultArr := []bool{}
    maxValue := getMaxVlaue(candies)
    for _, v := range candies {
        resultValue := v + extraCandies >= maxValue
        resultArr = append(resultArr, resultValue)
    }
    return resultArr;
}

func getMaxVlaue(list []int) int {
    max := 0
    for _, v := range list{
        if max < v {
            max = v
        }
    }
    return max
}
```

+ 最速の例題

```go
func kidsWithCandies(candies []int, extraCandies int) []bool {
    max := 0

    for i:=0; i<len(candies); i++ {
        if max<candies[i]{
            max = candies[i]
        }
    }
    result := make([]bool, len(candies))

    for i:=0; i<len(candies); i++ {
        if candies[i] + extraCandies >= max{
            result[i] = true
        }
    }
    return result
}
```

+ 違い
  + for文を使っている
    + for range より for文のほうが速い？
  + 可変長（スライス）じゃなく、固定長（配列）を使っている。


+ 検証
  + 以下のように修正したら最速と同じ実行時間になった。
```go
func kidsWithCandies(candies []int, extraCandies int) []bool {
    resultArr := make([]bool, len(candies))
    maxValue := getMaxVlaue(candies)
    for i, v := range candies {
        resultValue := v + extraCandies >= maxValue
        resultArr[i] = resultValue
    }
    return resultArr;
}

func getMaxVlaue(list []int) int {
    max := 0
    for _, v := range list{
        if max < v {
            max = v
        }
    }
    return max
}
```