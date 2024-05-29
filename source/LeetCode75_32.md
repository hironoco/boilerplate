---
title: Leetcode75-32
date: 2024-5-29
---
## 説明

+ ポインタでつながったリンク配列がある。
+ 最初のインデックスを1としたときに、奇数のインデックスの要素を先頭に、偶数のインデックスの要素を後方にまとめる。

### 原文

---
You are given the head of a linked list. Delete the middle node, and return the head of the modified linked list.

The middle node of a linked list of size n is the ⌊n / 2⌋th node from the start using 0-based indexing, where ⌊x⌋ denotes the largest integer less than or equal to x.

For n = 1, 2, 3, 4, and 5, the middle nodes are 0, 1, 1, 2, and 2, respectively.

---

## 例題との相違点

+ 自分の回答(3ms)
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

func oddEvenList(head *ListNode) *ListNode {
	oddList := head
	evenList := &ListNode{}
	evenHead := evenList

	for oddList != nil && evenList != nil {
		evenList.Next = oddList.Next
		evenList = evenList.Next
        if oddList.Next == nil {
			break
		}
		oddList.Next = oddList.Next.Next
		if oddList.Next == nil {
			break
		}
		oddList = oddList.Next

	}

	if oddList != nil && oddList != nil {
		oddList.Next = evenHead.Next
	}

	return head
}
```

+ 回答例（0ms）
  + 例外処理は最初に外している。（その方が難しいこと考えなくていいし、読みやすいかも）

```go
func oddEvenList(head *ListNode) *ListNode {
    if head == nil {
        return nil
    }
    if head.Next == nil {
        return head
    }
    start := &ListNode{}
    end := &ListNode{}
    startHead := start
    endHead := end

    odd, even := head, head.Next
    for odd != nil && even != nil {
        start.Next = odd
        start = start.Next
        if odd.Next != nil && odd.Next.Next != nil{
            odd = odd.Next.Next
        } else {
            odd = nil
        }
        end.Next = even
        end = end.Next
        if even.Next != nil && even.Next.Next != nil{
            even = even.Next.Next
        } else{
            even = nil
        }
    }

    if odd != nil  {
        start.Next = odd
        start = start.Next
    } else if even != nil {
        end.Next = even
        end = end.Next
    }

    if endHead.Next != nil {
        start.Next = endHead.Next
        end.Next = nil
    } else {
        start.Next = nil
    }
    return startHead.Next
}
```

## 感想

+ 内部の処理見たらあまり違いがなかったが、何回か実行したら例題でも3msとかになった。
+ 違いはない。
