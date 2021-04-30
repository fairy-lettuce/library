---
data:
  _extendedDependsOn:
  - icon: ':x:'
    path: structure/develop/splay-tree.cpp
    title: structure/develop/splay-tree.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-5-a-2.test.cpp
    title: test/verify/aoj-grl-5-a-2.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/develop/splay-tree.cpp\"\ntemplate< typename key_t,\
    \ size_t V >\nstruct SplayTree {\n\n  const key_t e;\n\n  SplayTree() : pool(),\
    \ e(key_t()) {}\n\n  struct Node {\n    Node *l, *r, *p;\n    key_t sum;\n\n \
    \   Node() = default;\n\n    explicit Node(const key_t &k) : sum(k), l(nullptr),\
    \ r(nullptr), p(nullptr) {}\n  };\n\n  ArrayPool< Node, V > pool;\n\nprivate:\n\
    \  void rotr(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->l = t->r))\
    \ t->r->p = x;\n    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p\
    \ = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n    \
    \  update(y);\n    }\n  }\n\n  void rotl(Node *t) {\n    auto *x = t->p, *y =\
    \ x->p;\n    if((x->r = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x),\
    \ update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r\
    \ == x) y->r = t;\n      update(y);\n    }\n  }\n\n  void update(Node *t) {\n\
    \    t->sum.set_sum();\n    if(t->l) t->sum.update(t->l->sum);\n    if(t->r) t->sum.update(t->r->sum);\n\
    \  }\n\n  Node *get_right(Node *t) const {\n    while(t->r) t = t->r;\n    return\
    \ t;\n  }\n\n  inline Node *alloc(const key_t &v) {\n    auto p = &(*pool.alloc()\
    \ = Node(v));\n    update(p);\n    return p;\n  }\n\n  void splay(Node *t) {\n\
    \    while(t->p) {\n      auto *q = t->p;\n      if(!q->p) {\n        if(q->l\
    \ == t) rotr(t);\n        else rotl(t);\n      } else {\n        auto *r = q->p;\n\
    \        if(r->l == q) {\n          if(q->l == t) rotr(q), rotr(t);\n        \
    \  else rotl(t), rotr(t);\n        } else {\n          if(q->r == t) rotl(q),\
    \ rotl(t);\n          else rotr(t), rotl(t);\n        }\n      }\n    }\n  }\n\
    \npublic:\n  inline const key_t &sum(Node *t) {\n    return t ? t->sum : e;\n\
    \  }\n\n  Node *push_back(Node *t, const key_t &v) {\n    if(!t) {\n      t =\
    \ alloc(v);\n      return t;\n    } else {\n      Node *cur = get_right(t), *z\
    \ = alloc(v);\n      z->p = cur;\n      cur->r = z;\n      update(cur);\n    \
    \  splay(z);\n      return z;\n    }\n  }\n\n  Node *erase(Node *t) {\n    splay(t);\n\
    \    Node *x = t->l, *y = t->r;\n    pool.free(t);\n    if(!x) {\n      t = y;\n\
    \      if(t) t->p = nullptr;\n    } else if(!y) {\n      t = x;\n      t->p =\
    \ nullptr;\n    } else {\n      x->p = nullptr;\n      t = get_right(x);\n   \
    \   splay(t);\n      t->r = y;\n      y->p = t;\n      update(t);\n    }\n   \
    \ return t;\n  }\n};\n#line 2 \"structure/develop/link-cut-tree-subtree.cpp\"\n\
    \ntemplate< typename T, size_t V >\nstruct LinkCutTreeSubTree {\n  using key_t\
    \ = typename T::key_t;\n  using heavy_t = typename T::heavy_t;\n  using light_t\
    \ = typename T::light_t;\n\n  struct Node {\n    Node *l, *r, *p;\n\n    typename\
    \ SplayTree< light_t, V >::Node *light, *belong;\n    heavy_t sum;\n\n    Node()\
    \ = default;\n\n    bool is_root() const {\n      return !p || (p->l != this &&\
    \ p->r != this);\n    }\n\n    Node(const key_t &key) :\n        belong(nullptr),\
    \ l(nullptr), r(nullptr), p(nullptr), light(nullptr) {\n      sum.set_key(key);\n\
    \    }\n  };\n\n  using ST = SplayTree< light_t, V >;\n\n  ST st;\n  const heavy_t\
    \ ident;\n  ArrayPool< Node, V > pool;\n\n  LinkCutTreeSubTree() : ident(heavy_t()),\
    \ st(), pool() {}\n\n  Node *alloc(const key_t &key) {\n    auto ret = &(*pool.alloc()\
    \ = Node(key));\n    update(ret);\n    return ret;\n  }\n\n  Node *set_key(Node\
    \ *t, const key_t &key) {\n    expose(t);\n    t->sum.set_key(key);\n    update(t);\n\
    \    return t;\n  }\n\n  void update(Node *t) {\n    t->sum.update(t->l ? t->l->sum\
    \ : ident, t->r ? t->r->sum : ident, st.sum(t->light));\n  }\n\n  void rotr(Node\
    \ *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n\
    \    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n  \
    \    if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n\
    \    }\n  }\n\n  void rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r\
    \ = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n\n  void splay(Node *t) {\n\n    Node\
    \ *rot = t;\n    while(!rot->is_root()) rot = rot->p;\n    t->belong = rot->belong;\n\
    \    if(t != rot) rot->belong = nullptr;\n\n    while(!t->is_root()) {\n     \
    \ auto *q = t->p;\n      if(q->is_root()) {\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        auto *r = q->p;\n        if(r->l\
    \ == q) {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t),\
    \ rotr(t);\n        } else {\n          if(q->r == t) rotl(q), rotl(t);\n    \
    \      else rotr(t), rotl(t);\n        }\n      }\n    }\n\n  }\n\n\n  Node *expose(Node\
    \ *t) {\n    Node *rp = nullptr;\n    for(auto *cur = t; cur; cur = cur->p) {\n\
    \      splay(cur);\n      if(cur->r) {\n        cur->light = st.push_back(cur->light,\
    \ cur->r->sum.add());\n        cur->r->belong = cur->light;\n      }\n      cur->r\
    \ = rp;\n      if(cur->r) {\n        cur->light = st.erase(cur->r->belong);\n\
    \      }\n      update(cur);\n      rp = cur;\n    }\n    splay(t);\n    return\
    \ rp;\n  }\n\n  void link(Node *child, Node *parent) {\n    expose(child);\n \
    \   expose(parent);\n    child->p = parent;\n    parent->r = child;\n    update(parent);\n\
    \  }\n\n  void cut(Node *child) {\n    expose(child);\n    auto *parent = child->l;\n\
    \    child->l = nullptr;\n    parent->p = nullptr;\n    update(child);\n  }\n\n\
    \  Node *lca(Node *u, Node *v) {\n    if(get_root(u) != get_root(v)) return nullptr;\n\
    \    expose(u);\n    return expose(v);\n  }\n\n  Node *get_root(Node *x) {\n \
    \   expose(x);\n    while(x->l) {\n      push(x);\n      x = x->l;\n    }\n  \
    \  return x;\n  }\n};\n"
  code: "#include \"splay-tree.cpp\"\n\ntemplate< typename T, size_t V >\nstruct LinkCutTreeSubTree\
    \ {\n  using key_t = typename T::key_t;\n  using heavy_t = typename T::heavy_t;\n\
    \  using light_t = typename T::light_t;\n\n  struct Node {\n    Node *l, *r, *p;\n\
    \n    typename SplayTree< light_t, V >::Node *light, *belong;\n    heavy_t sum;\n\
    \n    Node() = default;\n\n    bool is_root() const {\n      return !p || (p->l\
    \ != this && p->r != this);\n    }\n\n    Node(const key_t &key) :\n        belong(nullptr),\
    \ l(nullptr), r(nullptr), p(nullptr), light(nullptr) {\n      sum.set_key(key);\n\
    \    }\n  };\n\n  using ST = SplayTree< light_t, V >;\n\n  ST st;\n  const heavy_t\
    \ ident;\n  ArrayPool< Node, V > pool;\n\n  LinkCutTreeSubTree() : ident(heavy_t()),\
    \ st(), pool() {}\n\n  Node *alloc(const key_t &key) {\n    auto ret = &(*pool.alloc()\
    \ = Node(key));\n    update(ret);\n    return ret;\n  }\n\n  Node *set_key(Node\
    \ *t, const key_t &key) {\n    expose(t);\n    t->sum.set_key(key);\n    update(t);\n\
    \    return t;\n  }\n\n  void update(Node *t) {\n    t->sum.update(t->l ? t->l->sum\
    \ : ident, t->r ? t->r->sum : ident, st.sum(t->light));\n  }\n\n  void rotr(Node\
    \ *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n\
    \    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n  \
    \    if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n\
    \    }\n  }\n\n  void rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r\
    \ = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n\n  void splay(Node *t) {\n\n    Node\
    \ *rot = t;\n    while(!rot->is_root()) rot = rot->p;\n    t->belong = rot->belong;\n\
    \    if(t != rot) rot->belong = nullptr;\n\n    while(!t->is_root()) {\n     \
    \ auto *q = t->p;\n      if(q->is_root()) {\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        auto *r = q->p;\n        if(r->l\
    \ == q) {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t),\
    \ rotr(t);\n        } else {\n          if(q->r == t) rotl(q), rotl(t);\n    \
    \      else rotr(t), rotl(t);\n        }\n      }\n    }\n\n  }\n\n\n  Node *expose(Node\
    \ *t) {\n    Node *rp = nullptr;\n    for(auto *cur = t; cur; cur = cur->p) {\n\
    \      splay(cur);\n      if(cur->r) {\n        cur->light = st.push_back(cur->light,\
    \ cur->r->sum.add());\n        cur->r->belong = cur->light;\n      }\n      cur->r\
    \ = rp;\n      if(cur->r) {\n        cur->light = st.erase(cur->r->belong);\n\
    \      }\n      update(cur);\n      rp = cur;\n    }\n    splay(t);\n    return\
    \ rp;\n  }\n\n  void link(Node *child, Node *parent) {\n    expose(child);\n \
    \   expose(parent);\n    child->p = parent;\n    parent->r = child;\n    update(parent);\n\
    \  }\n\n  void cut(Node *child) {\n    expose(child);\n    auto *parent = child->l;\n\
    \    child->l = nullptr;\n    parent->p = nullptr;\n    update(child);\n  }\n\n\
    \  Node *lca(Node *u, Node *v) {\n    if(get_root(u) != get_root(v)) return nullptr;\n\
    \    expose(u);\n    return expose(v);\n  }\n\n  Node *get_root(Node *x) {\n \
    \   expose(x);\n    while(x->l) {\n      push(x);\n      x = x->l;\n    }\n  \
    \  return x;\n  }\n};\n"
  dependsOn:
  - structure/develop/splay-tree.cpp
  isVerificationFile: false
  path: structure/develop/link-cut-tree-subtree.cpp
  requiredBy: []
  timestamp: '2020-11-04 13:55:57+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-5-a-2.test.cpp
documentation_of: structure/develop/link-cut-tree-subtree.cpp
layout: document
redirect_from:
- /library/structure/develop/link-cut-tree-subtree.cpp
- /library/structure/develop/link-cut-tree-subtree.cpp.html
title: structure/develop/link-cut-tree-subtree.cpp
---
