---
title: Leetcode75-31
date: 2024-5-29
---
## 説明

+ ポインタでつながったリンク配列がある。
+ この配列の長さの半分の整数値（7なら3）のインデックスの要素を削除したものを返す。

### 原文

---
You are given the head of a linked list. Delete the middle node, and return the head of the modified linked list.

The middle node of a linked list of size n is the ⌊n / 2⌋th node from the start using 0-based indexing, where ⌊x⌋ denotes the largest integer less than or equal to x.

For n = 1, 2, 3, 4, and 5, the middle nodes are 0, 1, 1, 2, and 2, respectively.

---

## 例題との相違点

+ 自分の回答(248ms)
  + 配列の最初にダミーの要素を追加した。
  + これにより、次の次を参照してもエラーにならなくなった。
  + 基本的には長さを求めて、半分の阿多愛を出して、先頭からたどって削除対象のインデックスになったら、nextをnext.nextに置き換える。

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

func deleteMiddle(head *ListNode) *ListNode {
	dummy := &ListNode{Next: head}
	length := 0
	for node := head; node != nil; node = node.Next {
		length++
	}

	delIndex := length / 2
	workHead := dummy
	for i := 0; i < delIndex; i++ {
		workHead = workHead.Next
	}

	workHead.Next = workHead.Next.Next
	return dummy.Next
}
```

+ 回答例（なし）

## 感想

+ そのアルゴリズムは全く分からなかった。
+ 何回もappendするけど早いのか？
+ 自分のやつも結構appendしていた。
+ 追加するものが、単体なのか配列なのかで速さが変わっていそう。
+ 配列を追加するとその長さ分単一追加のappendをしているのと同じ。
