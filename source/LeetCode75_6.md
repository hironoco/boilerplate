---
title: Leetcode75-6
date: 2024-3-22
---

## 例題との相違点

+ 自分の回答（8ms）

```go
import "strings"

func reverseWords(s string) string {
    arr := strings.Fields(s)
    result := ""

    for i := len(arr)-1; i>= 0; i-- {

        if i==0 {
            result += arr[i]
        } else {
            result += arr[i]
            result += " "
        }
    }
    return result
}
```

+ 最速の例題

```go
func reverseWords(s string) string {
    words := strings.Split(s, " ")
	result := ""
	for i := len(words) - 1; i >= 0; i-- {
		if words[i] != "" {
			result += strings.TrimSpace(words[i]) + " "
		}
	}
	return strings.TrimSpace(result)
}
```

+ 違い
  + Fieldsではなく、Splitを使ってる
  + i が０かどうかで判定せず、TrimSpaceで先頭と末尾のスペースをとっている。

+ 検証
  + i＝＝０での判定をやめて、最後に末尾を除いたら最速になった。
  + Fieldsとsplitは試していないが、そこまで違いはなさそう。

+ 以下が直したコード(0ms)
  
```go
func reverseWords(s string) string {
    arr := strings.Fields(s)
    result := ""

    for i := len(arr)-1; i>= 0; i-- {

        result += arr[i] + " "
    }
    return result[:len(result) -1 ]
}
```

## 感想

+ Splitで分けると、スペースが連続で続いている場合、""となる箇所がある。
