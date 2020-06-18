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


# :x: Link-Cut-Tree <small>(structure/others/link-cut-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#40d73e22b7d986e3399449c25c8b23a1">structure/others</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/others/link-cut-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-18 21:29:10+09:00




## Verified with

* :x: <a href="../../../verify/test/verify/aoj-2450-2.test.cpp.html">test/verify/aoj-2450-2.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-dynamic-tree-vertex-add-path-sum.test.cpp.html">test/verify/yosupo-dynamic-tree-vertex-add-path-sum.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp.html">test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Link-Cut-Tree
 */
template< template< typename, typename > typename ST, typename Monoid = int, typename OperatorMonoid = Monoid >
struct LinkCutTree : ST< Monoid, OperatorMonoid > {
  using LST = ST< Monoid, OperatorMonoid >;
  using LST::ST;
  using Node = typename LST::Node;

  Node *expose(Node *t) {
    Node *rp = nullptr;
    for(Node *cur = t; cur; cur = cur->p) {
      this->splay(cur);
      cur->r = rp;
      this->update(cur);
      rp = cur;
    }
    this->splay(t);
    return rp;
  }

  void link(Node *child, Node *parent) {
    expose(child);
    expose(parent);
    child->p = parent;
    parent->r = child;
    this->update(parent);
  }

  void cut(Node *child) {
    expose(child);
    auto *parent = child->l;
    child->l = nullptr;
    parent->p = nullptr;
    this->update(child);
  }

  void evert(Node *t) {
    expose(t);
    this->toggle(t);
    this->push(t);
  }

  Node *lca(Node *u, Node *v) {
    if(get_root(u) != get_root(v)) return nullptr;
    expose(u);
    return expose(v);
  }

  void set_propagate(Node *t, const OperatorMonoid &x) {
    expose(t);
    LST::set_propagate(t, x);
  }

  Node *get_kth(Node *x, int k) {
    expose(x);
    while(x) {
      this->push(x);
      if(x->r && x->r->sz > k) {
        x = x->r;
      } else {
        if(x->r) k -= x->r->sz;
        if(k == 0) return x;
        k -= 1;
        x = x->l;
      }
    }
    return nullptr;
  }

  Node *get_root(Node *x) {
    expose(x);
    while(x->l) {
      this->push(x);
      x = x->l;
    }
    return x;
  }

  const Monoid &query(Node *t) {
    expose(t);
    return t->sum;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/others/link-cut-tree.cpp"
/**
 * @brief Link-Cut-Tree
 */
template< template< typename, typename > typename ST, typename Monoid = int, typename OperatorMonoid = Monoid >
struct LinkCutTree : ST< Monoid, OperatorMonoid > {
  using LST = ST< Monoid, OperatorMonoid >;
  using LST::ST;
  using Node = typename LST::Node;

  Node *expose(Node *t) {
    Node *rp = nullptr;
    for(Node *cur = t; cur; cur = cur->p) {
      this->splay(cur);
      cur->r = rp;
      this->update(cur);
      rp = cur;
    }
    this->splay(t);
    return rp;
  }

  void link(Node *child, Node *parent) {
    expose(child);
    expose(parent);
    child->p = parent;
    parent->r = child;
    this->update(parent);
  }

  void cut(Node *child) {
    expose(child);
    auto *parent = child->l;
    child->l = nullptr;
    parent->p = nullptr;
    this->update(child);
  }

  void evert(Node *t) {
    expose(t);
    this->toggle(t);
    this->push(t);
  }

  Node *lca(Node *u, Node *v) {
    if(get_root(u) != get_root(v)) return nullptr;
    expose(u);
    return expose(v);
  }

  void set_propagate(Node *t, const OperatorMonoid &x) {
    expose(t);
    LST::set_propagate(t, x);
  }

  Node *get_kth(Node *x, int k) {
    expose(x);
    while(x) {
      this->push(x);
      if(x->r && x->r->sz > k) {
        x = x->r;
      } else {
        if(x->r) k -= x->r->sz;
        if(k == 0) return x;
        k -= 1;
        x = x->l;
      }
    }
    return nullptr;
  }

  Node *get_root(Node *x) {
    expose(x);
    while(x->l) {
      this->push(x);
      x = x->l;
    }
    return x;
  }

  const Monoid &query(Node *t) {
    expose(t);
    return t->sum;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

