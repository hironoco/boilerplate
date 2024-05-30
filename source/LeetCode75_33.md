---
title: Leetcode75-33
date: 2024-5-30
---
## 説明

+ ポインタでつながったリンク配列がある。
+ このリンク配列を逆順にする

### 原文

---
You are given the head of a linked list. Delete the middle node, and return the head of the modified linked list.

The middle node of a linked list of size n is the ⌊n / 2⌋th node from the start using 0-based indexing, where ⌊x⌋ denotes the largest integer less than or equal to x.

For n = 1, 2, 3, 4, and 5, the middle nodes are 0, 1, 1, 2, and 2, respectively.

---

## 例題との相違点

+ 自分の回答(3ms)
  + tempを用いて、順番にひっくり返した。
  + 普通の配列と違って、ちょっと工夫が必要だが同じやり方。

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

func reverseList(head *ListNode) *ListNode {
	var revList *ListNode

	for head != nil {
		temp := head
		head = head.Next
		temp.Next = revList
		revList = temp
	}
	return revList
}
```

+ 回答例（なし）
  + 例外処理は最初に外している。（その方が難しいこと考えなくていいし、読みやすいかも）

## 感想

+ 例題も同じ処理
