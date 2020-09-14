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


# :question: Dominator-Tree <small>(graph/others/dominator-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#e557c7f962c39680942b9dada22cabec">graph/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/others/dominator-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-30 01:47:11+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-0294.test.cpp.html">test/verify/aoj-0294.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-dominatortree.test.cpp.html">test/verify/yosupo-dominatortree.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Dominator-Tree
 */
template< typename T = int >
struct DominatorTree : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;

  void build(int root) {
    rg = Graph< T >(g.size());
    par.assign(g.size(), 0);
    idom.assign(g.size(), -1);
    semi.assign(g.size(), -1);
    ord.reserve(g.size());
    UnionFind uf(semi);

    const int N = (int) g.size();
    dfs(root);
    for(int i = 0; i < N; i++) {
      for(auto &to : g[i]) {
        if(~semi[i]) rg.add_directed_edge(to, i);
      }
    }

    vector< vector< int > > bucket(N);
    vector< int > U(N);
    for(int i = (int) ord.size() - 1; i >= 0; i--) {
      int x = ord[i];
      for(int v : rg.g[x]) {
        v = uf.eval(v);
        if(semi[x] > semi[v]) semi[x] = semi[v];
      }
      bucket[ord[semi[x]]].emplace_back(x);
      for(int v : bucket[par[x]]) U[v] = uf.eval(v);
      bucket[par[x]].clear();
      uf.link(par[x], x);
    }
    for(int i = 1; i < ord.size(); i++) {
      int x = ord[i], u = U[x];
      idom[x] = semi[x] == semi[u] ? semi[x] : idom[u];
    }
    for(int i = 1; i < ord.size(); i++) {
      int x = ord[i];
      idom[x] = ord[idom[x]];
    }
    idom[root] = root;
  }

  int operator[](const int &k) const {
    return idom[k];
  }

private:
  Graph< T > rg;

  struct UnionFind {
    const vector< int > &semi;
    vector< int > par, m;

    explicit UnionFind(const vector< int > &semi) : semi(semi), par(semi.size()), m(semi.size()) {
      iota(begin(par), end(par), 0);
      iota(begin(m), end(m), 0);
    }

    int find(int v) {
      if(par[v] == v) return v;
      int r = find(par[v]);
      if(semi[m[v]] > semi[m[par[v]]]) m[v] = m[par[v]];
      return par[v] = r;
    }

    int eval(int v) {
      find(v);
      return m[v];
    }

    void link(int p, int c) {
      par[c] = p;
    }
  };

  vector< int > ord, par;
  vector< int > idom, semi;

  void dfs(int idx) {
    semi[idx] = (int) ord.size();
    ord.emplace_back(idx);
    for(auto &to : g[idx]) {
      if(~semi[to]) continue;
      dfs(to);
      par[to] = idx;
    }
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/others/dominator-tree.cpp"
/**
 * @brief Dominator-Tree
 */
template< typename T = int >
struct DominatorTree : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;

  void build(int root) {
    rg = Graph< T >(g.size());
    par.assign(g.size(), 0);
    idom.assign(g.size(), -1);
    semi.assign(g.size(), -1);
    ord.reserve(g.size());
    UnionFind uf(semi);

    const int N = (int) g.size();
    dfs(root);
    for(int i = 0; i < N; i++) {
      for(auto &to : g[i]) {
        if(~semi[i]) rg.add_directed_edge(to, i);
      }
    }

    vector< vector< int > > bucket(N);
    vector< int > U(N);
    for(int i = (int) ord.size() - 1; i >= 0; i--) {
      int x = ord[i];
      for(int v : rg.g[x]) {
        v = uf.eval(v);
        if(semi[x] > semi[v]) semi[x] = semi[v];
      }
      bucket[ord[semi[x]]].emplace_back(x);
      for(int v : bucket[par[x]]) U[v] = uf.eval(v);
      bucket[par[x]].clear();
      uf.link(par[x], x);
    }
    for(int i = 1; i < ord.size(); i++) {
      int x = ord[i], u = U[x];
      idom[x] = semi[x] == semi[u] ? semi[x] : idom[u];
    }
    for(int i = 1; i < ord.size(); i++) {
      int x = ord[i];
      idom[x] = ord[idom[x]];
    }
    idom[root] = root;
  }

  int operator[](const int &k) const {
    return idom[k];
  }

private:
  Graph< T > rg;

  struct UnionFind {
    const vector< int > &semi;
    vector< int > par, m;

    explicit UnionFind(const vector< int > &semi) : semi(semi), par(semi.size()), m(semi.size()) {
      iota(begin(par), end(par), 0);
      iota(begin(m), end(m), 0);
    }

    int find(int v) {
      if(par[v] == v) return v;
      int r = find(par[v]);
      if(semi[m[v]] > semi[m[par[v]]]) m[v] = m[par[v]];
      return par[v] = r;
    }

    int eval(int v) {
      find(v);
      return m[v];
    }

    void link(int p, int c) {
      par[c] = p;
    }
  };

  vector< int > ord, par;
  vector< int > idom, semi;

  void dfs(int idx) {
    semi[idx] = (int) ord.size();
    ord.emplace_back(idx);
    for(auto &to : g[idx]) {
      if(~semi[to]) continue;
      dfs(to);
      par[to] = idx;
    }
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

