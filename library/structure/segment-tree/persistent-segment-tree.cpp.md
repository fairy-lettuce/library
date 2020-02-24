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


# :warning: Persistent-Segment-Tree(永続セグメント木) <small>(structure/segment-tree/persistent-segment-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#bd066fce418dc5d58690e9bbe0a7a21f">structure/segment-tree</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/segment-tree/persistent-segment-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-20 22:23:04+09:00




## 概要

セグメント木のある要素に対して何らかの更新を行うとする. ここで更新後のセグメント木をすべてコピーして残しておくことが永続であるが, これを単純に実装すると, $1$ 回のコピーに $O(N)$ かかってこわれてしまう. $1$ 回の更新によって $O(\log N)$ 個のノードの情報しか変化しないので, 変化したノードの情報だけ新しくノードを生成してその部分のみ張り替えるする操作を行えば $O(\log N)$ でのコピーが可能になり, これは一般のセグメント木の計算量と変わらない.

* `PersistentSegmentTree(f, M1)`: `f` は2つの区間の要素をマージする二項演算, `M1` はモノイドの単位元である.
* `build(v)`: 配列 `v` を各要素としたセグメント木を構築し, その根を返す.
* `update(t, k, x)`: `t` を根とするセグメント木に対し `k` 番目の要素を `x` に更新し, 更新後の根を返す.
* `query(t, a, b)`: `t` を根とするセグメント木に対し, 区間 $[a, b)$ の要素を二項演算した結果を返す.


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Persistent-Segment-Tree(永続セグメント木)
 * @docs docs/persistent-segment-tree.md
 */
template< typename Monoid >
struct PersistentSegmentTree {
  using F = function< Monoid(Monoid, Monoid) >;

  struct Node {
    Monoid data;
    Node *l, *r;

    Node(const Monoid &data) : data(data), l(nullptr), r(nullptr) {}
  };

  int sz;
  const F f;
  const Monoid M1;

  PersistentSegmentTree(const F f, const Monoid &M1) : f(f), M1(M1) {}

  Node *build(vector< Monoid > &v) {
    sz = (int) v.size();
    return build(0, (int) v.size(), v);
  }

  Node *merge(Node *l, Node *r) {
    auto t = new Node(f(l->data, r->data));
    t->l = l;
    t->r = r;
    return t;
  }

  Node *build(int l, int r, vector< Monoid > &v) {
    if(l + 1 >= r) return new Node(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *update(int a, const Monoid &x, Node *k, int l, int r) {
    if(r <= a || a + 1 <= l) {
      return k;
    } else if(a <= l && r <= a + 1) {
      return new Node(x);
    } else {
      return merge(update(a, x, k->l, l, (l + r) >> 1), update(a, x, k->r, (l + r) >> 1, r));
    }
  }

  Node *update(Node *t, int k, const Monoid &x) {
    return update(k, x, t, 0, sz);
  }

  Monoid query(int a, int b, Node *k, int l, int r) {
    if(r <= a || b <= l) {
      return M1;
    } else if(a <= l && r <= b) {
      return k->data;
    } else {
      return f(query(a, b, k->l, l, (l + r) >> 1),
               query(a, b, k->r, (l + r) >> 1, r));
    }
  }

  Monoid query(Node *t, int a, int b) {
    return query(a, b, t, 0, sz);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/segment-tree/persistent-segment-tree.cpp"
/**
 * @brief Persistent-Segment-Tree(永続セグメント木)
 * @docs docs/persistent-segment-tree.md
 */
template< typename Monoid >
struct PersistentSegmentTree {
  using F = function< Monoid(Monoid, Monoid) >;

  struct Node {
    Monoid data;
    Node *l, *r;

    Node(const Monoid &data) : data(data), l(nullptr), r(nullptr) {}
  };

  int sz;
  const F f;
  const Monoid M1;

  PersistentSegmentTree(const F f, const Monoid &M1) : f(f), M1(M1) {}

  Node *build(vector< Monoid > &v) {
    sz = (int) v.size();
    return build(0, (int) v.size(), v);
  }

  Node *merge(Node *l, Node *r) {
    auto t = new Node(f(l->data, r->data));
    t->l = l;
    t->r = r;
    return t;
  }

  Node *build(int l, int r, vector< Monoid > &v) {
    if(l + 1 >= r) return new Node(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *update(int a, const Monoid &x, Node *k, int l, int r) {
    if(r <= a || a + 1 <= l) {
      return k;
    } else if(a <= l && r <= a + 1) {
      return new Node(x);
    } else {
      return merge(update(a, x, k->l, l, (l + r) >> 1), update(a, x, k->r, (l + r) >> 1, r));
    }
  }

  Node *update(Node *t, int k, const Monoid &x) {
    return update(k, x, t, 0, sz);
  }

  Monoid query(int a, int b, Node *k, int l, int r) {
    if(r <= a || b <= l) {
      return M1;
    } else if(a <= l && r <= b) {
      return k->data;
    } else {
      return f(query(a, b, k->l, l, (l + r) >> 1),
               query(a, b, k->r, (l + r) >> 1, r));
    }
  }

  Monoid query(Node *t, int a, int b) {
    return query(a, b, t, 0, sz);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

