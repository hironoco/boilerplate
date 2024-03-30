---
title: Leetcode75-9
date: 2024-3-30
---
## 説明

+ byte配列の中の連続した文字列をカウントして、元の配列に反映する処理
+ 例えば[a,a,a]なら[a,3]のようにする。
+ 原文
> Given an array of characters chars, compress it using the following algorithm:
>
> Begin with an empty string s. For each group of consecutive repeating characters in chars:
>
> If the group's length is 1, append the character to s.
> Otherwise, append the character followed by the group's length.
> The compressed string s should not be returned separately, but instead, be stored in the input character array chars. Note that group lengths that are 10 or longer will be > > split into multiple characters in chars.
>
> After you are done modifying the input array, return the new length of the array.
>
> You must write an algorithm that uses only constant extra space.

## 例題との相違点

+ 自分の回答
  + 力技で配列を操作している
  + インデックスを戻したり、など微妙な調整が必要

```go
func compress(chars []byte) int {
    startIndex := 0
    count := 0
    tmpChar := chars[0]

    for i:=0; i < len(chars); i++ {
        if tmpChar == chars[i] {
            count++
			if i == len(chars) - 1 {
				if count > 1 {
					strCount := strconv.Itoa(count)
					chars = append(chars[:startIndex+1],[]byte(strCount)...)
				}
			}
        }else{
            tmpChar = chars[i]
            if count > 1 {
                strCount := strconv.Itoa(count)
                chars = append(append(chars[:startIndex+1],[]byte(strCount)...),chars[i:]...)
				i = startIndex + len(strCount) + 1
            }
			startIndex = i
			count = 1
        }
    }

    return len(chars)  
}
```

+ ほかの人のシンプルな回答

```go
// ulalawell-San
func compress(chars []byte) int {
	l, r := 0, 0 

    for ;r<len(chars); {
        j := r + 1
        for ;j<len(chars) && chars[j] == chars[j-1]; j++ {} 

        chars[l] = chars[r]
        l++
        if j != r + 1 {
            for _, number := range(strconv.Itoa(j-r)) {
                chars[l] = byte(number)
                l++
            }
        }
        r = j
    }

    chars = chars[:l]
    return len(chars)
}
```

## 相違点

+ シンプルな方は配列を頭から書き換えているのに対して、自分は随時圧縮している
+ 圧縮するから、先頭のほうを書き換えても問題が起こらない。
+ 最後に不要な部分を切り捨てている。

## 感想

+ 配列を都度圧縮するのは新しくメモリを取り直していそう
+ 圧縮→先頭から書き換えても問題ない、この発想がなかった。
