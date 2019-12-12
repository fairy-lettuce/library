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


# :heavy_check_mark: structure/heap/skew-heap.cpp
<a href="../../../index.html">Back to top page</a>

* category: structure/heap
* <a href="{{ site.github.repository_url }}/blob/master/structure/heap/skew-heap.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Verified With
* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-grl-2-b.test.cpp.html">test/verify/aoj-grl-2-b.test.cpp</a>


## Code
{% raw %}
```cpp
template< typename T, typename E = T >
struct SkewHeap {
  using G = function< T(T, E) >;
  using H = function< E(E, E) >;
 
  struct Node {
    T key;
    E lazy;
    Node *l, *r;
  };
 
  const bool rev;
  const G g;
  const H h;
 
  SkewHeap(bool rev = false) : g([](const T &a, const E &b) { return a + b; }),
                               h([](const E &a, const E &b) { return a + b; }), rev(rev) {}
 
  SkewHeap(const G &g, const H &h, bool rev = false) : g(g), h(h), rev(rev) {}
 
  Node *propagate(Node *t) {
    if(t->lazy != 0) {
      if(t->l) t->l->lazy = h(t->l->lazy, t->lazy);
      if(t->r) t->r->lazy = h(t->r->lazy, t->lazy);
      t->key = g(t->key, t->lazy);
      t->lazy = 0;
    }
    return t;
  }
 
  Node *merge(Node *x, Node *y) {
    if(!x || !y) return x ? x : y;
    propagate(x), propagate(y);
    if((x->key > y->key) ^ rev) swap(x, y);
    x->r = merge(y, x->r);
    swap(x->l, x->r);
    return x;
  }
 
  void push(Node *&root, const T &key) {
    root = merge(root, new Node({key, 0, nullptr, nullptr}));
  }
 
  T top(Node *root) {
    return propagate(root)->key;
  }
 
  T pop(Node *&root) {
    T top = propagate(root)->key;
    auto *temp = root;
    root = merge(root->l, root->r);
    delete temp;
    return top;
  }
 
  bool empty(Node *root) const {
    return !root;
  }
 
  void add(Node *root, const E &lazy) {
    if(root) {
      root->lazy = h(root->lazy, lazy);
      propagate(root);
    }
  }
 
  Node *makeheap() {
    return nullptr;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

