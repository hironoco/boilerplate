---
title: Leetcode75-28
date: 2024-5-26
---
## 説明

+ 3[ac]のような文字列が渡される。
+ これはacが3つという意味で、acacacに変換できる。
+ 以上のルールで、文字列を変換する。

### 原文

---
Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there will not be input like 3a or 2[4].

The test cases are generated so that the length of the output will never exceed 105.

---

## 例題との相違点

+ 自分の回答(1ms)
  + 素直に数字を見つけたら覚えておき、そのあとの[]内の文字列をその数値分つなげるようにしている。
  + 工夫点は再帰的に呼び出せるようにしているところ

```go
func decodeString(s string) string {
	byNum := 0
	useFrame := 0
	result := ""
	stack := ""

	for _, k := range s {
		if k >= '0' && k <= '9' && useFrame == 0 {
			byNum = byNum*10 + int(k-'0')
		} else if k == '[' {
			if useFrame > 0 {
				stack += string(k)
			}
			useFrame += 1
		} else if k == ']' {
			useFrame -= 1
			if useFrame == 0 {
				tmp := decodeString(stack)
				for i := 0; i < byNum; i++ {
					result += tmp
					// result += stack
				}
                stack = ""
                byNum = 0
			} else {
				stack += string(k)
			}
		} else {
			if useFrame == 0 {
				result += string(k)
			} else {
				stack += string(k)
			}
		}
	}

	return result
}
```

+ 回答例（なし）

## 感想

+ 再帰的に実装するのは難しかったが、挑戦してみてよかった。
