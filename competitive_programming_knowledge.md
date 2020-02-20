competitive_programming_knowledge.md
---
# 競プロ知識まとめ
※色は目安です

## 〜緑
- C++基本文法

- STLの知識
  - はじめはこれを参照しながらコンテスト出ていた(https://www.qoosky.io/techs/5cd1a59497)

## 〜水
- ダイクストラ、ワーシャルフロイド

- 1次元状の区間の数え上げで左端か右端を固定したときの場合の数を高速に求める

- グラフのDFSはprevを持っておくと簡単にかける(usedのboolの配列を使う必要がなくなる)

- グリッドグラフ上の構築で連結性を保ちたいときにギザギザ
  - https://codeforces.com/contest/1254/submission/65362266

- 非負整数`x`の桁数は`to_string(x).size()`で求まる！
  - https://atcoder.jp/contests/abc146/tasks/abc146_c

- グリッドは二部グラフ！
  - 1次元 https://codeforces.com/contest/1264/problem/B
  - 2次元 市松模様 https://codeforces.com/contest/1268/problem/B

## 〜青
- ベルマンフォード
  - 始点から負閉路を経由して到達できる頂点の検出は少しややこしい(https://atcoder.jp/contests/abc137/submissions/8174983)
  
- 周期性のあるものは計算量調和級数を疑う
  - https://onlinejudge.u-aizu.ac.jp/services/room.html#HUPC2019Day2/problems/F
  
- 1次元上の、距離の絶対値の和の最小化する点は中央値
  - これはかなり非自明に感じた(黄-橙ぐらいかも)(https://codeforces.com/contest/1254/submission/65411564)
  
- d進数での繰り上がりのときの不変量に注目する系
  - https://atcoder.jp/contests/ddcc2020-qual/tasks/ddcc2020_qual_d
  
- next[i][j]: 文字列Sのi番目以降で初めてjが現れるindexを事前計算する系
  - https://atcoder.jp/contests/sumitrust2019/submissions/8735709

- 1,2,3,...,nの部分和で1~n(n+1)/2の全てを表せる(大きい方から貪欲)
  - https://codeforces.com/contest/1072/submission/66305676

- モノイド列について、各a_iを取り除いたときの合成は、左右からの累積を計算しておけば高速に求まる
  - ナップサックdpバージョン https://atcoder.jp/contests/abc145/tasks/abc145_e
    - この問題解き方が３つあって教育的 https://sen-comp.hatenablog.com/entry/2019/11/17/003150

- 中央値へ移動するための距離をオンラインで管理
  - https://atcoder.jp/contests/abc127/submissions/5682940
  - https://codeforces.com/contest/1268/submission/67359861
  
- 桁dp
dp[i][j]...: 上からi桁目まで見てjなら緩和されていて(!jならgirigiri)条件kの場合の数
```
REP(i, n) {
  REP(j, 2) {
    REP(d, j ? 10 : s[i] - '0' + 1) {
      dp[i + 1][j | (d < s[i] - '0')] += dp[i][j];
    }
  }
}
```
  - https://atcoder.jp/contests/abc154/tasks/abc154_e
  - 上界と下界がある典型 https://abc007.contest.atcoder.jp/submissions/10042746

## 〜黄
- 木上のパス(u, v)は(root, u), (root, v), 2 * (root, LCA(u, v))に分解できる
  - https://atcoder.jp/contests/abc133/submissions/6314387

- 左右の違いを気にしないといけないときに分割統治するとlogをつけてそれを無視できる
  - https://onlinejudge.u-aizu.ac.jp/services/room.html#HUPC2019Day2/problems/H
  
- ブルーフカ
  - セグ木とかと一緒に使って殴れることが多いイメージ https://codeforces.com/contest/1242/submission/64478638
  
- 上と同じ問題、グラフの次数の最小値は2m/n以下なので、その近傍についてO(n)かけてもO(m)になる(疎グラフの嬉しい性質) https://codeforces.com/contest/1242/submission/64455567

- setとかをうまく使うと償却が高速化される系
  - https://atcoder.jp/contests/abc128/tasks/abc128_e
  - https://atcoder.jp/contests/abc127/tasks/abc127_f
  - https://csacademy.com/contest/fii-code-2019-final-round-online-mirror/task/dazzling-trams/
  - https://codeforces.com/contest/1242/submission/64454203 (上と同じ最小全域木問題)

- 二乗の木DP
  - https://codeforces.com/contest/1266/submission/67106367

- DPでvalの値の種類が少ないときにkeyとvalを入れ替えて高速化
  - https://atcoder.jp/contests/agc033/tasks/agc033_d

- 最小費用流: 2部グラフの最小割り当て・被らないような複数本のコスト最小のパスを見つける

- minmax法を符号マイナスで書くときは
  - for (child : g[v]) chmax(ma, -dfs(child));
  - 符号こんがらがりやいので注意
    - https://onlinejudge.u-aizu.ac.jp/problems/2713

- n頂点、m辺のグラフには次数2m/n以下の頂点がある
  - 次数最小の頂点全てにO(n)の操作を行っても合計でO(m)->疎グラフのときに嬉しい！
    - https://codeforces.com/contest/1242/submission/64455567
    
- 基本の耳dp(問題に直接書かれていない定数個の状態の遷移に帰着するdp)
  - https://codeforces.com/contest/1257/submission/65451841 (これはLISでもできる)
  
- トーナメント表の性質
  - 優勝するための条件 https://codeforces.com/contest/1260/submission/66260024

- 隣接要素に影響が及ぶ操作をする系 -> 累積か差分を考える (TODO: まだどういうときにうまくいくのか理解してない!)
  - https://codeforces.com/contest/1110/problem/E
  - https://atcoder.jp/contests/dwacon5th-final-open/tasks/dwacon5th_final_b
  
- 極限考えて立式する系の期待値計算
  - E[i]:iを抜けるために必要な試行回数の期待値 https://codeforces.com/contest/1264/submission/66382913
  - TODO: https://tdpc.contest.atcoder.jp/tasks/tdpc_ball

- iから{i+k,i+2k,i+3k,...},{i-k,i-2k,i-3k}に対して操作をしたくなったときは整数の集合をmod kで分けることを考える
  - https://atcoder.jp/contests/abc147/tasks/abc147_f\

- 区間をイベントソートして走査するやつ
  - multisetに入れたり出したりする、今入ってるものが区間としてかぶっている https://codeforces.com/contest/1284/problem/D

- stack使う系
  - https://codeforces.com/contest/1299/problem/C


## 〜橙
- 複数回やるともとに戻る操作(行列の転置とか)を遅延セグ木に載せたいときは、候補を全て持っておいてswapとかするとうまくい(https://codeforces.com/contest/1252/submission/63677635)

- 2次元グリッド状を上か右に動いて目的地に達する方法を数え上げる問題で、途中である直線上を通るものの個数
  - 初めてその直線上に達した地点以降の経路をその直線を中心に折り返すテクニック（カタラン数の一般式の証明にも使える）が使える(https://onlinejudge.u-aizu.ac.jp/status/users/knshnb/submissions/1/2836/judge/3940086/C++14)
  
- 場合分け面倒くさい、最適な区間をO(n)で求める問題は耳dpでうまく書けることがある
  - https://codeforces.com/contest/1239/submission/65450821

- 2次元グリッド状を上か右に動いて目的地に達する方法を数え上げる問題で、途中である直線上を通るものの個数

- 単調性がなくてもtrue, falseの区切りを一つ求めるのに二分法は使える
  - https://atcoder.jp/contests/ddcc2020-qual/submissions/8594615

- Alien DP: ラグランジュ緩和っぽいことをして次元を落としてにぶたんする(判定でdp)
  - https://twitter.com/yosupot/status/928313911891214336
  - https://twitter.com/snuke_/status/928314561890959360
  - https://codeforces.com/contest/1279/problem/F
    - まだ証明できてない

- 2次元グリッド上の構築パズル
  - https://atcoder.jp/contests/agc041/tasks/agc041_c
  
  
- combinationの式変形
  - (1+x)^nのx^cの係数 = (1+x)^(n-c) * (1+x^-1)^cの定数項として等比数列の和の公式使うと結構色々示せる
    - https://atcoder.jp/contests/abc154/tasks/abc154_f

competitive_programming_note.md
---
# 競プロ注意点まとめ
※色は目安です

## 〜緑
- C++でvector::size() - 1とかやると0のときにアンダーフローする

## 〜水
- 演算子の優先順位
  - `x + y < z` vs `x + (y < z)`
  - `x + 1LL << y1` vs `x + (1LL << y1)`

## 〜青
- using mint = double;
をするとfactがオーバーフローして0になる！

- ifで条件分岐してcontinueしたときに全体で共通処理したいやつまでcontinueされないか注意！！！
```
   int cur = 0;
    for (char c : s) {
        if (c == 'X') {
            if (cur < b) {
                continue;
            } else if (cur < a) {
                no();
                return;
            } else {
                d.push_back(cur);
            }
            cur = 0;
        } else {
            cur++;
        }
    }
```

## 〜黄
- dfsで葉に達したときにreturnする処理を書きたいときに
  - if (g[v].size() == 1) return hoge;
  - って書くと根の次数が1のときに死ぬの罠だな

- 凸関数を最大値で左右に分けるとそれぞれ(狭義)単調増加・単調減少になる。このときに最大値が２つあるコーナーケースに注意！
  - https://codeforces.com/contest/1254/submission/65411064

- うまい実装集
  - https://atcoder.jp/contests/agc041/submissions/9180689
  
## 〜橙


