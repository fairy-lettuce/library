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


# :heavy_check_mark: Leftist-Heap <small>(structure/heap/leftist-heap.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#36999f024b84f3ad86db908172fedb57">structure/heap</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/heap/leftist-heap.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 22:49:30+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-alds-1-9-c.test.cpp.html">test/verify/aoj-alds-1-9-c.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Leftist-Heap
 */
template< typename T, bool isMin = true >
struct LeftistHeap {
  struct Node {
    Node *l, *r;
    int s;
    T key;

    explicit Node(const T &key) : key(key), s(1), l(nullptr), r(nullptr) {}
  };

  LeftistHeap() = default;

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *alloc(const T &key) {
    return new Node(key);
  }

  Node *meld(Node *a, Node *b) {
    if(!a || !b) return a ? a : b;
    if((a->key < b->key) ^ isMin) swap(a, b);
    a = clone(a);
    a->r = meld(a->r, b);
    if(!a->l || a->l->s < a->r->s) swap(a->l, a->r);
    a->s = (a->r ? a->r->s : 0) + 1;
    return a;
  }

  Node *push(Node *t, const T &key) {
    return meld(t, alloc(key));
  }

  Node *pop(Node *t) {
    assert(t != nullptr);
    auto ret = meld(t->l, t->r);
    delete t;
    return ret;
  }

  Node *make_root() {
    return nullptr;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/heap/leftist-heap.cpp"
/**
 * @brief Leftist-Heap
 */
template< typename T, bool isMin = true >
struct LeftistHeap {
  struct Node {
    Node *l, *r;
    int s;
    T key;

    explicit Node(const T &key) : key(key), s(1), l(nullptr), r(nullptr) {}
  };

  LeftistHeap() = default;

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *alloc(const T &key) {
    return new Node(key);
  }

  Node *meld(Node *a, Node *b) {
    if(!a || !b) return a ? a : b;
    if((a->key < b->key) ^ isMin) swap(a, b);
    a = clone(a);
    a->r = meld(a->r, b);
    if(!a->l || a->l->s < a->r->s) swap(a->l, a->r);
    a->s = (a->r ? a->r->s : 0) + 1;
    return a;
  }

  Node *push(Node *t, const T &key) {
    return meld(t, alloc(key));
  }

  Node *pop(Node *t) {
    assert(t != nullptr);
    auto ret = meld(t->l, t->r);
    delete t;
    return ret;
  }

  Node *make_root() {
    return nullptr;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

