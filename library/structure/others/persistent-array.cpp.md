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


# :warning: structure/others/persistent-array.cpp
* category: structure/others


[Back to top page](../../../index.html)



## Code
{% raw %}
```cpp
template< typename T, int LOG >
struct PersistentArray {
  struct Node {
    T data;
    Node *child[1 << LOG] = {};

    Node() {}

    Node(const T &data) : data(data) {}
  };

  Node *root;

  PersistentArray() : root(nullptr) {}

  T get(Node *t, int k) {
    if(k == 0) return t->data;
    return get(t->child[k & ((1 << LOG) - 1)], k >> LOG);
  }

  T get(const int &k) {
    return get(root, k);
  }

  pair< Node *, T * > mutable_get(Node *t, int k) {
    t = t ? new Node(*t) : new Node();
    if(k == 0) return {t, &t->data};
    auto p = mutable_get(t->child[k & ((1 << LOG) - 1)], k >> LOG);
    t->child[k & ((1 << LOG) - 1)] = p.first;
    return {t, p.second};
  }

  T *mutable_get(const int &k) {
    auto ret = mutable_get(root, k);
    root = ret.first;
    return ret.second;
  }

  Node *build(Node *t, const T &data, int k) {
    if(!t) t = new Node();
    if(k == 0) {
      t->data = data;
      return t;
    }
    auto p = build(t->child[k & ((1 << LOG) - 1)], data, k >> LOG);
    t->child[k & ((1 << LOG) - 1)] = p;
    return t;
  }

  void build(const vector< T > &v) {
    root = nullptr;
    for(int i = 0; i < v.size(); i++) {
      root = build(root, v[i], i);
    }
  }
};


```
{% endraw %}

[Back to top page](../../../index.html)

