---
title: Leetcode75-30
date: 2024-5-27
---
## 説明

+ 2種類の議会の参加者が記録された配列がある。
+ 参加者はもう1方の参加者を退場させることができる
+ 相手の参加者をすべて退場させたら勝ち
+ 参加者は左から順にほかの参加者を退場させていく
+ 全員が最適な行動をとった際に勝つ議会を返す

### 原文

---
In the world of Dota2, there are two parties: the Radiant and the Dire.

The Dota2 senate consists of senators coming from two parties. Now the Senate wants to decide on a change in the Dota2 game. The voting for this change is a round-based procedure. In each round, each senator can exercise one of the two rights:

Ban one senator's right: A senator can make another senator lose all his rights in this and all the following rounds.
Announce the victory: If this senator found the senators who still have rights to vote are all from the same party, he can announce the victory and decide on the change in the game.
Given a string senate representing each senator's party belonging. The character 'R' and 'D' represent the Radiant party and the Dire party. Then if there are n senators, the size of the given string will be n.

The round-based procedure starts from the first senator to the last senator in the given order. This procedure will last until the end of voting. All the senators who have lost their rights will be skipped during the procedure.

Suppose every senator is smart enough and will play the best strategy for his own party. Predict which party will finally announce the victory and change the Dota2 game. The output should be "Radiant" or "Dire".

---

## 例題との相違点

+ 自分の回答(8ms)
  + 権利実行前の議員の数を格納するmapを使った。
  + 権利を実行したら結果配列に格納する。
  + 最後に権利を実行してない人が残る場合は、結果配列の先頭から相手側の議員を除く。
  + 議員を除くか、除く議員がいなくなったら結果配列に入れる。
  + 今回も再帰的に呼び出してターン制を実現している

```go
func predictPartyVictory(senate string) string {

	noVotingCount := make(map[byte]int)
	result := []byte{}
	count := make(map[byte]int)

	for _, v := range senate {
		if v == 'R' {
			if noVotingCount['D'] > 0 {
				noVotingCount['D']--
				result = append(result, 'D')
				count['D']++
			} else {
				noVotingCount['R']++
			}
		} else {
			if noVotingCount['R'] > 0 {
				noVotingCount['R']--
				result = append(result, 'R')
				count['R']++
			} else {
				noVotingCount['D']++
			}
		}
	}

	for i := 0; i < noVotingCount['R']; i++ {
		if count['D'] > 0 {
			result, _ = removeFirstChar(result, 'D')
			count['D']--
		}
		result = append(result, 'R')
		count['R']++
	}
	for i := 0; i < noVotingCount['D']; i++ {
		if count['R'] > 0 {
			result, _ = removeFirstChar(result, 'R')
			count['R']--
		}
		result = append(result, 'D')
		count['D']++
	}

	if count['R'] > 0 && count['D'] > 0 {
		return predictPartyVictory(string(result))
	} else if count['R'] == 0 {
		return "Dire"
	} else {
		return "Radiant"
	}

}

func removeFirstChar(list []byte, char byte) ([]byte, bool) {
	for i, v := range list {
		if v == char {
			return append(list[:i], list[i+1:]...), true
		}
	}
	return list, false
}
```

+ 回答例（0ms）
  + radiantとDireの配列を作り、それぞれ度のインデックスにいるかを格納している。
  + インデックス0を比較し、小さい方の配列の後ろに、配列の長さ+インデックス0の値を格納している。
  + for文を回す中で、0のインデックスは除いている。
  + これを繰り返すと、配列が短くなっていき、最終的に0になる。
  + 配列の長さが長い方が勝ち

```go
func predictPartyVictory(senate string) string {
    radiant, dire := make([]int, 0), make([]int, 0)

    for i := 0; i < len(senate); i++ {
        if senate[i] == 'R' {
            radiant = append(radiant, i)
        } else {
            dire = append(dire, i)
        }
    }


    for len(radiant) > 0 && len(dire) > 0 {
        if radiant[0] < dire[0] {
            radiant = append(radiant, len(senate) + radiant[0])
        } else {
            dire = append(dire, len(senate) + dire[0])
        }
        dire, radiant = dire[1:], radiant[1:]
    }
    
    if len(dire) > len(radiant) {
        return "Dire"
    }
    return "Radiant"
}
```

## 感想

+ そのアルゴリズムは全く分からなかった。
+ 何回もappendするけど早いのか？
+ 自分のやつも結構appendしていた。
+ 追加するものが、単体なのか配列なのかで速さが変わっていそう。
+ 配列を追加するとその長さ分単一追加のappendをしているのと同じ。
