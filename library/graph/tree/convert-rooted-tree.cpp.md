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


# :warning: ConvertRootedTree(根付き木に変換) <small>(graph/tree/convert-rooted-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#28790b6202284cbbffc9d712b59f4b80">graph/tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/tree/convert-rooted-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-30 02:08:59+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief ConvertRootedTree(根付き木に変換)
 */
template< typename T >
Graph< T > convert_rooted_tree(const Graph< T > &g, int r = 0) {
  int N = (int) g.size();
  Graph< T > rg(N);
  vector< int > v(N);
  v[r] = 1;
  queue< int > que;
  que.emplace(r);
  while(!que.empty()) {
    auto p = que.front();
    que.pop();
    for(auto &to : g.g[p]) {
      if(v[to] == 0) {
        v[to] = 1;
        que.emplace(to);
        rg.add_directed_edge(p, to, to.cost);
      }
    }
  }
  return rg;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/tree/convert-rooted-tree.cpp"
/**
 * @brief ConvertRootedTree(根付き木に変換)
 */
template< typename T >
Graph< T > convert_rooted_tree(const Graph< T > &g, int r = 0) {
  int N = (int) g.size();
  Graph< T > rg(N);
  vector< int > v(N);
  v[r] = 1;
  queue< int > que;
  que.emplace(r);
  while(!que.empty()) {
    auto p = que.front();
    que.pop();
    for(auto &to : g.g[p]) {
      if(v[to] == 0) {
        v[to] = 1;
        que.emplace(to);
        rg.add_directed_edge(p, to, to.cost);
      }
    }
  }
  return rg;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

