---
title: Leetcode75-2
date: 2024-2-25
---

## 例題との相違点

+ 自分の回答
```go
import("strings")

func gcdOfStrings(str1 string, str2 string) string {
    tmpAns := ""
    Ans := ""
    for i:=0; i<len(str1) && i<len(str2) && str1[i] == str2[i]; i++{
        tmpAns += string(str1[i])
        if removeSubstring(str1, tmpAns) == "" && removeSubstring(str2, tmpAns) == ""{
            Ans = tmpAns
        }
    }
    return Ans
}

func removeSubstring(input, substring string) string {
	// 指定した部分文字列を空文字に置換する
	result := strings.Replace(input, substring, "", -1)
	return result
}

```

+ 最速の例題
```go
func gcd(a, b int) int {
	for b != 0 {
		a, b = b, a%b
	}
	return a
}

func gcdOfStrings(str1, str2 string) string {
	gcd := gcd(len(str1), len(str2))
	subst := str1[:gcd]

	for i := 0; i < len(str1); i = i + gcd {
		if subst != str1[i:gcd+i] {
			return ""
		}
	}

	for i := 0; i < len(str2); i = i + gcd {
		if subst != str2[i:gcd+i] {
			return ""
		}
	}

	return subst
}
```

+ 違い
自分：文字列ベースで処理しようとしている。
回答例：文字列の長さが、最小単位の倍数になっていることを考慮して、文字数で最小公倍数を求めている。
文字列より数値のほうが処理が速い。