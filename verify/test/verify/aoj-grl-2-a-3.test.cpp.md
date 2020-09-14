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


# :heavy_check_mark: test/verify/aoj-grl-2-a-3.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-grl-2-a-3.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-08 23:29:00+09:00


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/mst/boruvka.cpp.html">Boruvka(最小全域木) <small>(graph/mst/boruvka.cpp)</small></a>
* :question: <a href="../../../library/structure/union-find/union-find.cpp.html">Union-Find <small>(structure/union-find/union-find.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A"

#include "../../template/template.cpp"

#include "../../structure/union-find/union-find.cpp"

#include "../../graph/mst/boruvka.cpp"

int main() {
  int V, E;
  cin >> V >> E;
  vector< int > X(E), Y(E), Z(E);
  for(int i = 0; i < E; i++) {
    cin >> X[i] >> Y[i] >> Z[i];
  }
  Boruvka< int > mst(V);
  auto f = [&](vector< pair< int, int > > &ret) {
    for(int i = 0; i < E; i++) {
      X[i] = mst.find(X[i]);
      Y[i] = mst.find(Y[i]);
      if(X[i] == Y[i]) continue;
      ret[X[i]] = min(ret[X[i]], make_pair(Z[i], Y[i]));
      ret[Y[i]] = min(ret[Y[i]], make_pair(Z[i], X[i]));
    }
    return ret;
  };
  cout << mst.build(f) << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/aoj-grl-2-a-3.test.cpp"
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_A"

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
#line 4 "test/verify/aoj-grl-2-a-3.test.cpp"

#line 1 "structure/union-find/union-find.cpp"
/**
 * @brief Union-Find
 * @docs docs/union-find.md
 */
struct UnionFind {
  vector< int > data;

  UnionFind() = default;

  explicit UnionFind(size_t sz) : data(sz, -1) {}

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return false;
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return true;
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return data[k] = find(data[k]);
  }

  int size(int k) {
    return -data[find(k)];
  }

  bool same(int x, int y) {
    return find(x) == find(y);
  }
};
#line 6 "test/verify/aoj-grl-2-a-3.test.cpp"

#line 1 "graph/mst/boruvka.cpp"
/**
 * @brief Boruvka(最小全域木)
 * @docs docs/boruvka.md
 */
template< typename T >
struct Boruvka {
private:
  size_t V;
  const T INF;
  UnionFind uf;

public:
  explicit Boruvka(size_t V, T INF = numeric_limits< T >::max()) : V(V), uf(V), INF(INF) {}

  inline int find(int k) {
    return uf.find(k);
  }

  template< typename F >
  T build(const F &update) {
    T ret = T();
    while(uf.size(0) < V) {
      vector< pair< T, int > > v(V, make_pair(INF, -1));
      update(v);
      bool con = false;
      for(int i = 0; i < V; i++) {
        if(v[i].second >= 0 && uf.unite(i, v[i].second)) {
          ret += v[i].first;
          con = true;
        }
      }
      if(!con) return INF;
    }
    return ret;
  }
};
#line 8 "test/verify/aoj-grl-2-a-3.test.cpp"

int main() {
  int V, E;
  cin >> V >> E;
  vector< int > X(E), Y(E), Z(E);
  for(int i = 0; i < E; i++) {
    cin >> X[i] >> Y[i] >> Z[i];
  }
  Boruvka< int > mst(V);
  auto f = [&](vector< pair< int, int > > &ret) {
    for(int i = 0; i < E; i++) {
      X[i] = mst.find(X[i]);
      Y[i] = mst.find(Y[i]);
      if(X[i] == Y[i]) continue;
      ret[X[i]] = min(ret[X[i]], make_pair(Z[i], Y[i]));
      ret[Y[i]] = min(ret[Y[i]], make_pair(Z[i], X[i]));
    }
    return ret;
  };
  cout << mst.build(f) << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

