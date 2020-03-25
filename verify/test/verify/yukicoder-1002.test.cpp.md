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


# :heavy_check_mark: test/verify/yukicoder-1002.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-1002.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-26 01:18:25+09:00


* see: <a href="https://yukicoder.me/problems/no/1002">https://yukicoder.me/problems/no/1002</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/graph-template.cpp.html">graph/graph-template.cpp</a>
* :heavy_check_mark: <a href="../../../library/graph/tree/centroid-decomposition.cpp.html">Centroid-Decomosition(重心分解) <small>(graph/tree/centroid-decomposition.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://yukicoder.me/problems/no/1002"

#include "../../template/template.cpp"

#include "../../graph/graph-template.cpp"

#include "../../graph/tree/centroid-decomposition.cpp"

int main() {
  int N, K;
  cin >> N >> K;
  CentroidDecomposition< int > g(N);
  g.read(N - 1, -1, true);
  int root = g.build();
  int64 ret = 0;
  vector< int > used(N);

  map< pair< int, int >, int > mp;
  int all;
  map< int, int > mp2;
  map< int, int > mp3;


  auto get_vec = MFP([&](auto get_vec, int idx, int par, int a, int b) -> void {
    if(b == -1) {
      ret += all - mp2[a];
      ret += mp3[a];
    } else {
      ret++;
      ret += mp2[a] + mp2[b];
      ret += mp[minmax(a, b)];
    }
    for(auto &e : g.g[idx]) {
      if(e.to == par) continue;
      if(used[e.to]) continue;
      if(a == e.cost) {
        get_vec(e.to, idx, e.cost, b);
      } else if(b == -1 || b == e.cost) {
        get_vec(e.to, idx, a, e.cost);
      }
    }
  });

  auto add_vec = MFP([&](auto add_vec, int idx, int par, int a, int b) -> void {
    if(b == -1) {
      mp2[a]++;
      all++;
    } else {
      mp[minmax(a, b)]++;
      mp3[a]++;
      mp3[b]++;
    }
    for(auto &e : g.g[idx]) {
      if(e.to == par) continue;
      if(used[e.to]) continue;
      if(a == e.cost) {
        add_vec(e.to, idx, e.cost, b);
      } else if(b == -1 || b == e.cost) {
        add_vec(e.to, idx, a, e.cost);
      }
    }
  });

  auto rec = MFP([&](auto rec, int idx) -> void {
    used[idx] = true;
    mp.clear();
    mp2.clear();
    mp3.clear();
    all = 0;
    for(auto &e : g.g[idx]) {
      if(used[e.to]) continue;
      get_vec(e.to, idx, e.cost, -1);
      add_vec(e.to, idx, e.cost, -1);
    }
    for(auto &to : g.tree.g[idx]) {
      rec(to);
    }
    used[idx] = false;
  });
  rec(root);
  cout << ret << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-1002.test.cpp"
#define PROBLEM "https://yukicoder.me/problems/no/1002"

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
#line 4 "test/verify/yukicoder-1002.test.cpp"

#line 1 "graph/graph-template.cpp"
template< typename T = int >
struct Edge {
  int from, to;
  T cost;
  int idx;

  Edge() = default;

  Edge(int from, int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost), idx(idx) {}

  operator int() const { return to; }
};

template< typename T = int >
struct Graph {
  vector< vector< Edge< T > > > g;
  int es;

  Graph() = default;

  explicit Graph(int n) : g(n), es(0) {}

  size_t size() const {
    return g.size();
  }

  void add_directed_edge(int from, int to, T cost = 1) {
    g[from].emplace_back(from, to, cost, es++);
  }

  void add_edge(int from, int to, T cost = 1) {
    g[from].emplace_back(from, to, cost, es);
    g[to].emplace_back(to, from, cost, es++);
  }

  void read(int M, int padding = -1, bool weighted = false, bool directed = false) {
    for(int i = 0; i < M; i++) {
      int a, b;
      cin >> a >> b;
      a += padding;
      b += padding;
      T c = T(1);
      if(weighted) cin >> c;
      if(directed) add_directed_edge(a, b, c);
      else add_edge(a, b, c);
    }
  }
};
#line 6 "test/verify/yukicoder-1002.test.cpp"

#line 1 "graph/tree/centroid-decomposition.cpp"
/**
 * @brief Centroid-Decomosition(重心分解)
 */
template< typename T >
struct CentroidDecomposition : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  Graph< int > tree;

  int build(int t = 0) {
    sub.assign(g.size(), 0);
    v.assign(g.size(), 0);
    tree = Graph< T >(g.size());
    return build_dfs(0);
  }

  explicit CentroidDecomposition(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > sub;
  vector< int > v;

  inline int build_dfs(int idx, int par) {
    sub[idx] = 1;
    for(auto &to : g[idx]) {
      if(to == par || v[to]) continue;
      sub[idx] += build_dfs(to, idx);
    }
    return sub[idx];
  }

  inline int search_centroid(int idx, int par, const int mid) {
    for(auto &to : g[idx]) {
      if(to == par || v[to]) continue;
      if(sub[to] > mid) return search_centroid(to, idx, mid);
    }
    return idx;
  }

  inline int build_dfs(int idx) {
    int centroid = search_centroid(idx, -1, build_dfs(idx, -1) / 2);
    v[centroid] = true;
    for(auto &to : g[centroid]) {
      if(!v[to]) tree.add_directed_edge(centroid, build_dfs(to));
    }
    v[centroid] = false;
    return centroid;
  }
};
#line 8 "test/verify/yukicoder-1002.test.cpp"

int main() {
  int N, K;
  cin >> N >> K;
  CentroidDecomposition< int > g(N);
  g.read(N - 1, -1, true);
  int root = g.build();
  int64 ret = 0;
  vector< int > used(N);

  map< pair< int, int >, int > mp;
  int all;
  map< int, int > mp2;
  map< int, int > mp3;


  auto get_vec = MFP([&](auto get_vec, int idx, int par, int a, int b) -> void {
    if(b == -1) {
      ret += all - mp2[a];
      ret += mp3[a];
    } else {
      ret++;
      ret += mp2[a] + mp2[b];
      ret += mp[minmax(a, b)];
    }
    for(auto &e : g.g[idx]) {
      if(e.to == par) continue;
      if(used[e.to]) continue;
      if(a == e.cost) {
        get_vec(e.to, idx, e.cost, b);
      } else if(b == -1 || b == e.cost) {
        get_vec(e.to, idx, a, e.cost);
      }
    }
  });

  auto add_vec = MFP([&](auto add_vec, int idx, int par, int a, int b) -> void {
    if(b == -1) {
      mp2[a]++;
      all++;
    } else {
      mp[minmax(a, b)]++;
      mp3[a]++;
      mp3[b]++;
    }
    for(auto &e : g.g[idx]) {
      if(e.to == par) continue;
      if(used[e.to]) continue;
      if(a == e.cost) {
        add_vec(e.to, idx, e.cost, b);
      } else if(b == -1 || b == e.cost) {
        add_vec(e.to, idx, a, e.cost);
      }
    }
  });

  auto rec = MFP([&](auto rec, int idx) -> void {
    used[idx] = true;
    mp.clear();
    mp2.clear();
    mp3.clear();
    all = 0;
    for(auto &e : g.g[idx]) {
      if(used[e.to]) continue;
      get_vec(e.to, idx, e.cost, -1);
      add_vec(e.to, idx, e.cost, -1);
    }
    for(auto &to : g.tree.g[idx]) {
      rec(to);
    }
    used[idx] = false;
  });
  rec(root);
  cout << ret << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

