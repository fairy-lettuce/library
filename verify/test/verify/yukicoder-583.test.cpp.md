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


# :heavy_check_mark: test/verify/yukicoder-583.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-583.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-26 02:14:53+09:00


* see: <a href="https://yukicoder.me/problems/no/583">https://yukicoder.me/problems/no/583</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/others/eulerian-trail.cpp.html">Eulerian-Trail(オイラー路) <small>(graph/others/eulerian-trail.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/union-find/union-find.cpp.html">Union-Find <small>(structure/union-find/union-find.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://yukicoder.me/problems/no/583"

#include "../../template/template.cpp"

#include "../../structure/union-find/union-find.cpp"

#include "../../graph/others/eulerian-trail.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  vector< int > A(M), B(M);
  EulerianTrail< false > et(N);
  for(int i = 0; i < M; i++) {
    cin >> A[i] >> B[i];
    et.add_edge(A[i], B[i]);
  }
  if(et.enumerate_semi_eulerian_trail().size() == 1) cout << "YES\n";
  else cout << "NO\n";
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-583.test.cpp"
#define PROBLEM "https://yukicoder.me/problems/no/583"

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
#line 4 "test/verify/yukicoder-583.test.cpp"

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
#line 6 "test/verify/yukicoder-583.test.cpp"

#line 1 "graph/others/eulerian-trail.cpp"
/**
 * @brief Eulerian-Trail(オイラー路)
 */
template< bool directed >
struct EulerianTrail {
  vector< vector< pair< int, int > > > g;
  vector< pair< int, int > > es;
  int M;
  vector< int > used_vertex, used_edge, deg;

  explicit EulerianTrail(int V) : g(V), M(0), deg(V), used_vertex(V) {}

  void add_edge(int a, int b) {
    es.emplace_back(a, b);
    g[a].emplace_back(b, M);
    if(directed) {
      deg[a]++;
      deg[b]--;
    } else {
      g[b].emplace_back(a, M);
      deg[a]++;
      deg[b]++;
    }
    M++;
  }

  pair< int, int > get_edge(int idx) const {
    return es[idx];
  }

  vector< vector< int > > enumerate_eulerian_trail() {
    if(directed) {
      for(auto &p : deg) if(p != 0) return {};
    } else {
      for(auto &p : deg) if(p & 1) return {};
    }
    used_edge.assign(M, 0);
    vector< vector< int > > ret;
    for(int i = 0; i < (int) g.size(); i++) {
      if(g[i].empty() || used_vertex[i]) continue;
      ret.emplace_back(go(i));
    }
    return ret;
  }

  vector< vector< int > > enumerate_semi_eulerian_trail() {
    UnionFind uf(g.size());
    for(auto &p : es) uf.unite(p.first, p.second);
    vector< vector< int > > group(g.size());
    for(int i = 0; i < (int) g.size(); i++) group[uf.find(i)].emplace_back(i);
    vector< vector< int > > ret;
    used_edge.assign(M, 0);
    for(auto &vs : group) {
      if(vs.empty()) continue;
      int latte = -1, malta = -1;
      if(directed) {
        for(auto &p : vs) {
          if(abs(deg[p]) > 1) {
            return {};
          } else if(deg[p] == 1) {
            if(latte >= 0) return {};
            latte = p;
          }
        }
      } else {
        for(auto &p : vs) {
          if(deg[p] & 1) {
            if(latte == -1) latte = p;
            else if(malta == -1) malta = p;
            else return {};
          }
        }
      }
      ret.emplace_back(go(latte == -1 ? vs.front() : latte));
      if(ret.back().empty()) ret.pop_back();
    }
    return ret;
  }

  vector< int > go(int s) {
    stack< pair< int, int > > st;
    vector< int > ord;
    st.emplace(s, -1);
    while(!st.empty()) {
      int idx = st.top().first;
      used_vertex[idx] = true;
      if(g[idx].empty()) {
        ord.emplace_back(st.top().second);
        st.pop();
      } else {
        auto e = g[idx].back();
        g[idx].pop_back();
        if(used_edge[e.second]) continue;
        used_edge[e.second] = true;
        st.emplace(e);
      }
    }
    ord.pop_back();
    reverse(ord.begin(), ord.end());
    return ord;
  }
};
#line 8 "test/verify/yukicoder-583.test.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  vector< int > A(M), B(M);
  EulerianTrail< false > et(N);
  for(int i = 0; i < M; i++) {
    cin >> A[i] >> B[i];
    et.add_edge(A[i], B[i]);
  }
  if(et.enumerate_semi_eulerian_trail().size() == 1) cout << "YES\n";
  else cout << "NO\n";
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

