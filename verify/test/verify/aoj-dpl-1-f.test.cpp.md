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
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :heavy_check_mark: test/verify/aoj-dpl-1-f.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-dpl-1-f.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-21 17:07:30+09:00


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_F">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_F</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/dp/knapsack-01-2.cpp.html">Knapsack-01(0-1ナップサック問題) $O(N \sum {v_i})$ <small>(dp/knapsack-01-2.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_F"

#include "../../template/template.cpp"

#include "../../dp/knapsack-01-2.cpp"

int main() {
  int N, W;
  cin >> N >> W;
  vector< int > v(N), w(N);
  for(int i = 0; i < N; i++) cin >> v[i] >> w[i];
  cout << knapsack_01_2(w, v, W) << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/aoj-dpl-1-f.test.cpp"
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_1_F"

#line 1 "template/template.cpp"
#include<bits/stdc++.h>

using namespace std;

using int64 = long long;
const int mod = 1e9 + 7;

const int64 infll = (1LL << 62) - 1;
const int inf = (1 << 30) - 1;

struct IoSetup {
  IoSetup() {
    cin.tie(nullptr);
    ios::sync_with_stdio(false);
    cout << fixed << setprecision(10);
    cerr << fixed << setprecision(10);
  }
} iosetup;


template< typename T1, typename T2 >
ostream &operator<<(ostream &os, const pair< T1, T2 >& p) {
  os << p.first << " " << p.second;
  return os;
}

template< typename T1, typename T2 >
istream &operator>>(istream &is, pair< T1, T2 > &p) {
  is >> p.first >> p.second;
  return is;
}

template< typename T >
ostream &operator<<(ostream &os, const vector< T > &v) {
  for(int i = 0; i < (int) v.size(); i++) {
    os << v[i] << (i + 1 != v.size() ? " " : "");
  }
  return os;
}

template< typename T >
istream &operator>>(istream &is, vector< T > &v) {
  for(T &in : v) is >> in;
  return is;
}

template< typename T1, typename T2 >
inline bool chmax(T1 &a, T2 b) { return a < b && (a = b, true); }

template< typename T1, typename T2 >
inline bool chmin(T1 &a, T2 b) { return a > b && (a = b, true); }

template< typename T = int64 >
vector< T > make_v(size_t a) {
  return vector< T >(a);
}

template< typename T, typename... Ts >
auto make_v(size_t a, Ts... ts) {
  return vector< decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));
}

template< typename T, typename V >
typename enable_if< is_class< T >::value == 0 >::type fill_v(T &t, const V &v) {
  t = v;
}

template< typename T, typename V >
typename enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {
  for(auto &e : t) fill_v(e, v);
}

template< typename F >
struct FixPoint : F {
  FixPoint(F &&f) : F(forward< F >(f)) {}
 
  template< typename... Args >
  decltype(auto) operator()(Args &&... args) const {
    return F::operator()(*this, forward< Args >(args)...);
  }
};
 
template< typename F >
inline decltype(auto) MFP(F &&f) {
  return FixPoint< F >{forward< F >(f)};
}
#line 4 "test/verify/aoj-dpl-1-f.test.cpp"

#line 1 "dp/knapsack-01-2.cpp"
/**
 * @brief Knapsack-01(0-1ナップサック問題) $O(N \sum {v_i})$
 * @docs docs/knapsack-01-2.md
 */
template< typename T >
T knapsack_01_2(const vector< T > &w, const vector< int > &v, const T &W) {
  const int N = (int) w.size();
  const int sum = accumulate(begin(v), end(v), 0);
  vector< T > dp(sum + 1, W + 1);
  dp[0] = T();
  for(int i = 0; i < N; i++) {
    for(int j = sum; j >= v[i]; j--) {
      dp[j] = min(dp[j], dp[j - v[i]] + w[i]);
    }
  }
  int ret = 0;
  for(int i = 0; i <= sum; i++) {
    if(dp[i] <= W) ret = i;
  }
  return ret;
}
#line 6 "test/verify/aoj-dpl-1-f.test.cpp"

int main() {
  int N, W;
  cin >> N >> W;
  vector< int > v(N), w(N);
  for(int i = 0; i < N; i++) cin >> v[i] >> w[i];
  cout << knapsack_01_2(w, v, W) << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

