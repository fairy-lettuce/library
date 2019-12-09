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


# :warning: structure/bbst/persistent-red-black-tree.cpp
* category: structure/bbst


[Back to top page](../../../index.html)



## Code
{% raw %}
```cpp
template< class D, class L, D (*f)(D, D), D (*g)(D, L), L (*h)(L, L), L (*p)(L, int) >
struct PersistentRedBlackTree : RedBlackTree< D, L, f, g, h, p > {
  using RBT = RedBlackTree< D, L, f, g, h, p >;
  using Node = typename RBT::Node;

  PersistentRedBlackTree(int sz, const D &M1, const L &OM0) :
      RBT(sz, M1, OM0) {}

  Node *clone(Node *t) override { return &(*RBT::pool.alloc() = *t); }

  Node *rebuild(Node *r) {
    auto ret = RBT::dump(r);
    RBT::pool.clear();
    return RBT::build(ret);
  }
};

```
{% endraw %}

[Back to top page](../../../index.html)

