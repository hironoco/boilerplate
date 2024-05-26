---
title: Leetcode75-27
date: 2024-5-26
---
## 説明

+ 整数値の配列を与えられる。その値は星の質量で、プラスマイナスは移動方向を示している。
+ プラスは右、マイナスは左に動く。
+ 星は衝突すると質量の大きいほうだけ残る。
+ 同じ質量のときは両方消失する。
+ 最終的に残る星の配列を返す。

+ 原文

We are given an array asteroids of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

## 例題との相違点

+ 自分の回答(35ms)
  + 左から順に2つの要素を比較し、衝突するなら重さで判定をしている。

```go
func asteroidCollision(asteroids []int) []int {
	for i := 0; i < len(asteroids); i++ {
		if len(asteroids) > i+1 {
			if asteroids[i] > 0 && asteroids[i+1] < 0 {
				if asteroids[i] > -1*asteroids[i+1] {
					asteroids = append(asteroids[:i+1], asteroids[i+2:]...)
				} else if asteroids[i] < -1*asteroids[i+1] {
					asteroids = append(asteroids[:i], asteroids[i+1:]...)
				} else {
                    asteroids = append(asteroids[:i], asteroids[i+2:]...)
				}
				i = -1
			}
		} else {
			return asteroids
		}
	}
	return asteroids
}
```

+ 回答例（9ms）
  + 別に配列を作ってそこに値を入れていっている。
  + 右方向に動くものはいったん配列に入れているが、その後の判定で消すこともする。

```go
func asteroidCollision(ast []int) []int {
    stack := make([]int,0)
    for i :=0;i<len(ast);i++ {
        if ast[i] > 0  {
            stack = append(stack,ast[i])
        }else{
            for len(stack) > 0 && stack[len(stack)-1] > 0 && (stack[len(stack)-1] < -ast[i]) {
                stack = stack[:len(stack)-1]
            }
            if len(stack) > 0 && stack[len(stack)-1] == -ast[i] {
                stack = stack[:len(stack)-1]
            }else if len(stack) == 0 || stack[len(stack)-1] < 0 {
                stack = append(stack,ast[i])
            }
        }
    }

    return stack
}
```

## 感想

+ appendを使うときに要素数の大きいものを変更すると時間がかかるのかもしれない
