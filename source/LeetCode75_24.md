---
title: Leetcode75-24
date: 2024-5-26
---
## 説明

+ 与えられた2つの文字列を、以下のルールに従って変換可能かどうかを返す
  + 2つの文字の位置を入れ替える
  + 2種類の文字を相互に入れ替える

+ 原文

Two strings are considered close if you can attain one from the other using the following operations:

Operation 1: Swap any two existing characters.

> For example, abcde -> aecdb

Operation 2: Transform every occurrence of one existing character into another existing character, and do the same with the other character.

> For example, aacabb -> bbcbaa (all a's turn into b's, and all b's turn into a's)

You can use the operations on either string as many times as necessary.

Given two strings, word1 and word2, return true if word1 and word2 are close, and false otherwise.

## 例題との相違点

+ 自分の回答(91ms)
  + 条件から以下の条件を満たせば、与えられた手順で置換可能であることが分かった。
  + 使用している文字が同じこと
  + 使用している文字数の組み合わせが同じこと
  + 以上を確認するためにmapを用いて文字の出現回数を記録した。
  + 出現回数の個数もmapで記録し、その処理中で片方の文字がもう片方にないことを確認
  + 出現回数の個数が同じなら交換可能のため両方のmapから要素を消す
  + 食い違いがあればfalse、最後まで処理できればtrue

```go
func closeStrings(word1 string, word2 string) bool {
    if(len(word1) != len(word2)){
        return false
    }
    charCount1 := make(map[byte]int)
    charCount2 := make(map[byte]int)

    for i := 0; i < len(word1); i++ {
        charCount1[word1[i]]++
        charCount2[word2[i]]++
    }

    countCount1 := make(map[int]int)
    countCount2 := make(map[int]int)

    for k, v := range charCount1 {
        countCount1[v]++
        if _, ok := charCount2[k]; !ok {
            return false
        }
    }
    for k, v := range charCount2 {
        countCount2[v]++
        if _, ok := charCount1[k]; !ok {
            return false
        }
    }

    for k, v := range countCount1 {
        if countCount2[k] == v {
            delete(countCount2, k)
            delete(countCount1, k)
        }else{
            return false
        }
    }
    return true

}
```

+ 回答例（15ms）
  + 基本同じことを行っているが、128というのがみそ
  + a~zはbyteに直すと97～122
  + そのため122までの配列を作って、そこにその文字が何回出てきたかを記録している。
  + 何回出てきたかの回数をソートし、小さい方から一致するかどうかを見ている。

```go
func closeStrings(word1 string, word2 string) bool {

	wordOneBytes := []byte(word1)
	wordTwoBytes := []byte(word2)

	setOne := make([]int, 128)
	setTwo := make([]int, 128)

	for i := 0; i < len(wordOneBytes); i++ {
		setOne[wordOneBytes[i]]++
	}

	for i := 0; i < len(wordTwoBytes); i++ {
		setTwo[wordTwoBytes[i]]++
	}

    for i := 0; i < 128; i++ {
        if setOne[i] > 0 && setTwo[i] == 0{
            return false
        }

        if setTwo[i] > 0 && setOne[i] == 0{
            return false
        }
    }

	sort.Ints(setOne)
	sort.Ints(setTwo)

	for i := 0; i < 128; i++ {
		if setOne[i] != setTwo[i] {
			return false
		}
	}

	return true
}
```

## 感想

+ byteベースで処理しているため早い。
+ ソートしているから遅いとも思ったが、影響は少ない
