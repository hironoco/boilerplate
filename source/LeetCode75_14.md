---
title: 1680
date: 2024-4-15
---
## 説明

+ LeetCode 75 のものではなかった。

+ １から渡された数値を２進数に変換し、それを順番に結合しまた10進数に直す。
+ それを10の9条+7で割った余りを返す
+ 原文

>Given an integer n, return the decimal value of the binary string formed by concatenating the binary representations of 1 to n in order, modulo 109 + 7.

## 例題との相違点

+ 自分の回答(119ms)
  + 渡された数値分for文を回す
  + for文の中では数値を2進数に変換し結合
  + 10進数に変換して10~9+7で割った余りを算出し、それをもとの文字列とする。
  + for文の中で余りを求めているのはオーバーフローを防ぐため、これに気づかず解決にとても時間がかかった

```go
import "strconv"

func concatenatedBinary(n int) int {
    bitStr := ""
    result := 0
    for i := 1; i<= n; i++ {
        bitStr += fmt.Sprintf("%b", i)

        temp,_ := strconv.ParseInt(bitStr, 2, 0)

        result = int(temp % 1000000007)

        bitStr = fmt.Sprintf("%b", result)

    }

    return result
}
```

+ 回答例(26ms)

```go
func concatenatedBinary(n int) int {
	var res int
    var mod int = 1e9 + 7
	i := 1
	offset := 0
	for i <= n {
        if i & (i - 1) == 0 {
            offset += 1
        }

		res = (res<<offset | i) % mod
		i++
	}
	return res
}
```

## 相違点

+ 文字列に直さず、ビットシフトで処理している

## 感想

+ 余剰演算の等価性に気づけず、オーバーフローしてしまっていた。
+ ビットで数値を扱うのが不慣れすぎて理解に時間がかかった。
