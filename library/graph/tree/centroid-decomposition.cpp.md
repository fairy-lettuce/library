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


# :heavy_check_mark: Centroid-Decomosition(重心分解) <small>(graph/tree/centroid-decomposition.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/centroid-decomposition.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-26 01:18:25+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3139.test.cpp.html">test/verify/aoj-3139.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yukicoder-1002.test.cpp.html">test/verify/yukicoder-1002.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
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

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

