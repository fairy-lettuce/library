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


# :heavy_check_mark: Heavy-Light-Decomposition(HL分解) <small>(graph/tree/heavy-light-decomposition.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/heavy-light-decomposition.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-03 16:48:02+09:00


* see: <a href="https://smijake3.hatenablog.com/entry/2019/09/15/200200">https://smijake3.hatenablog.com/entry/2019/09/15/200200</a>


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2450.test.cpp.html">test/verify/aoj-2450.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2667.test.cpp.html">test/verify/aoj-2667.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-5-c-2.test.cpp.html">test/verify/aoj-grl-5-c-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Heavy-Light-Decomposition(HL分解)
 * @see https://smijake3.hatenablog.com/entry/2019/09/15/200200
 */
template< typename G >
struct HeavyLightDecomposition {
  G &g;
  vector< int > sz, in, out, head, rev, par, dep;

  explicit HeavyLightDecomposition(G &g) :
      g(g), sz(g.size()), in(g.size()), out(g.size()), head(g.size()), rev(g.size()), par(g.size()), dep(g.size()) {}

  void dfs_sz(int idx, int p, int d) {
    dep[idx] = d;
    par[idx] = p;
    sz[idx] = 1;
    if(g[idx].size() && g[idx][0] == p) swap(g[idx][0], g[idx].back());
    for(auto &to : g[idx]) {
      if(to == p) continue;
      dfs_sz(to, idx, d + 1);
      sz[idx] += sz[to];
      if(sz[g[idx][0]] < sz[to]) swap(g[idx][0], to);
    }
  }

  void dfs_hld(int idx, int p, int &times) {
    in[idx] = times++;
    rev[in[idx]] = idx;
    for(auto &to : g[idx]) {
      if(to == p) continue;
      head[to] = (g[idx][0] == to ? head[idx] : to);
      dfs_hld(to, idx, times);
    }
    out[idx] = times;
  }

  void build() {
    dfs_sz(0, -1, 0);
    int t = 0;
    dfs_hld(0, -1, t);
  }

  /* k: 0-indexed */
  int la(int v, int k) {
    while(1) {
      int u = head[v];
      if(in[v] - k >= in[u]) return rev[in[v] - k];
      k -= in[v] - in[u] + 1;
      v = par[u];
    }
  }

  int lca(int u, int v) const {
    for(;; v = par[head[v]]) {
      if(in[u] > in[v]) swap(u, v);
      if(head[u] == head[v]) return u;
    }
  }

  int dist(int u, int v) const {
    return dep[u] + dep[v] - 2 * dep[lca(u, v)];
  }

  template< typename T, typename Q, typename F, typename S >
  T query(int u, int v, const T &ti, const Q &q, const F &f, const S &s, bool edge = false) {
    T l = ti, r = ti;
    for(;; v = par[head[v]]) {
      if(in[u] > in[v]) swap(u, v), swap(l, r);
      if(head[u] == head[v]) break;
      l = f(q(in[head[v]], in[v] + 1), l);
    }
    return s(f(q(in[u] + edge, in[v] + 1), l), r);
  }

  template< typename T, typename Q, typename F >
  T query(int u, int v, const T &ti, const Q &q, const F &f, bool edge = false) {
    return query(u, v, ti, q, f, f, edge);
  }

  template< typename Q >
  void add(int u, int v, const Q &q, bool edge = false) {
    for(;; v = par[head[v]]) {
      if(in[u] > in[v]) swap(u, v);
      if(head[u] == head[v]) break;
      q(in[head[v]], in[v] + 1);
    }
    q(in[u] + edge, in[v] + 1);
  }

  /* {parent, child} */
  vector< pair< int, int > > compress(vector< int > &remark) {
    auto cmp = [&](int a, int b) { return in[a] < in[b]; };
    sort(begin(remark), end(remark), cmp);
    remark.erase(unique(begin(remark), end(remark)), end(remark));
    int K = (int) remark.size();
    for(int k = 1; k < K; k++) remark.emplace_back(lca(remark[k - 1], remark[k]));
    sort(begin(remark), end(remark), cmp);
    remark.erase(unique(begin(remark), end(remark)), end(remark));
    vector< pair< int, int > > es;
    stack< int > st;
    for(auto &k : remark) {
      while(!st.empty() && out[st.top()] <= in[k]) st.pop();
      if(!st.empty()) es.emplace_back(st.top(), k);
      st.emplace(k);
    }
    return es;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/tree/heavy-light-decomposition.cpp"
/**
 * @brief Heavy-Light-Decomposition(HL分解)
 * @see https://smijake3.hatenablog.com/entry/2019/09/15/200200
 */
template< typename G >
struct HeavyLightDecomposition {
  G &g;
  vector< int > sz, in, out, head, rev, par, dep;

  explicit HeavyLightDecomposition(G &g) :
      g(g), sz(g.size()), in(g.size()), out(g.size()), head(g.size()), rev(g.size()), par(g.size()), dep(g.size()) {}

  void dfs_sz(int idx, int p, int d) {
    dep[idx] = d;
    par[idx] = p;
    sz[idx] = 1;
    if(g[idx].size() && g[idx][0] == p) swap(g[idx][0], g[idx].back());
    for(auto &to : g[idx]) {
      if(to == p) continue;
      dfs_sz(to, idx, d + 1);
      sz[idx] += sz[to];
      if(sz[g[idx][0]] < sz[to]) swap(g[idx][0], to);
    }
  }

  void dfs_hld(int idx, int p, int &times) {
    in[idx] = times++;
    rev[in[idx]] = idx;
    for(auto &to : g[idx]) {
      if(to == p) continue;
      head[to] = (g[idx][0] == to ? head[idx] : to);
      dfs_hld(to, idx, times);
    }
    out[idx] = times;
  }

  void build() {
    dfs_sz(0, -1, 0);
    int t = 0;
    dfs_hld(0, -1, t);
  }

  /* k: 0-indexed */
  int la(int v, int k) {
    while(1) {
      int u = head[v];
      if(in[v] - k >= in[u]) return rev[in[v] - k];
      k -= in[v] - in[u] + 1;
      v = par[u];
    }
  }

  int lca(int u, int v) const {
    for(;; v = par[head[v]]) {
      if(in[u] > in[v]) swap(u, v);
      if(head[u] == head[v]) return u;
    }
  }

  int dist(int u, int v) const {
    return dep[u] + dep[v] - 2 * dep[lca(u, v)];
  }

  template< typename T, typename Q, typename F, typename S >
  T query(int u, int v, const T &ti, const Q &q, const F &f, const S &s, bool edge = false) {
    T l = ti, r = ti;
    for(;; v = par[head[v]]) {
      if(in[u] > in[v]) swap(u, v), swap(l, r);
      if(head[u] == head[v]) break;
      l = f(q(in[head[v]], in[v] + 1), l);
    }
    return s(f(q(in[u] + edge, in[v] + 1), l), r);
  }

  template< typename T, typename Q, typename F >
  T query(int u, int v, const T &ti, const Q &q, const F &f, bool edge = false) {
    return query(u, v, ti, q, f, f, edge);
  }

  template< typename Q >
  void add(int u, int v, const Q &q, bool edge = false) {
    for(;; v = par[head[v]]) {
      if(in[u] > in[v]) swap(u, v);
      if(head[u] == head[v]) break;
      q(in[head[v]], in[v] + 1);
    }
    q(in[u] + edge, in[v] + 1);
  }

  /* {parent, child} */
  vector< pair< int, int > > compress(vector< int > &remark) {
    auto cmp = [&](int a, int b) { return in[a] < in[b]; };
    sort(begin(remark), end(remark), cmp);
    remark.erase(unique(begin(remark), end(remark)), end(remark));
    int K = (int) remark.size();
    for(int k = 1; k < K; k++) remark.emplace_back(lca(remark[k - 1], remark[k]));
    sort(begin(remark), end(remark), cmp);
    remark.erase(unique(begin(remark), end(remark)), end(remark));
    vector< pair< int, int > > es;
    stack< int > st;
    for(auto &k : remark) {
      while(!st.empty() && out[st.top()] <= in[k]) st.pop();
      if(!st.empty()) es.emplace_back(st.top(), k);
      st.emplace(k);
    }
    return es;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

