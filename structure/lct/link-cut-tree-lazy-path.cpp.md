---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2450-2.test.cpp
    title: test/verify/aoj-2450-2.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/link-cut-tree-lazy-path.md
    document_title: Link-Cut-Tree-Lazy-Path
    links: []
  bundledCode: "#line 1 \"structure/lct/link-cut-tree-lazy-path.cpp\"\n/**\n * @brief\
    \ Link-Cut-Tree-Lazy-Path\n * @docs docs/link-cut-tree-lazy-path.md\n */\ntemplate<\
    \ typename T, typename E, typename F, typename G, typename H, typename S >\nstruct\
    \ LinkCutTreeLazyPath {\n\nprivate:\n  F f;\n  G g;\n  H h;\n  S s;\n  E e0;\n\
    \n  struct Node {\n    Node *l, *r, *p;\n    T key, sum;\n    E lazy;\n    bool\
    \ rev;\n    size_t sz;\n\n    explicit Node(const T &v, const E &e) : key(v),\
    \ sum(v), lazy(e), sz(1), rev(false),\n                                      \
    \      l(nullptr), r(nullptr), p(nullptr) {}\n\n    bool is_root() const {\n \
    \     return not p or (p->l != this and p->r != this);\n    }\n  };\n\npublic:\n\
    \  using NP = Node *;\n\nprivate:\n  NP update(NP t) {\n    t->sz = 1;\n    t->sum\
    \ = t->key;\n    if(t->l) t->sz += t->l->sz, t->sum = f(t->l->sum, t->sum);\n\
    \    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum, t->r->sum);\n    return t;\n\
    \  }\n\n  void rotr(NP t) {\n    NP x = t->p, y = x->p;\n    if((x->l = t->r))\
    \ t->r->p = x;\n    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p\
    \ = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n    \
    \  update(y);\n    }\n  }\n\n  void rotl(NP t) {\n    NP x = t->p, y = x->p;\n\
    \    if((x->r = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n  void toggle(NP t) {\n    swap(t->l,\
    \ t->r);\n    t->sum = s(t->sum);\n    t->rev ^= true;\n  }\n\n  void propagate(NP\
    \ t, const E &e) {\n    t->lazy = h(t->lazy, e);\n    t->key = g(t->key, e);\n\
    \    t->sum = g(t->sum, e);\n  }\n\n  void push(NP t) {\n    if(t->lazy != e0)\
    \ {\n      if(t->l) propagate(t->l, t->lazy);\n      if(t->r) propagate(t->r,\
    \ t->lazy);\n      t->lazy = e0;\n    }\n    if(t->rev) {\n      if(t->l) toggle(t->l);\n\
    \      if(t->r) toggle(t->r);\n      t->rev = false;\n    }\n  }\n\n  void splay(NP\
    \ t) {\n    push(t);\n    while(not t->is_root()) {\n      NP q = t->p;\n    \
    \  if(q->is_root()) {\n        push(q), push(t);\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        NP r = q->p;\n        push(r),\
    \ push(q), push(t);\n        if(r->l == q) {\n          if(q->l == t) rotr(q),\
    \ rotr(t);\n          else rotl(t), rotr(t);\n        } else {\n          if(q->r\
    \ == t) rotl(q), rotl(t);\n          else rotr(t), rotl(t);\n        }\n     \
    \ }\n    }\n  }\n\npublic:\n  LinkCutTreeLazyPath(const F &f, const G &g, const\
    \ H &h, const S &s, const E &e0) :\n      f(f), g(g), h(h), s(s), e0(e0) {}\n\n\
    \  NP alloc(const T &v = T()) {\n    return new Node(v, e0);\n  }\n\n  vector<\
    \ NP > build(vector< T > &vs) {\n    vector< NP > nodes(vs.size());\n    for(int\
    \ i = 0; i < (int) vs.size(); i++) {\n      nodes[i] = alloc(vs[i]);\n    }\n\
    \    return nodes;\n  }\n\n  NP expose(NP t) {\n    NP rp = nullptr;\n    for(NP\
    \ cur = t; cur; cur = cur->p) {\n      splay(cur);\n      cur->r = rp;\n     \
    \ update(cur);\n      rp = cur;\n    }\n    splay(t);\n    return rp;\n  }\n\n\
    \  void evert(NP t) {\n    expose(t);\n    toggle(t);\n    push(t);\n  }\n\n \
    \ void link(NP child, NP parent) {\n    expose(parent);\n    child->p = parent;\n\
    \    parent->r = child;\n    update(parent);\n  }\n\n  void cut(NP child) {\n\
    \    expose(child);\n    NP parent = child->l;\n    child->l = nullptr;\n    parent->p\
    \ = nullptr;\n    update(child);\n  }\n\n  bool is_connected(NP u, NP v) {\n \
    \   expose(u), expose(v);\n    return u == v or u->p;\n  }\n\n  NP lca(NP u, NP\
    \ v) {\n    if(not is_connected(u, v)) return nullptr;\n    expose(u);\n    return\
    \ expose(v);\n  }\n\n  NP get_kth(NP x, int k) {\n    expose(x);\n    while(x)\
    \ {\n      push(x);\n      if(x->r && x->r->sz > k) {\n        x = x->r;\n   \
    \   } else {\n        if(x->r) k -= x->r->sz;\n        if(k == 0) return x;\n\
    \        k -= 1;\n        x = x->l;\n      }\n    }\n    return nullptr;\n  }\n\
    \n  const T &query(NP u) {\n    expose(u);\n    return u->sum;\n  }\n\n  const\
    \ T &query(NP u, NP v) {\n    evert(u);\n    return query(v);\n  }\n\n  void set_key(NP\
    \ t, T v) {\n    expose(t);\n    t->key = v;\n    update(t);\n  }\n\n  void set_propagate(NP\
    \ t, const E &e) {\n    expose(t);\n    propagate(t, e);\n    push(t);\n  }\n\n\
    \  void set_propagate(NP u, NP v, const E &e) {\n    evert(u);\n    set_propagate(v,\
    \ e);\n  }\n};\n\ntemplate< typename T, typename E, typename F, typename G, typename\
    \ H, typename S >\nLinkCutTreeLazyPath< T, E, F, G, H, S > get_link_cut_tree_lazy_path(const\
    \ F &f, const G &g, const H &h, const S &s, const E &e0) {\n  return {f, g, h,\
    \ s, e0};\n}\n"
  code: "/**\n * @brief Link-Cut-Tree-Lazy-Path\n * @docs docs/link-cut-tree-lazy-path.md\n\
    \ */\ntemplate< typename T, typename E, typename F, typename G, typename H, typename\
    \ S >\nstruct LinkCutTreeLazyPath {\n\nprivate:\n  F f;\n  G g;\n  H h;\n  S s;\n\
    \  E e0;\n\n  struct Node {\n    Node *l, *r, *p;\n    T key, sum;\n    E lazy;\n\
    \    bool rev;\n    size_t sz;\n\n    explicit Node(const T &v, const E &e) :\
    \ key(v), sum(v), lazy(e), sz(1), rev(false),\n                              \
    \              l(nullptr), r(nullptr), p(nullptr) {}\n\n    bool is_root() const\
    \ {\n      return not p or (p->l != this and p->r != this);\n    }\n  };\n\npublic:\n\
    \  using NP = Node *;\n\nprivate:\n  NP update(NP t) {\n    t->sz = 1;\n    t->sum\
    \ = t->key;\n    if(t->l) t->sz += t->l->sz, t->sum = f(t->l->sum, t->sum);\n\
    \    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum, t->r->sum);\n    return t;\n\
    \  }\n\n  void rotr(NP t) {\n    NP x = t->p, y = x->p;\n    if((x->l = t->r))\
    \ t->r->p = x;\n    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p\
    \ = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n    \
    \  update(y);\n    }\n  }\n\n  void rotl(NP t) {\n    NP x = t->p, y = x->p;\n\
    \    if((x->r = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n  void toggle(NP t) {\n    swap(t->l,\
    \ t->r);\n    t->sum = s(t->sum);\n    t->rev ^= true;\n  }\n\n  void propagate(NP\
    \ t, const E &e) {\n    t->lazy = h(t->lazy, e);\n    t->key = g(t->key, e);\n\
    \    t->sum = g(t->sum, e);\n  }\n\n  void push(NP t) {\n    if(t->lazy != e0)\
    \ {\n      if(t->l) propagate(t->l, t->lazy);\n      if(t->r) propagate(t->r,\
    \ t->lazy);\n      t->lazy = e0;\n    }\n    if(t->rev) {\n      if(t->l) toggle(t->l);\n\
    \      if(t->r) toggle(t->r);\n      t->rev = false;\n    }\n  }\n\n  void splay(NP\
    \ t) {\n    push(t);\n    while(not t->is_root()) {\n      NP q = t->p;\n    \
    \  if(q->is_root()) {\n        push(q), push(t);\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        NP r = q->p;\n        push(r),\
    \ push(q), push(t);\n        if(r->l == q) {\n          if(q->l == t) rotr(q),\
    \ rotr(t);\n          else rotl(t), rotr(t);\n        } else {\n          if(q->r\
    \ == t) rotl(q), rotl(t);\n          else rotr(t), rotl(t);\n        }\n     \
    \ }\n    }\n  }\n\npublic:\n  LinkCutTreeLazyPath(const F &f, const G &g, const\
    \ H &h, const S &s, const E &e0) :\n      f(f), g(g), h(h), s(s), e0(e0) {}\n\n\
    \  NP alloc(const T &v = T()) {\n    return new Node(v, e0);\n  }\n\n  vector<\
    \ NP > build(vector< T > &vs) {\n    vector< NP > nodes(vs.size());\n    for(int\
    \ i = 0; i < (int) vs.size(); i++) {\n      nodes[i] = alloc(vs[i]);\n    }\n\
    \    return nodes;\n  }\n\n  NP expose(NP t) {\n    NP rp = nullptr;\n    for(NP\
    \ cur = t; cur; cur = cur->p) {\n      splay(cur);\n      cur->r = rp;\n     \
    \ update(cur);\n      rp = cur;\n    }\n    splay(t);\n    return rp;\n  }\n\n\
    \  void evert(NP t) {\n    expose(t);\n    toggle(t);\n    push(t);\n  }\n\n \
    \ void link(NP child, NP parent) {\n    expose(parent);\n    child->p = parent;\n\
    \    parent->r = child;\n    update(parent);\n  }\n\n  void cut(NP child) {\n\
    \    expose(child);\n    NP parent = child->l;\n    child->l = nullptr;\n    parent->p\
    \ = nullptr;\n    update(child);\n  }\n\n  bool is_connected(NP u, NP v) {\n \
    \   expose(u), expose(v);\n    return u == v or u->p;\n  }\n\n  NP lca(NP u, NP\
    \ v) {\n    if(not is_connected(u, v)) return nullptr;\n    expose(u);\n    return\
    \ expose(v);\n  }\n\n  NP get_kth(NP x, int k) {\n    expose(x);\n    while(x)\
    \ {\n      push(x);\n      if(x->r && x->r->sz > k) {\n        x = x->r;\n   \
    \   } else {\n        if(x->r) k -= x->r->sz;\n        if(k == 0) return x;\n\
    \        k -= 1;\n        x = x->l;\n      }\n    }\n    return nullptr;\n  }\n\
    \n  const T &query(NP u) {\n    expose(u);\n    return u->sum;\n  }\n\n  const\
    \ T &query(NP u, NP v) {\n    evert(u);\n    return query(v);\n  }\n\n  void set_key(NP\
    \ t, T v) {\n    expose(t);\n    t->key = v;\n    update(t);\n  }\n\n  void set_propagate(NP\
    \ t, const E &e) {\n    expose(t);\n    propagate(t, e);\n    push(t);\n  }\n\n\
    \  void set_propagate(NP u, NP v, const E &e) {\n    evert(u);\n    set_propagate(v,\
    \ e);\n  }\n};\n\ntemplate< typename T, typename E, typename F, typename G, typename\
    \ H, typename S >\nLinkCutTreeLazyPath< T, E, F, G, H, S > get_link_cut_tree_lazy_path(const\
    \ F &f, const G &g, const H &h, const S &s, const E &e0) {\n  return {f, g, h,\
    \ s, e0};\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/lct/link-cut-tree-lazy-path.cpp
  requiredBy: []
  timestamp: '2021-05-09 20:53:58+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-2450-2.test.cpp
documentation_of: structure/lct/link-cut-tree-lazy-path.cpp
layout: document
redirect_from:
- /library/structure/lct/link-cut-tree-lazy-path.cpp
- /library/structure/lct/link-cut-tree-lazy-path.cpp.html
title: Link-Cut-Tree-Lazy-Path
---
## 概要

Link Cut Tree とは動的木の一つで, 辺の追加や削除などの木構造の動的な変化がある場合でも効率的にクエリを処理できる.


## 使い方

* `LinkCutTree(f, g, h, s, e0)`: コンストラクタ. `f` は 2 つの要素の値をマージする二項演算, `g` は要素と作用素をマージする二項演算, `h` は作用素同士をマージする二項演算, `s` は要素を反転する演算を指す. また　`e0` は作用素の単位元を指す.
* `alloc(v)`: 要素の値を `v` としたノードを生成する.
* `build(vs)`: 各要素の値を `vs[i]` としたノードを生成し, その配列を返す.
* `expose(t)`: `t` と根をつなげて, `t` を splay Tree の根にする.
* `evert(t)`: `t` を根に変更する.
* `link(child, parent)`: `child` の親を `parent` にする. `child` と `parent` は別の連結成分で, `child` が根であることを要求する.
* `cut(child)`: `child` の親と `child` を切り離す.
* `is_connected(u, v)`: `u` と `v` が同じ連結成分に属する場合は `true`, そうでなければ `false` を返す.
* `lca(u, v)`: `u` と `v` の lca を返す. `u` と `v` が異なる連結成分なら `nullptr` を返す.
* `get_kth(x, k)`: `x` から根までのパスに出現するノードを並べたとき, 0-indexed で `k` 番目のノードを返す.
* `query(u)`: `u` から根までのパス上の頂点の値を二項演算でまとめた結果を返す.
* `query(u, v)`: `u` から `v` までのパス上の頂点の値を二項演算でまとめた結果を返す.
* `set_key(t, v)`: `t` の値を `v` に変更する.
* `set_propagate(t, e)`: `t` から根までのパス上の頂点に作用素 `e` を加える.
* `set_propagate(u, v, e)`: `u` から `v` までのパス上の頂点に作用素 `e` を加える.

## 計算量

* 各クエリ ならし $O(\log n)$
