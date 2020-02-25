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


# :heavy_check_mark: test/verify/yosupo-maximum-independent-set-2.test.cpp

<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-maximum-independent-set-2.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-25 22:57:51+09:00


* see: <a href="https://judge.yosupo.jp/problem/maximum_independent_set">https://judge.yosupo.jp/problem/maximum_independent_set</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/others/maximum-clique.cpp.html">Maximum-Clique(最大クリーク) <small>(graph/others/maximum-clique.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/maximum_independent_set"

#include "../../template/template.cpp"

#include "../../graph/others/maximum-clique.cpp"

int main() {
  int V, E;
  cin >> V >> E;
  auto D = make_v< int >(V, V);
  for(int i = 0; i < E; i++) {
    int a, b;
    cin >> a >> b;
    D[a][b] = D[b][a] = true;
  }
  MaximumClique< 40 > mc(V);
  for(int i = 0; i < V; i++) {
    for(int j = 0; j < i; j++) {
      if(!D[i][j]) mc.add_edge(i, j);
    }
  }
  auto ret = mc.solve();
  cout << ret.size() << "\n";
  cout << ret << "\n";
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-maximum-independent-set-2.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/maximum_independent_set"

#line 1 "test/verify/../../template/template.cpp"
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
#line 4 "test/verify/yosupo-maximum-independent-set-2.test.cpp"

#line 1 "test/verify/../../graph/others/maximum-clique.cpp"
/**
 * @brief Maximum-Clique(最大クリーク)
 */
template< int V >
struct MaximumClique {
  using B = bitset< V >;
  vector< B > g, col_buf;

  struct P {
    int idx, col, deg;

    P(int idx, int col, int deg) : idx(idx), col(col), deg(deg) {}
  };

  MaximumClique() = default;

  explicit MaximumClique(int N) : g(N), col_buf(N) {}

  void add_edge(int a, int b) {
    g[a].set(b);
    g[b].set(a);
  }

  vector< int > now, clique;

  void dfs(vector< P > &rem) {
    if(clique.size() < now.size()) clique = now;
    sort(begin(rem), end(rem), [](const P &a, const P &b) {
      return a.deg > b.deg;
    });
    int max_c = 1;
    for(auto &p : rem) {
      p.col = 0;
      while((g[p.idx] & col_buf[p.col]).any()) ++p.col;
      max_c = max(max_c, p.idx + 1);
      col_buf[p.col].set(p.idx);
    }
    for(int i = 0; i < max_c; i++) col_buf[i].reset();
    sort(begin(rem), end(rem), [&](const P &a, const P &b) {
      return a.col < b.col;
    });
    for(; !rem.empty(); rem.pop_back()) {
      auto &p = rem.back();
      if(now.size() + p.col + 1 <= clique.size()) break;
      vector< P > nrem;
      B bs;
      for(auto &q : rem) {
        if(g[p.idx][q.idx]) {
          nrem.emplace_back(q.idx, -1, 0);
          bs.set(q.idx);
        }
      }
      for(auto &q : nrem) {
        q.deg = (bs & g[q.idx]).count();
      }
      now.emplace_back(p.idx);
      dfs(nrem);
      now.pop_back();
    }
  }

  vector< int > solve() {
    vector< P > remark;
    for(int i = 0; i < g.size(); i++) {
      remark.emplace_back(i, -1, (int) g[i].size());
    }
    dfs(remark);
    return clique;
  }
};
#line 6 "test/verify/yosupo-maximum-independent-set-2.test.cpp"

int main() {
  int V, E;
  cin >> V >> E;
  auto D = make_v< int >(V, V);
  for(int i = 0; i < E; i++) {
    int a, b;
    cin >> a >> b;
    D[a][b] = D[b][a] = true;
  }
  MaximumClique< 40 > mc(V);
  for(int i = 0; i < V; i++) {
    for(int j = 0; j < i; j++) {
      if(!D[i][j]) mc.add_edge(i, j);
    }
  }
  auto ret = mc.solve();
  cout << ret.size() << "\n";
  cout << ret << "\n";
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

