---
title: Leetcode75-4
date: 2024-3-12
---

## 例題との相違点

+ 自分の回答

```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    
    arrangeArray := append([]int{0}, flowerbed...)
    arrangeArray = append(arrangeArray, 0)


    for i := 1; i < len(flowerbed)+1; i++{
        if arrangeArray[i-1] == 0 && arrangeArray[i] == 0 && arrangeArray[i+1] == 0{
            arrangeArray[i] =1
            n--
        }
    }

    return n<=0;
}
```

+ 最速の例題

```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    var available int

    for i := 0; i < len(flowerbed); i++ {
        if flowerbed[i] != 0 {
            continue
        }

        prevIsZero := i == 0 || flowerbed[i-1] == 0
        nextIsZero := i == len(flowerbed)-1 || flowerbed[i+1] == 0

        if prevIsZero && nextIsZero {
            flowerbed[i] = 1
            available++
        }
    }

    return available >= n
}
```

+ 違い
  + 確認箇所が0じゃなかったらそもそも置けないから飛ばしている
  + 外からの変数(n)ではなく、関数内で定義した変数(available)を操作している。
  + 配列操作をせずに、条件で最初と最後の要素を処理している。(以下のところ)
```go
prevIsZero := i == 0 || flowerbed[i-1] == 0
nextIsZero := i == len(flowerbed)-1 || flowerbed[i+1] == 0
```



+ 検証
  + arrangeArray[i] == 0 を一番最初に評価したら2~4ms早くなった
  + 関数内の変数を使うようにしたら2ms早くなった
  + 1をセットするときに、i++したら余計に遅くなった。(処理する配列は少なくなるのになぜ？)
  + 配列操作を減らしてもあまり変わらない
  + 前後を判定する前に、インデックスi の箇所が0じゃなったら飛ばすのが最も早い。
  + 以下の形が、自分の回答を最も早くした形。
```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    ava := 0

    arrangeArray := append([]int{0}, flowerbed...)
    arrangeArray = append(arrangeArray, 0)


    for i := 1; i < len(flowerbed)+1; i++{
        if arrangeArray[i] == 0 && arrangeArray[i-1] == 0 && arrangeArray[i+1] == 0{
            arrangeArray[i] =1
            ava++
        }
    }

    return n<=ava;
}
```