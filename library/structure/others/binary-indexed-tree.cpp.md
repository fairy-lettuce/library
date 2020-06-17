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


# :heavy_check_mark: Binary-Indexed-Tree(BIT) <small>(structure/others/binary-indexed-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/binary-indexed-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-17 14:51:53+09:00




## 概要

Fenwick Tree とも呼ばれる. 数列に対し, ある要素に値を加える操作と, 区間和を求める操作をそれぞれ対数時間で行うことが出来るデータ構造. セグメント木や平衡二分探索
木の機能を制限したものであるが, 実装が非常に単純で定数倍も軽いなどの利点がある.

* `BinaryIndexedTree(sz)`: 長さ `sz` の $0$ で初期化された配列で構築する.
* `BinaryIndexedTree(vs)`: 配列 `vs` で構築する.
* `add(k, x)`: 要素 `k` に値 `x` を加える.
* `query(k)`: 区間 $[0,k]$ の総和を求める(閉区間なので注意すること).
* `lower_bound(x)`: 区間 $[0,k]$ の総和が `x` 以上となる最小の $k$ を返す.
* `upper_bound(x)`: 区間 $[0,k]$ の総和が `x` を上回る最小の $k$ を返す.

## 計算量

* 構築: $O(N)$
* クエリ: $O(\log N)$


## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-dsl-2-b.test.cpp.html">test/verify/aoj-dsl-2-b.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-point-add-rectangle-sum.test.cpp.html">test/verify/yosupo-point-add-rectangle-sum.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Binary-Indexed-Tree(BIT)
 * @docs docs/binary-indexed-tree.md
 */
template< typename T >
struct BinaryIndexedTree {
  vector< T > data;

  BinaryIndexedTree() = default;

  explicit BinaryIndexedTree(size_t sz) : data(sz + 1, 0) {}

  explicit BinaryIndexedTree(const vector< T > &vs) : data(vs.size() + 1, 0) {
    for(size_t i = 0; i < vs.size(); i++) data[i + 1] = vs[i];
    for(size_t i = 1; i < data.size(); i++) {
      size_t j = i + (i & -i);
      if(j < data.size()) data[j] += data[i];
    }
  }

  void add(int k, const T &x) {
    for(++k; k < (int) data.size(); k += k & -k) data[k] += x;
  }

  T query(int k) const {
    T ret = T();
    for(++k; k > 0; k -= k & -k) ret += data[k];
    return ret;
  }

  int lower_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] < x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }

  int upper_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] <= x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/binary-indexed-tree.cpp"
/**
 * @brief Binary-Indexed-Tree(BIT)
 * @docs docs/binary-indexed-tree.md
 */
template< typename T >
struct BinaryIndexedTree {
  vector< T > data;

  BinaryIndexedTree() = default;

  explicit BinaryIndexedTree(size_t sz) : data(sz + 1, 0) {}

  explicit BinaryIndexedTree(const vector< T > &vs) : data(vs.size() + 1, 0) {
    for(size_t i = 0; i < vs.size(); i++) data[i + 1] = vs[i];
    for(size_t i = 1; i < data.size(); i++) {
      size_t j = i + (i & -i);
      if(j < data.size()) data[j] += data[i];
    }
  }

  void add(int k, const T &x) {
    for(++k; k < (int) data.size(); k += k & -k) data[k] += x;
  }

  T query(int k) const {
    T ret = T();
    for(++k; k > 0; k -= k & -k) ret += data[k];
    return ret;
  }

  int lower_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] < x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }

  int upper_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] <= x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

