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


# :question: Tree-Diameter(木の直径) <small>(graph/tree/tree-diameter.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/tree-diameter.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-28 20:39:54+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-5-a.test.cpp.html">test/verify/aoj-grl-5-a.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-tree-diameter.test.cpp.html">test/verify/yosupo-tree-diameter.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Tree-Diameter(木の直径)
 */
template< typename T = int >
struct TreeDiameter : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< Edge< T > > path;

  T build() {
    to.assign(g.size(), -1);
    auto p = dfs(0, -1);
    auto q = dfs(p.second, -1);

    int now = p.second;
    while(now != q.second) {
      for(auto &e : g[now]) {
        if(to[now] == e.to) {
          path.emplace_back(e);
        }
      }
      now = to[now];
    }
    return q.first;
  }

  explicit TreeDiameter(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > to;

  pair< T, int > dfs(int idx, int par) {
    pair< T, int > ret(0, idx);
    for(auto &e : g[idx]) {
      if(e.to == par) continue;
      auto cost = dfs(e.to, idx);
      cost.first += e.cost;
      if(ret < cost) {
        ret = cost;
        to[idx] = e.to;
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/tree/tree-diameter.cpp"
/**
 * @brief Tree-Diameter(木の直径)
 */
template< typename T = int >
struct TreeDiameter : Graph< T > {
public:
  using Graph< T >::Graph;
  using Graph< T >::g;
  vector< Edge< T > > path;

  T build() {
    to.assign(g.size(), -1);
    auto p = dfs(0, -1);
    auto q = dfs(p.second, -1);

    int now = p.second;
    while(now != q.second) {
      for(auto &e : g[now]) {
        if(to[now] == e.to) {
          path.emplace_back(e);
        }
      }
      now = to[now];
    }
    return q.first;
  }

  explicit TreeDiameter(const Graph< T > &g) : Graph< T >(g) {}

private:
  vector< int > to;

  pair< T, int > dfs(int idx, int par) {
    pair< T, int > ret(0, idx);
    for(auto &e : g[idx]) {
      if(e.to == par) continue;
      auto cost = dfs(e.to, idx);
      cost.first += e.cost;
      if(ret < cost) {
        ret = cost;
        to[idx] = e.to;
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

