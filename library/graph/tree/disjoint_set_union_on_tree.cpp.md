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


# :warning: Disjoint-Set-Union-On-Tree <small>(graph/tree/disjoint_set_union_on_tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/disjoint_set_union_on_tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-08 23:29:00+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Disjoint-Set-Union-On-Tree
 */
template< typename T >
struct DisjointSetUnionOnTree : Graph< T > {
  using F = function< void(int) >;
  using Graph< T >::g;
  vector< int > heavy, sz, in, out, ord;
  const F expand, shrink, query;
 
  explicit DisjointSetUnionOnTree(int n, F expand, F shrink, F query)
      : Graph< T >(n), expand(move(expand)), shrink(move(shrink)), query(move(query)) {}
 
private:
  queue< int > que;
 
  int build_subtree(int idx) {
    in[idx] = ord.size();
    ord.emplace_back(idx);
    for(auto &to : g[idx]) {
      int sub = build_subtree(to);
      sz[idx] += sub;
      if(heavy[idx] == -1 || sz[heavy[idx]] < sub) {
        heavy[idx] = to;
      }
    }
    out[idx] = ord.size();
    return sz[idx];
  }
 
  void dfs(int idx, bool keep) {
    for(auto &to : g[idx]) {
      if(heavy[idx] == to) continue;
      dfs(to, false);
    }
    if(heavy[idx] != -1) {
      dfs(heavy[idx], true);
    }
    for(auto &to : g[idx]) {
      if(heavy[idx] == to) continue;
      for(int p = in[to]; p < out[to]; p++) {
        expand(ord[p]);
      }
    }
    expand(idx);
    query(idx);
    if(!keep) {
      for(int p = in[idx]; p < out[idx]; p++) shrink(ord[p]);
    }
  }
 
public:
  void build(int root = 0) {
    g = convert_rooted_tree(*this, root).g;
    sz.assign(g.size(), 1);
    heavy.assign(g.size(), -1);
    in.resize(g.size());
    out.resize(g.size());
    build_subtree(root);
    dfs(root, false);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/tree/disjoint_set_union_on_tree.cpp"
/**
 * @brief Disjoint-Set-Union-On-Tree
 */
template< typename T >
struct DisjointSetUnionOnTree : Graph< T > {
  using F = function< void(int) >;
  using Graph< T >::g;
  vector< int > heavy, sz, in, out, ord;
  const F expand, shrink, query;
 
  explicit DisjointSetUnionOnTree(int n, F expand, F shrink, F query)
      : Graph< T >(n), expand(move(expand)), shrink(move(shrink)), query(move(query)) {}
 
private:
  queue< int > que;
 
  int build_subtree(int idx) {
    in[idx] = ord.size();
    ord.emplace_back(idx);
    for(auto &to : g[idx]) {
      int sub = build_subtree(to);
      sz[idx] += sub;
      if(heavy[idx] == -1 || sz[heavy[idx]] < sub) {
        heavy[idx] = to;
      }
    }
    out[idx] = ord.size();
    return sz[idx];
  }
 
  void dfs(int idx, bool keep) {
    for(auto &to : g[idx]) {
      if(heavy[idx] == to) continue;
      dfs(to, false);
    }
    if(heavy[idx] != -1) {
      dfs(heavy[idx], true);
    }
    for(auto &to : g[idx]) {
      if(heavy[idx] == to) continue;
      for(int p = in[to]; p < out[to]; p++) {
        expand(ord[p]);
      }
    }
    expand(idx);
    query(idx);
    if(!keep) {
      for(int p = in[idx]; p < out[idx]; p++) shrink(ord[p]);
    }
  }
 
public:
  void build(int root = 0) {
    g = convert_rooted_tree(*this, root).g;
    sz.assign(g.size(), 1);
    heavy.assign(g.size(), -1);
    in.resize(g.size());
    out.resize(g.size());
    build_subtree(root);
    dfs(root, false);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

