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


# :heavy_check_mark: Doubling-Lowest-Common-Ancestor(最小共通祖先) <small>(graph/tree/doubling-lowest-common-ancestor.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/doubling-lowest-common-ancestor.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-26 01:02:16+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-5-c.test.cpp.html">test/verify/aoj-grl-5-c.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Doubling-Lowest-Common-Ancestor(最小共通祖先)
 */
template< typename T >
struct DoublingLowestCommonAncestor : Graph< T > {
public:
  using Graph< T >::g;
  vector< int > dep;
  vector< T > sum;
  vector< vector< int > > table;
  const int LOG;

  explicit DoublingLowestCommonAncestor(int n)
      : LOG(32 - __builtin_clz(g.size())), Graph< T >(n) {}

  explicit DoublingLowestCommonAncestor(const Graph< T > &g)
      : LOG(32 - __builtin_clz(g.size())), Graph< T >(g) {}

  void build() {
    dep.assign(g.size(), 0);
    sum.assign(g.size(), 0);
    table.assign(LOG, vector< int >(g.size(), -1));
    dfs(0, -1, 0);
    for(int k = 0; k + 1 < LOG; k++) {
      for(int i = 0; i < table[k].size(); i++) {
        if(table[k][i] == -1) table[k + 1][i] = -1;
        else table[k + 1][i] = table[k][table[k][i]];
      }
    }
  }

  int lca(int u, int v) {
    if(dep[u] > dep[v]) swap(u, v);
    for(int i = LOG - 1; i >= 0; i--) {
      if(((dep[v] - dep[u]) >> i) & 1) v = table[i][v];
    }
    if(u == v) return u;
    for(int i = LOG - 1; i >= 0; i--) {
      if(table[i][u] != table[i][v]) {
        u = table[i][u];
        v = table[i][v];
      }
    }
    return table[0][u];
  }

  T dist(int u, int v) {
    return sum[u] + sum[v] - 2 * sum[lca(u, v)];
  }

private:
  void dfs(int idx, int par, int d) {
    table[0][idx] = par;
    dep[idx] = d;
    for(auto &to : g[idx]) {
      if(to != par) {
        sum[to] = sum[idx] + to.cost;
        dfs(to, idx, d + 1);
      }
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/tree/doubling-lowest-common-ancestor.cpp"
/**
 * @brief Doubling-Lowest-Common-Ancestor(最小共通祖先)
 */
template< typename T >
struct DoublingLowestCommonAncestor : Graph< T > {
public:
  using Graph< T >::g;
  vector< int > dep;
  vector< T > sum;
  vector< vector< int > > table;
  const int LOG;

  explicit DoublingLowestCommonAncestor(int n)
      : LOG(32 - __builtin_clz(g.size())), Graph< T >(n) {}

  explicit DoublingLowestCommonAncestor(const Graph< T > &g)
      : LOG(32 - __builtin_clz(g.size())), Graph< T >(g) {}

  void build() {
    dep.assign(g.size(), 0);
    sum.assign(g.size(), 0);
    table.assign(LOG, vector< int >(g.size(), -1));
    dfs(0, -1, 0);
    for(int k = 0; k + 1 < LOG; k++) {
      for(int i = 0; i < table[k].size(); i++) {
        if(table[k][i] == -1) table[k + 1][i] = -1;
        else table[k + 1][i] = table[k][table[k][i]];
      }
    }
  }

  int lca(int u, int v) {
    if(dep[u] > dep[v]) swap(u, v);
    for(int i = LOG - 1; i >= 0; i--) {
      if(((dep[v] - dep[u]) >> i) & 1) v = table[i][v];
    }
    if(u == v) return u;
    for(int i = LOG - 1; i >= 0; i--) {
      if(table[i][u] != table[i][v]) {
        u = table[i][u];
        v = table[i][v];
      }
    }
    return table[0][u];
  }

  T dist(int u, int v) {
    return sum[u] + sum[v] - 2 * sum[lca(u, v)];
  }

private:
  void dfs(int idx, int par, int d) {
    table[0][idx] = par;
    dep[idx] = d;
    for(auto &to : g[idx]) {
      if(to != par) {
        sum[to] = sum[idx] + to.cost;
        dfs(to, idx, d + 1);
      }
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

