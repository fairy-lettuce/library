---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../assets/css/copy-button.css" />


# :heavy_check_mark: Knapsack-Limitations(個数制限つきナップサック問題) $O(N^2 \max(v_i)^2)$ <small>(dp/knapsack-limitations-2.cpp)</small>

<a href="../../index.html">Back to top page</a>

* category: <a href="../../index.html#95687afb5d9a2a9fa39038f991640b0c">dp</a>
* <a href="{{ site.github.repository_url }}/blob/master/dp/knapsack-limitations-2.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-15 00:43:54+09:00




## 概要

個数制限つきナップサック問題を次に示す.

重さ $w_i$, 価値 $v_i$ であるような $N$ 種類の品物がある. $i$ 番目の品物は $m_i$ 個まで選ぶことができる. 重さの和が $W$ 以下となるように選ぶとき, 価値の最大値を求めよ.

まず「dp[価値の和]:= 重さの和の最小値」をある程度の大きさ($N \max(v_i)^2$)まで求める。残りの分は, 効率が良い順(価値/重さが大きい順)に貪欲にとってもいいことが示せて, なんかできる(c).

* `knapsack_limitations(w, m, v, W)`: 価値の最大値を求める. 

## 計算量

* $O(N^2 \max(v_i)^2)$


## Depends on

* :heavy_check_mark: <a href="knapsack-limitations.cpp.html">Knapsack-Limitations(個数制限つきナップサック問題) $O(NW)$ <small>(dp/knapsack-limitations.cpp)</small></a>


## Verified with

* :heavy_check_mark: <a href="../../verify/test/verify/aoj-dpl-1-i.test.cpp.html">test/verify/aoj-dpl-1-i.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#include "knapsack-limitations.cpp"

/**
 * @brief Knapsack-Limitations(個数制限つきナップサック問題) $O(N^2 \max(v_i)^2)$
 * @docs docs/knapsack-limitations-2.md
 */
template< typename T >
T knapsack_limitations(const vector< T > &w, const vector< T > &m, const vector< int > &v,
                       const T &W) {
  const int N = (int) w.size();
  auto v_max = *max_element(begin(v), end(v));
  if(v_max == 0) return 0;
  vector< int > ma(N);
  vector< T > mb(N);
  for(int i = 0; i < N; i++) {
    ma[i] = min< T >(m[i], v_max - 1);
    mb[i] = m[i] - ma[i];
  }
  T sum = 0;
  for(int i = 0; i < N; i++) sum += ma[i] * v[i];
  auto dp = knapsack_limitations(v, ma, w, sum, T(-1), less<>());
  vector< int > ord(N);
  iota(begin(ord), end(ord), 0);
  sort(begin(ord), end(ord), [&](int a, int b) {
    return v[a] * w[b] > v[b] * w[a];
  });
  T ret = T();
  for(int i = 0; i < dp.size(); i++) {
    if(dp[i] > W || dp[i] == -1) continue;
    T rest = W - dp[i], cost = i;
    for(auto &p : ord) {
      auto get = min(mb[p], rest / w[p]);
      if(get == 0) break;
      cost += get * v[p];
      rest -= get * w[p];
    }
    ret = max(ret, cost);
  }
  return ret;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "dp/knapsack-limitations.cpp"
/**
 * @brief Knapsack-Limitations(個数制限つきナップサック問題) $O(NW)$
 * @docs docs/knapsack-limitations.md
 */
template< typename T, typename Compare = greater< T > >
vector< T > knapsack_limitations(const vector< int > &w, const vector< int > &m, const vector< T > &v,
                                 const int &W, const T &NG, const Compare &comp = Compare()) {
  const int N = (int) w.size();
  vector< T > dp(W + 1, NG), deqv(W + 1);
  dp[0] = T();
  vector< int > deq(W + 1);
  for(int i = 0; i < N; i++) {
    for(int a = 0; a < w[i]; a++) {
      int s = 0, t = 0;
      for(int j = 0; w[i] * j + a <= W; j++) {
        if(dp[w[i] * j + a] != NG) {
          auto val = dp[w[i] * j + a] - j * v[i];
          while(s < t && comp(val, deqv[t - 1])) --t;
          deq[t] = j;
          deqv[t++] = val;
        }
        if(s < t) {
          dp[j * w[i] + a] = deqv[s] + j * v[i];
          if(deq[s] == j - m[i]) ++s;
        }
      }
    }
  }
  return dp;
}
#line 2 "dp/knapsack-limitations-2.cpp"

/**
 * @brief Knapsack-Limitations(個数制限つきナップサック問題) $O(N^2 \max(v_i)^2)$
 * @docs docs/knapsack-limitations-2.md
 */
template< typename T >
T knapsack_limitations(const vector< T > &w, const vector< T > &m, const vector< int > &v,
                       const T &W) {
  const int N = (int) w.size();
  auto v_max = *max_element(begin(v), end(v));
  if(v_max == 0) return 0;
  vector< int > ma(N);
  vector< T > mb(N);
  for(int i = 0; i < N; i++) {
    ma[i] = min< T >(m[i], v_max - 1);
    mb[i] = m[i] - ma[i];
  }
  T sum = 0;
  for(int i = 0; i < N; i++) sum += ma[i] * v[i];
  auto dp = knapsack_limitations(v, ma, w, sum, T(-1), less<>());
  vector< int > ord(N);
  iota(begin(ord), end(ord), 0);
  sort(begin(ord), end(ord), [&](int a, int b) {
    return v[a] * w[b] > v[b] * w[a];
  });
  T ret = T();
  for(int i = 0; i < dp.size(); i++) {
    if(dp[i] > W || dp[i] == -1) continue;
    T rest = W - dp[i], cost = i;
    for(auto &p : ord) {
      auto get = min(mb[p], rest / w[p]);
      if(get == 0) break;
      cost += get * v[p];
      rest -= get * w[p];
    }
    ret = max(ret, cost);
  }
  return ret;
}

```
{% endraw %}

<a href="../../index.html">Back to top page</a>

