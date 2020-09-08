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


# :heavy_check_mark: Eulerian-Trail(オイラー路) <small>(graph/others/eulerian-trail.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/eulerian-trail.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-08 21:03:17+09:00




## 概要

有向/無向グラフが与えられたときに, グラフの全ての辺をちょうど $1$ 回ずつ通る閉路やパスを各連結成分について求める.

連結なグラフでオイラー閉路が存在する必要十分条件は, 有向グラフでは全ての頂点について入次数と出次数が等しいこと, 無向グラフでは全ての頂点の次数が偶数であることである.

連結なグラフでオイラー路が存在する必要十分条件は, オイラー閉路の条件にマッチするかどうかに加えて, 有向グラフでは入次数と出次数の差が $1$ である頂点が $2$ 個, 無向グラフでは次数が奇数の頂点が $2$ 個であることである.

## 使い方

* `add_edge(a, b)`: 頂点 `a`, `b` 間に辺をはる.
* `enumerate_eulerian_trail()`: すべての連結成分についてオイラー路を列挙し, オイラー路の辺の idx の列を結合したものを返す. オイラー路が存在しない連結成分があるとき空列を返す.
* `enumerate_semi_eulerian_trail()`: すべての連結成分について準オイラー路を列挙し, 準オイラー路の辺の idx の列を結合したものを返す. 準オイラー路が存在しない連結成分があるとき空列を返す.
* `get_edge(idx)`: `idx` 番目に追加した辺の ${from, to}$ を返す.

## 計算量

$O(V + E)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-bipartite-edge-coloring.test.cpp.html">test/verify/yosupo-bipartite-edge-coloring.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yukicoder-583.test.cpp.html">test/verify/yukicoder-583.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Eulerian-Trail(オイラー路)
 * @docs docs/eulerian-trail.md
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/eulerian-trail.cpp"
/**
 * @brief Eulerian-Trail(オイラー路)
 * @docs docs/eulerian-trail.md
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

