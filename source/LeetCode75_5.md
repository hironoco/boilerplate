---
title: Leetcode75-5
date: 2024-3-13
---

## 例題との相違点

+ 自分の回答（343ms）

```go
func reverseVowels(s string) string {

	i := 0
	j := len(s)-1
	var resultFront string
	var resultBack string

	isFrontVowel := false
	isBackVowel := false

	for i <= j {
		isFrontVowel = isVowels(s[i])
		isBackVowel = isVowels(s[j])

        if i == j {
            resultFront += string(s[i])
            break
        }

		if !isFrontVowel {
			resultFront = resultFront + string(s[i])
			i++
		}

		if !isBackVowel {
			resultBack = string(s[j]) + resultBack
			j--
		}

		if isFrontVowel && isBackVowel {
			resultFront = resultFront + string(s[j])
			resultBack = string(s[i]) + resultBack
			i++
			j--
			isFrontVowel = false
			isBackVowel = false
		}
	}
	resultFront = resultFront + resultBack
	return resultFront
}

func isVowels(s byte) bool {
    if s == 'a' || s == 'e' || s == 'i' || s == 'o' || s == 'u' || s == 'A' || s == 'E' || s == 'I' || s == 'O' || s == 'U' {
        return true
    }
    return false
}
```

+ 最速の例題

```go
func reverseVowels(s string) string {
	bs := []byte(s)
	for f, b := 0, len(bs)-1; f < b; {
		if !vowel(bs[f]) {
			f++
		}

		if !vowel(bs[b]) {
			b--
		}

		if vowel(bs[f]) && vowel(bs[b]) {
			fv := bs[f]
			bs[f] = bs[b]
			bs[b] = fv

			f++
			b--
		}
	}

	return string(bs)
}

func vowel(b byte) bool {
	switch b {
	case 'a', 'A', 'e', 'E', 'i', 'I', 'o', 'O', 'u', 'U':
		return true
	}
	return false
}
```

+ 違い
  + 基本的にbyte型で処理している。
    + Stringは可変のため時間がかかりそう。
  + 母音判定はswitch-caseで行っている。
  + 無駄に変数を宣言しすぎている
    + 文字列は元のやつをbyte型配列にして再利用している。

+ 検証
  + String型で扱っていたのをByteに直したら121msになった（220msの短縮）
  + if文をswitch-caseにしたら遅くなった。
  + 元の文字列をbyteに直して再利用したら5msになった
  + 以下の形が、最も早かった

```go
func reverseVowels(s string) string {

	bs := []byte(s)

	i := 0
	j := len(s) - 1
	isFrontVowel := false
	isBackVowel := false

	for i <= j {
		isFrontVowel = isVowels(s[i])
		isBackVowel = isVowels(s[j])

		if !isFrontVowel {
			i++
		}

		if !isBackVowel {
			j--
		}

		if isFrontVowel && isBackVowel {
			buf := bs[i]
			bs[i] = bs[j]
			bs[j] = buf
			i++
			j--
		}
	}

	return string(bs)
}

func isVowels(s byte) bool {
	if s == 'a' || s == 'e' || s == 'i' || s == 'o' || s == 'u' || s == 'A' || s == 'E' || s == 'I' || s == 'O' || s == 'U' {
		return true
	}
	return false
}
```

## 感想

+ プログラミングではなく、一般的に考えたら箱を移し替えるのは労力がかかる。
+ アルゴリズムの大枠ができたら一般的にしてどうやったら早いか考えてみるとよいかもしれない。