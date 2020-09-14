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


# :x: Three-Edge-Connected-Components(三重辺連結成分分解) <small>(graph/connected-components/three-edge-connected-components.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#3a7c46e10de1b2cce1293b2074b86f0a">graph/connected-components</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/connected-components/three-edge-connected-components.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-15 01:29:43+09:00




## Verified with

* :x: <a href="../../../verify/test/verify/yosupo-three-edge-connected-components.test.cpp.html">test/verify/yosupo-three-edge-connected-components.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Three-Edge-Connected-Components(三重辺連結成分分解)
 */
template< typename T = int >
struct ThreeEdgeConnectedComponents : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< vector< int > > group;

  void build() {
    uf = UnionFind(g.size());
    bcc = IncrementalBridgeConnectivity(g.size());
    used.assign(g.size(), 0);
    in.assign(g.size(), 0);
    out.assign(g.size(), 0);
    deg.assign(g.size(), 0);
    low.assign(g.size(), g.size());
    for(int from = 0; from < g.size(); from++) {
      for(auto &to : g[from]) {
        if(from < to) bcc.add_edge(from, to);
      }
    }
    int cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(used[i]) continue;
      vector< int > tmp;
      dfs(i, -1, tmp, cnt);
      cnt++;
    }
    vector< int > id(g.size(), -1);
    cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(id[uf.find(i)] == -1) id[uf.find(i)] = cnt++;
    }
    group.resize(cnt);
    for(int i = 0; i < g.size(); i++) {
      group[id[uf.find(i)]].emplace_back(i);
    }
  }

  int operator[](const int &k) {
    return uf.find(k);
  }

private:
  vector< int > used;
  vector< int > in, out, low, deg;
  IncrementalBridgeConnectivity bcc;
  UnionFind uf;

  void absorb(vector< int > &path, int v, int w = -1) {
    while(!path.empty()) {
      int x = path.back();
      if(w != -1 && (in[x] > in[w] or in[w] >= out[x])) break;
      path.pop_back();
      uf.unite(v, x);
      deg[v] += deg[x] - 2;
    }
  }

  void dfs(int idx, int p, vector< int > &path, int &k) {
    used[idx] = 1;
    in[idx] = low[idx] = k++;
    for(auto &to : g[idx]) {
      if(idx == to || bcc.find(idx) != bcc.find(to)) continue;
      deg[idx]++;
      if(to == p) {
        p = -1;
        continue;
      }
      if(used[to]) {
        if(in[idx] > in[to]) {
          if(in[to] < low[idx]) {
            low[idx] = in[to];
            absorb(path, idx);
          }
        } else {
          deg[idx] -= 2;
          absorb(path, idx, to);
        }
      } else {
        vector< int > ps;
        dfs(to, idx, ps, k);
        if(deg[to] == 2) ps.pop_back();
        if(low[to] < low[idx]) {
          low[idx] = low[to];
          absorb(path, idx);
          path = ps;
        } else {
          absorb(ps, idx);
        }
      }
    }
    out[idx] = k;
    path.push_back(idx);
  }
};


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/connected-components/three-edge-connected-components.cpp"
/**
 * @brief Three-Edge-Connected-Components(三重辺連結成分分解)
 */
template< typename T = int >
struct ThreeEdgeConnectedComponents : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< vector< int > > group;

  void build() {
    uf = UnionFind(g.size());
    bcc = IncrementalBridgeConnectivity(g.size());
    used.assign(g.size(), 0);
    in.assign(g.size(), 0);
    out.assign(g.size(), 0);
    deg.assign(g.size(), 0);
    low.assign(g.size(), g.size());
    for(int from = 0; from < g.size(); from++) {
      for(auto &to : g[from]) {
        if(from < to) bcc.add_edge(from, to);
      }
    }
    int cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(used[i]) continue;
      vector< int > tmp;
      dfs(i, -1, tmp, cnt);
      cnt++;
    }
    vector< int > id(g.size(), -1);
    cnt = 0;
    for(int i = 0; i < g.size(); i++) {
      if(id[uf.find(i)] == -1) id[uf.find(i)] = cnt++;
    }
    group.resize(cnt);
    for(int i = 0; i < g.size(); i++) {
      group[id[uf.find(i)]].emplace_back(i);
    }
  }

  int operator[](const int &k) {
    return uf.find(k);
  }

private:
  vector< int > used;
  vector< int > in, out, low, deg;
  IncrementalBridgeConnectivity bcc;
  UnionFind uf;

  void absorb(vector< int > &path, int v, int w = -1) {
    while(!path.empty()) {
      int x = path.back();
      if(w != -1 && (in[x] > in[w] or in[w] >= out[x])) break;
      path.pop_back();
      uf.unite(v, x);
      deg[v] += deg[x] - 2;
    }
  }

  void dfs(int idx, int p, vector< int > &path, int &k) {
    used[idx] = 1;
    in[idx] = low[idx] = k++;
    for(auto &to : g[idx]) {
      if(idx == to || bcc.find(idx) != bcc.find(to)) continue;
      deg[idx]++;
      if(to == p) {
        p = -1;
        continue;
      }
      if(used[to]) {
        if(in[idx] > in[to]) {
          if(in[to] < low[idx]) {
            low[idx] = in[to];
            absorb(path, idx);
          }
        } else {
          deg[idx] -= 2;
          absorb(path, idx, to);
        }
      } else {
        vector< int > ps;
        dfs(to, idx, ps, k);
        if(deg[to] == 2) ps.pop_back();
        if(low[to] < low[idx]) {
          low[idx] = low[to];
          absorb(path, idx);
          path = ps;
        } else {
          absorb(ps, idx);
        }
      }
    }
    out[idx] = k;
    path.push_back(idx);
  }
};


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

