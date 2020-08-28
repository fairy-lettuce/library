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


# :heavy_check_mark: Link-Cut-Tree <small>(structure/develop/link-cut-tree.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#b1cd1e8cabf258d1ad55a5bb477f1b01">structure/develop</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/develop/link-cut-tree.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-29 03:56:51+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-2450-3.test.cpp.html">test/verify/aoj-2450-3.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp.html">test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp</a>
* :heavy_check_mark: <a href="../../../verify/test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp.html">test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Link-Cut-Tree
 */
template< typename STp >
struct LinkCutTree : STp {
  using ST = STp;
  using ST::ST;
  using Node = typename ST::Node;

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
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/develop/link-cut-tree.cpp"
/**
 * @brief Link-Cut-Tree
 */
template< typename STp >
struct LinkCutTree : STp {
  using ST = STp;
  using ST::ST;
  using Node = typename ST::Node;

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
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

