---
title: Leetcode75-29
date: 2024-5-26
---
## 説明

+ RecentCounterというクラスを実装する。
+ これは過去に送られたリクエストを保持する。
+ 初期化するとき（コンストラクタが呼ばれたとき）リクエストがない状態で初期化する。
+ pingをリクエストすると、過去3000ms以内に何回リクエストがあったか返す。

### 原文

---
You have a RecentCounter class which counts the number of recent requests within a certain time frame.

Implement the RecentCounter class:

RecentCounter() Initializes the counter with zero recent requests.
int ping(int t) Adds a new request at time t, where t represents some time in milliseconds, and returns the number of requests that has happened in the past 3000 milliseconds (including the new request). Specifically, return the number of requests that have happened in the inclusive range [t - 3000, t].
It is guaranteed that every call to ping uses a strictly larger value of t than the previous call.

---

## 例題との相違点

+ 自分の回答(317ms)
  + 過去のリクエストを保持するための配列を構造体に定義している
  + 初期化のときは、その配列をからの配列で初期化している。
  + Pingのときには配列に今の引数を追加したのち、過去3000ms以内のリクエスト数を数えて返している。

```go
type RecentCounter struct {
    request []int
}


func Constructor() RecentCounter {
    return RecentCounter{
        request: make([]int, 0),
    }
}


func (this *RecentCounter) Ping(t int) int {
    this.request = append(this.request, t)
    count := 0

    for _, v := range this.request{
        if v >= t -3000 {
            count++
        }
    }
    return count
}


/**
 * Your RecentCounter object will be instantiated and called as such:
 * obj := Constructor();
 * param_1 := obj.Ping(t);
 */
```

+ 回答例（85ms）
  + 配列の初期化にmakeを使ってない
  + 数を数えるのではなく、3000ms以前の要素は切り捨てて、配列の長さを返している。

```go
type RecentCounter struct {
    recorder []int
}


func Constructor() RecentCounter {
    return RecentCounter{
        recorder : []int{},
    }
}


func (this *RecentCounter) Ping(t int) int {

    this.recorder = append(this.recorder, t)
    // fmt.Println(this.recorder)
    if t > 3000{
        lowerLimit, index := t-3000, 0
        for ;index < len(this.recorder); index++{
            if this.recorder[index] >= lowerLimit{
                break
            }
        }
        this.recorder = this.recorder[index:]
        // fmt.Println(lowerLimit, this.recorder)
    }    
    return len(this.recorder)
}
```

## 感想

+ for文内で特定の条件のときだけ処理が走るから早いのか？
