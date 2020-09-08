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


# :heavy_check_mark: Boruvka(最小全域木) <small>(graph/mst/boruvka.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#51f95ed2fd9ed3be34f576d38fbd25a2">graph/mst</a>
* <a href="{{ site.github.repository_url }}/blob/master/graph/mst/boruvka.cpp">View this file on GitHub</a>
    - Last commit date: 2020-09-08 23:29:00+09:00




## 概要

最小全域木(全域木のうち, その辺群の重みの総和が最小になる木)を求める. それぞれの連結成分について, 他の連結成分を結ぶ重みが最小の辺を求めて縮約を繰り返すことにより最小全域木を求める. 繰り返し回数は $O(\log V)$ 回なので、普通の最小全域木であれば $O(E \log V)$ で求めることができる.

## 使い方
* `build(update)`: 最小全域木を求める. `update` の引数の型は `vector< pair< T, int > >&' (参照渡しなので注意). 引数で渡された要素のうち, それぞれの代表元について, 最小コストで向かえる連結成分の {コスト, その代表元(頂点番号でも良い)} を格納する処理をする(わからないと思うので詳細はverify コードを参照してください). 各頂点 $k$ の代表元を求める際には `find(k)` を呼び出すこと.
* `find(k)`: 現在の頂点 `k` が属する連結成分の代表元を返す.

## 計算量

* $O(E \log V)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-a-3.test.cpp.html">test/verify/aoj-grl-2-a-3.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Boruvka(最小全域木)
 * @docs docs/boruvka.md
 */
template< typename T >
struct Boruvka {
private:
  size_t V;
  const T INF;
  UnionFind uf;

public:
  explicit Boruvka(size_t V, T INF = numeric_limits< T >::max()) : V(V), uf(V), INF(INF) {}

  inline int find(int k) {
    return uf.find(k);
  }

  template< typename F >
  T build(const F &update) {
    T ret = T();
    while(uf.size(0) < V) {
      vector< pair< T, int > > v(V, make_pair(INF, -1));
      update(v);
      bool con = false;
      for(int i = 0; i < V; i++) {
        if(v[i].second >= 0 && uf.unite(i, v[i].second)) {
          ret += v[i].first;
          con = true;
        }
      }
      if(!con) return INF;
    }
    return ret;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "graph/mst/boruvka.cpp"
/**
 * @brief Boruvka(最小全域木)
 * @docs docs/boruvka.md
 */
template< typename T >
struct Boruvka {
private:
  size_t V;
  const T INF;
  UnionFind uf;

public:
  explicit Boruvka(size_t V, T INF = numeric_limits< T >::max()) : V(V), uf(V), INF(INF) {}

  inline int find(int k) {
    return uf.find(k);
  }

  template< typename F >
  T build(const F &update) {
    T ret = T();
    while(uf.size(0) < V) {
      vector< pair< T, int > > v(V, make_pair(INF, -1));
      update(v);
      bool con = false;
      for(int i = 0; i < V; i++) {
        if(v[i].second >= 0 && uf.unite(i, v[i].second)) {
          ret += v[i].first;
          con = true;
        }
      }
      if(!con) return INF;
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

