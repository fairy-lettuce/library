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


# :heavy_check_mark: Union-Find <small>(structure/union-find/union-find.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#16695eacefd17254ea5bccf40066c856">structure/union-find</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/union-find/union-find.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-19 21:42:58+09:00




## 概要

集合を高速に扱うためのデータ構造. 集合を合併する操作(unite), ある要素がどの集合に属しているか(find) を問い合わせる操作を行うことが出来る.

* `unite(x, y)`: 集合 `x` と `y` を併合する. 併合済のとき `false`, 未併合のとき `true` が返される.
* `find(k)`: 要素 `k` が属する集合を求める.
* `size(k)`: 要素 `k` が属する集合の要素の数を求める.
* `same(x, y)`: 要素 `x`, `y` が同じ集合に属するか判定する.

## 計算量

* クエリ: ならし $O(\alpha(N))$ ($\alpha$ はアッカーマンの逆関数) 


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2821.test.cpp.html">test/verify/aoj-2821.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-3139.test.cpp.html">test/verify/aoj-3139.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dsl-1-a.test.cpp.html">test/verify/aoj-dsl-1-a.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-a-2.test.cpp.html">test/verify/aoj-grl-2-a-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-a-3.test.cpp.html">test/verify/aoj-grl-2-a-3.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-b.test.cpp.html">test/verify/aoj-grl-2-b.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Union-Find
 * @docs docs/union-find.md
 */
struct UnionFind {
  vector< int > data;

  UnionFind() = default;

  explicit UnionFind(size_t sz) : data(sz, -1) {}

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return false;
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return true;
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return data[k] = find(data[k]);
  }

  int size(int k) {
    return -data[find(k)];
  }

  bool same(int x, int y) {
    return find(x) == find(y);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/union-find/union-find.cpp"
/**
 * @brief Union-Find
 * @docs docs/union-find.md
 */
struct UnionFind {
  vector< int > data;

  UnionFind() = default;

  explicit UnionFind(size_t sz) : data(sz, -1) {}

  bool unite(int x, int y) {
    x = find(x), y = find(y);
    if(x == y) return false;
    if(data[x] > data[y]) swap(x, y);
    data[x] += data[y];
    data[y] = x;
    return true;
  }

  int find(int k) {
    if(data[k] < 0) return (k);
    return data[k] = find(data[k]);
  }

  int size(int k) {
    return -data[find(k)];
  }

  bool same(int x, int y) {
    return find(x) == find(y);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

