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


# :warning: Persistent-Weight-Balanced-Tree(永続重み平衡木) <small>(structure/bbst/persistent-weight-balanced-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#ac1922c227762d9e573c4f7aedc86899">structure/bbst</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/bbst/persistent-weight-balanced-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-14 22:00:37+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Persistent-Weight-Balanced-Tree(永続重み平衡木)
 */
template< typename Monoid, typename F, size_t FULL = 1000 >
struct PersistentWeightBalancedTree : WeightBalancedTree< Monoid, F > {
  using WBT = WeightBalancedTree< Monoid, F >;
  using WBT::WeightBalancedTree;
  using Node = typename WBT::Node;

private:
  Node *clone(Node *t) override {
    return &(*WBT::pool.alloc() = *t);
  }

public:
  Node *rebuild(Node *r) {
    auto ret = WBT::dump(r);
    WBT::pool.clear();
    return WBT::build(ret);
  }

  bool almost_full() const {
    return this->pool.ptr < FULL;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/bbst/persistent-weight-balanced-tree.cpp"
/**
 * @brief Persistent-Weight-Balanced-Tree(永続重み平衡木)
 */
template< typename Monoid, typename F, size_t FULL = 1000 >
struct PersistentWeightBalancedTree : WeightBalancedTree< Monoid, F > {
  using WBT = WeightBalancedTree< Monoid, F >;
  using WBT::WeightBalancedTree;
  using Node = typename WBT::Node;

private:
  Node *clone(Node *t) override {
    return &(*WBT::pool.alloc() = *t);
  }

public:
  Node *rebuild(Node *r) {
    auto ret = WBT::dump(r);
    WBT::pool.clear();
    return WBT::build(ret);
  }

  bool almost_full() const {
    return this->pool.ptr < FULL;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

