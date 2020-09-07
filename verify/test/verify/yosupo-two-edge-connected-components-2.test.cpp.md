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


# :heavy_check_mark: test/verify/yosupo-two-edge-connected-components-2.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-two-edge-connected-components-2.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-15 01:29:43+09:00


* see: <a href="https://judge.yosupo.jp/problem/two_edge_connected_components">https://judge.yosupo.jp/problem/two_edge_connected_components</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/connected-components/incremental-bridge-connectivity.cpp.html">Incremental-Bridge-Connectivity <small>(graph/connected-components/incremental-bridge-connectivity.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/union-find/union-find.cpp.html">Union-Find <small>(structure/union-find/union-find.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/two_edge_connected_components"

#include "../../template/template.cpp"

#include "../../structure/union-find/union-find.cpp"

#include "../../graph/connected-components/incremental-bridge-connectivity.cpp"

int main() {
  int n, m;
  cin >> n >> m;
  IncrementalBridgeConnectivity ibc(n);
  for(int i = 0; i < m; i++) {
    int a, b;
    cin >> a >> b;
    ibc.add_edge(a, b);
  }
  vector< int > id(n, -1);
  int k = 0;
  vector< vector< int > > ans(n);
  for(int i = 0; i < n; i++) {
    int r = ibc.find(i);
    if(id[r] == -1) {
      id[r] = k;
      k += 1;
    }
    ans[id[r]].push_back(i);
  }
  cout << k << "\n";
  for(int i = 0; i < k; i++) {
    cout << ans[i].size() << " " << ans[i] << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-two-edge-connected-components-2.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/two_edge_connected_components"

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
#line 4 "test/verify/yosupo-two-edge-connected-components-2.test.cpp"

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
#line 6 "test/verify/yosupo-two-edge-connected-components-2.test.cpp"

#line 1 "graph/connected-components/incremental-bridge-connectivity.cpp"
/**
 * @brief Incremental-Bridge-Connectivity
 * @docs docs/incremental-bridge-connectivity.md
 * @see https://scrapbox.io/data-structures/Incremental_Bridge-Connectivity
 */
struct IncrementalBridgeConnectivity {
private:
  UnionFind cc, bcc;
  vector< int > bbf;
  size_t bridge;

  int size() {
    return bbf.size();
  }

  int par(int x) {
    return bbf[x] == size() ? size() : bcc.find(bbf[x]);
  }

  int lca(int x, int y) {
    unordered_set< int > used;
    for(;;) {
      if(x != size()) {
        if(!used.insert(x).second) return x;
        x = par(x);
      }
      swap(x, y);
    }
  }

  void compress(int x, int y) {
    while(bcc.find(x) != bcc.find(y)) {
      int nxt = par(x);
      bbf[x] = bbf[y];
      bcc.unite(x, y);
      x = nxt;
      --bridge;
    }
  }

  void link(int x, int y) {
    int v = x, pre = y;
    while(v != size()) {
      int nxt = par(v);
      bbf[v] = pre;
      pre = v;
      v = nxt;
    }
  }

public:
  IncrementalBridgeConnectivity() = default;

  explicit IncrementalBridgeConnectivity(int sz) : cc(sz), bcc(sz), bbf(sz, sz), bridge(0) {}

  int find(int k) {
    return bcc.find(k);
  }

  size_t bridge_size() const {
    return bridge;
  }

  void add_edge(int x, int y) {
    x = bcc.find(x);
    y = bcc.find(y);
    if(cc.find(x) == cc.find(y)) {
      int w = lca(x, y);
      compress(x, w);
      compress(y, w);
    } else {
      if(cc.size(x) > cc.size(y)) swap(x, y);
      link(x, y);
      cc.unite(x, y);
      ++bridge;
    }
  }
};
#line 8 "test/verify/yosupo-two-edge-connected-components-2.test.cpp"

int main() {
  int n, m;
  cin >> n >> m;
  IncrementalBridgeConnectivity ibc(n);
  for(int i = 0; i < m; i++) {
    int a, b;
    cin >> a >> b;
    ibc.add_edge(a, b);
  }
  vector< int > id(n, -1);
  int k = 0;
  vector< vector< int > > ans(n);
  for(int i = 0; i < n; i++) {
    int r = ibc.find(i);
    if(id[r] == -1) {
      id[r] = k;
      k += 1;
    }
    ans[id[r]].push_back(i);
  }
  cout << k << "\n";
  for(int i = 0; i < k; i++) {
    cout << ans[i].size() << " " << ans[i] << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

