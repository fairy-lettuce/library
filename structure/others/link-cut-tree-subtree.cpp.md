---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/others/link-cut-tree-subtree.cpp\"\ntemplate<\
    \ typename SUM, typename KEY >\nstruct LinkCutTreeSubtree {\n \n  struct Node\
    \ {\n    Node *l, *r, *p;\n \n    KEY key;\n    SUM sum;\n \n    bool rev;\n \
    \   int sz;\n \n    bool is_root() const {\n      return !p || (p->l != this &&\
    \ p->r != this);\n    }\n \n    Node(const KEY &key, const SUM &sum) :\n     \
    \   key(key), sum(sum), rev(false), sz(1),\n        l(nullptr), r(nullptr), p(nullptr)\
    \ {}\n  };\n \n  const SUM ident;\n \n  LinkCutTreeSubtree(const SUM &ident) :\
    \ ident(ident) {}\n \n  Node *make_node(const KEY &key) {\n    auto ret = new\
    \ Node(key, ident);\n    update(ret);\n    return ret;\n  }\n \n  Node *set_key(Node\
    \ *t, const KEY &key) {\n    expose(t);\n    t->key = key;\n    update(t);\n \
    \   return t;\n  }\n \n  void toggle(Node *t) {\n    swap(t->l, t->r);\n    t->sum.toggle();\n\
    \    t->rev ^= true;\n  }\n \n  void push(Node *t) {\n    if(t->rev) {\n     \
    \ if(t->l) toggle(t->l);\n      if(t->r) toggle(t->r);\n      t->rev = false;\n\
    \    }\n  }\n \n \n  void update(Node *t) {\n    t->sz = 1;\n    if(t->l) t->sz\
    \ += t->l->sz;\n    if(t->r) t->sz += t->r->sz;\n    t->sum.merge(t->key, t->l\
    \ ? t->l->sum : ident, t->r ? t->r->sum : ident);\n  }\n \n  void rotr(Node *t)\
    \ {\n    auto *x = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n    t->r\
    \ = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l\
    \ == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\
    \ \n  void rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r = t->l))\
    \ t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n    if((t->p\
    \ = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n    \
    \  update(y);\n    }\n  }\n \n \n  void splay(Node *t) {\n    push(t);\n    while(!t->is_root())\
    \ {\n      auto *q = t->p;\n      if(q->is_root()) {\n        push(q), push(t);\n\
    \        if(q->l == t) rotr(t);\n        else rotl(t);\n      } else {\n     \
    \   auto *r = q->p;\n        push(r), push(q), push(t);\n        if(r->l == q)\
    \ {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t), rotr(t);\n\
    \        } else {\n          if(q->r == t) rotl(q), rotl(t);\n          else rotr(t),\
    \ rotl(t);\n        }\n      }\n    }\n  }\n \n \n  Node *expose(Node *t) {\n\
    \    Node *rp = nullptr;\n    for(auto *cur = t; cur; cur = cur->p) {\n      splay(cur);\n\
    \      if(cur->r) cur->sum.add(cur->r->sum);\n      cur->r = rp;\n      if(cur->r)\
    \ cur->sum.erase(cur->r->sum);\n      update(cur);\n      rp = cur;\n    }\n \
    \   splay(t);\n    return rp;\n  }\n \n  void link(Node *child, Node *parent)\
    \ {\n    expose(child);\n    expose(parent);\n    child->p = parent;\n    parent->r\
    \ = child;\n    update(parent);\n  }\n \n  void cut(Node *child) {\n    expose(child);\n\
    \    auto *parent = child->l;\n    child->l = nullptr;\n    parent->p = nullptr;\n\
    \    update(child);\n  }\n \n  void evert(Node *t) {\n    expose(t);\n    toggle(t);\n\
    \    push(t);\n  }\n \n  Node *lca(Node *u, Node *v) {\n    if(get_root(u) !=\
    \ get_root(v)) return nullptr;\n    expose(u);\n    return expose(v);\n  }\n \n\
    \ \n  Node *get_kth(Node *x, int k) {\n    expose(x);\n    while(x) {\n      push(x);\n\
    \      if(x->r && x->r->sz > k) {\n        x = x->r;\n      } else {\n       \
    \ if(x->r) k -= x->r->sz;\n        if(k == 0) return x;\n        k -= 1;\n   \
    \     x = x->l;\n      }\n    }\n    return nullptr;\n  }\n \n  Node *get_root(Node\
    \ *x) {\n    expose(x);\n    while(x->l) {\n      push(x);\n      x = x->l;\n\
    \    }\n    return x;\n  }\n \n  SUM &query(Node *t) {\n    expose(t);\n    return\
    \ t->sum;\n  }\n};\n"
  code: "template< typename SUM, typename KEY >\nstruct LinkCutTreeSubtree {\n \n\
    \  struct Node {\n    Node *l, *r, *p;\n \n    KEY key;\n    SUM sum;\n \n   \
    \ bool rev;\n    int sz;\n \n    bool is_root() const {\n      return !p || (p->l\
    \ != this && p->r != this);\n    }\n \n    Node(const KEY &key, const SUM &sum)\
    \ :\n        key(key), sum(sum), rev(false), sz(1),\n        l(nullptr), r(nullptr),\
    \ p(nullptr) {}\n  };\n \n  const SUM ident;\n \n  LinkCutTreeSubtree(const SUM\
    \ &ident) : ident(ident) {}\n \n  Node *make_node(const KEY &key) {\n    auto\
    \ ret = new Node(key, ident);\n    update(ret);\n    return ret;\n  }\n \n  Node\
    \ *set_key(Node *t, const KEY &key) {\n    expose(t);\n    t->key = key;\n   \
    \ update(t);\n    return t;\n  }\n \n  void toggle(Node *t) {\n    swap(t->l,\
    \ t->r);\n    t->sum.toggle();\n    t->rev ^= true;\n  }\n \n  void push(Node\
    \ *t) {\n    if(t->rev) {\n      if(t->l) toggle(t->l);\n      if(t->r) toggle(t->r);\n\
    \      t->rev = false;\n    }\n  }\n \n \n  void update(Node *t) {\n    t->sz\
    \ = 1;\n    if(t->l) t->sz += t->l->sz;\n    if(t->r) t->sz += t->r->sz;\n   \
    \ t->sum.merge(t->key, t->l ? t->l->sum : ident, t->r ? t->r->sum : ident);\n\
    \  }\n \n  void rotr(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->l\
    \ = t->r)) t->r->p = x;\n    t->r = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n \n  void rotl(Node *t) {\n    auto *x =\
    \ t->p, *y = x->p;\n    if((x->r = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n\
    \    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n\
    \      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n \n \n  void splay(Node\
    \ *t) {\n    push(t);\n    while(!t->is_root()) {\n      auto *q = t->p;\n   \
    \   if(q->is_root()) {\n        push(q), push(t);\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        auto *r = q->p;\n        push(r),\
    \ push(q), push(t);\n        if(r->l == q) {\n          if(q->l == t) rotr(q),\
    \ rotr(t);\n          else rotl(t), rotr(t);\n        } else {\n          if(q->r\
    \ == t) rotl(q), rotl(t);\n          else rotr(t), rotl(t);\n        }\n     \
    \ }\n    }\n  }\n \n \n  Node *expose(Node *t) {\n    Node *rp = nullptr;\n  \
    \  for(auto *cur = t; cur; cur = cur->p) {\n      splay(cur);\n      if(cur->r)\
    \ cur->sum.add(cur->r->sum);\n      cur->r = rp;\n      if(cur->r) cur->sum.erase(cur->r->sum);\n\
    \      update(cur);\n      rp = cur;\n    }\n    splay(t);\n    return rp;\n \
    \ }\n \n  void link(Node *child, Node *parent) {\n    expose(child);\n    expose(parent);\n\
    \    child->p = parent;\n    parent->r = child;\n    update(parent);\n  }\n \n\
    \  void cut(Node *child) {\n    expose(child);\n    auto *parent = child->l;\n\
    \    child->l = nullptr;\n    parent->p = nullptr;\n    update(child);\n  }\n\
    \ \n  void evert(Node *t) {\n    expose(t);\n    toggle(t);\n    push(t);\n  }\n\
    \ \n  Node *lca(Node *u, Node *v) {\n    if(get_root(u) != get_root(v)) return\
    \ nullptr;\n    expose(u);\n    return expose(v);\n  }\n \n \n  Node *get_kth(Node\
    \ *x, int k) {\n    expose(x);\n    while(x) {\n      push(x);\n      if(x->r\
    \ && x->r->sz > k) {\n        x = x->r;\n      } else {\n        if(x->r) k -=\
    \ x->r->sz;\n        if(k == 0) return x;\n        k -= 1;\n        x = x->l;\n\
    \      }\n    }\n    return nullptr;\n  }\n \n  Node *get_root(Node *x) {\n  \
    \  expose(x);\n    while(x->l) {\n      push(x);\n      x = x->l;\n    }\n   \
    \ return x;\n  }\n \n  SUM &query(Node *t) {\n    expose(t);\n    return t->sum;\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/link-cut-tree-subtree.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp
documentation_of: structure/others/link-cut-tree-subtree.cpp
layout: document
redirect_from:
- /library/structure/others/link-cut-tree-subtree.cpp
- /library/structure/others/link-cut-tree-subtree.cpp.html
title: structure/others/link-cut-tree-subtree.cpp
---
