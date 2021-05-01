---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2450-3.test.cpp
    title: test/verify/aoj-2450-3.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-point-set-range-composite-3.test.cpp
    title: test/verify/yosupo-point-set-range-composite-3.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Splay-Tree-Base(Splay\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/develop/splay-tree-base.cpp\"\n/**\n * @brief\
    \ Splay-Tree-Base(Splay\u6728)\n */\ntemplate< typename Node >\nstruct SplayTreeBase\
    \ {\npublic:\n  bool is_root(Node *t) const {\n    return !t->p || (t->p->l !=\
    \ t && t->p->r != t);\n  }\n\n  inline size_t count(Node *t) const { return t\
    \ ? t->sz : 0; }\n\n  void splay(Node *t) {\n    push(t);\n    while(!is_root(t))\
    \ {\n      auto *q = t->p;\n      if(!is_root(t)) {\n        push(q), push(t);\n\
    \        if(q->l == t) rotr(t);\n        else rotl(t);\n      } else {\n     \
    \   auto *r = q->p;\n        push(r), push(q), push(t);\n        if(r->l == q)\
    \ {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t), rotr(t);\n\
    \        } else {\n          if(q->r == t) rotl(q), rotl(t);\n          else rotr(t),\
    \ rotl(t);\n        }\n      }\n    }\n  }\n\n  Node *erase(Node *t) {\n    splay(t);\n\
    \    Node *x = t->l, *y = t->r;\n    delete t;\n    if(!x) {\n      t = y;\n \
    \     if(t) t->p = nullptr;\n    } else if(!y) {\n      t = x;\n      t->p = nullptr;\n\
    \    } else {\n      x->p = nullptr;\n      t = get_right(x);\n      splay(t);\n\
    \      t->r = y;\n      y->p = t;\n    }\n    return t;\n  }\n\n  Node *get_left(Node\
    \ *t) const {\n    while(t->l) t = t->l;\n    return t;\n  }\n\n  Node *get_right(Node\
    \ *t) const {\n    while(t->r) t = t->r;\n    return t;\n  }\n\n  pair< Node *,\
    \ Node * > split(Node *t, int k) {\n    if(!t) return {nullptr, nullptr};\n  \
    \  push(t);\n    if(k <= count(t->l)) {\n      auto x = split(t->l, k);\n    \
    \  t->l = x.second;\n      t->p = nullptr;\n      if(x.second) x.second->p = t;\n\
    \      return {x.first, update(t)};\n    } else {\n      auto x = split(t->r,\
    \ k - count(t->l) - 1);\n      t->r = x.first;\n      t->p = nullptr;\n      if(x.first)\
    \ x.first->p = t;\n      return {update(t), x.second};\n    }\n  }\n\n  template<\
    \ typename ... Args >\n  Node *merge(Node *l, Args ...rest) {\n    Node *r = merge(rest...);\n\
    \    if(!l && !r) return nullptr;\n    if(!l) return splay(r), r;\n    if(!r)\
    \ return splay(l), l;\n    splay(l), splay(r);\n    l = get_right(l);\n    splay(l);\n\
    \    l->r = r;\n    r->p = l;\n    update(l);\n    return l;\n  }\n\n  tuple<\
    \ Node *, Node *, Node * > split3(Node *t, int a, int b) {\n    splay(t);\n  \
    \  auto x = split(t, a);\n    auto y = split(x.second, b - a);\n    return make_tuple(x.first,\
    \ y.first, y.second);\n  }\n\n  virtual void push(Node *t) = 0;\n\n  virtual Node\
    \ *update(Node *t) = 0;\n\nprivate:\n\n  void rotr(Node *t) {\n    auto *x = t->p,\
    \ *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n    t->r = x, x->p = t;\n  \
    \  update(x), update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n\
    \      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\n  void rotl(Node\
    \ *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r = t->l)) t->l->p = x;\n\
    \    t->l = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n  \
    \    if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n\
    \    }\n  }\n\nprotected:\n\n  Node *merge(Node *l) {\n    return l;\n  }\n\n\
    \  Node *build_node(const vector< Node * > &v) {\n    return build_node(0, v.size(),\
    \ v);\n  }\n\n  Node *build_node(int l, int r, const vector< Node * > &v) {\n\
    \    if(l + 1 >= r) return v[l];\n    return merge(build_node(l, (l + r) >> 1,\
    \ v), build_node((l + r) >> 1, r, v));\n  }\n\n  Node *push_front_node(Node *t,\
    \ Node *z) {\n    if(!t) {\n      return z;\n    } else {\n      splay(t);\n \
    \     Node *cur = get_left(t);\n      splay(cur);\n      z->p = cur;\n      cur->l\
    \ = z;\n      splay(z);\n      return z;\n    }\n  }\n\n  Node *push_back_node(Node\
    \ *t, Node *z) {\n    if(!t) {\n      return z;\n    } else {\n      splay(t);\n\
    \      Node *cur = get_right(t);\n      splay(cur);\n      z->p = cur;\n     \
    \ cur->r = z;\n      splay(z);\n      return z;\n    }\n  }\n\n  void insert_node(Node\
    \ *&t, int k, Node *v) {\n    splay(t);\n    auto x = split(t, k);\n    t = merge(merge(x.first,\
    \ v), x.second);\n  }\n\n  void erase_node(Node *&t, int k) {\n    splay(t);\n\
    \    auto x = split(t, k);\n    auto y = split(x.second, 1);\n    delete y.first;\n\
    \    t = merge(x.first, y.second);\n  }\n};\n"
  code: "/**\n * @brief Splay-Tree-Base(Splay\u6728)\n */\ntemplate< typename Node\
    \ >\nstruct SplayTreeBase {\npublic:\n  bool is_root(Node *t) const {\n    return\
    \ !t->p || (t->p->l != t && t->p->r != t);\n  }\n\n  inline size_t count(Node\
    \ *t) const { return t ? t->sz : 0; }\n\n  void splay(Node *t) {\n    push(t);\n\
    \    while(!is_root(t)) {\n      auto *q = t->p;\n      if(!is_root(t)) {\n  \
    \      push(q), push(t);\n        if(q->l == t) rotr(t);\n        else rotl(t);\n\
    \      } else {\n        auto *r = q->p;\n        push(r), push(q), push(t);\n\
    \        if(r->l == q) {\n          if(q->l == t) rotr(q), rotr(t);\n        \
    \  else rotl(t), rotr(t);\n        } else {\n          if(q->r == t) rotl(q),\
    \ rotl(t);\n          else rotr(t), rotl(t);\n        }\n      }\n    }\n  }\n\
    \n  Node *erase(Node *t) {\n    splay(t);\n    Node *x = t->l, *y = t->r;\n  \
    \  delete t;\n    if(!x) {\n      t = y;\n      if(t) t->p = nullptr;\n    } else\
    \ if(!y) {\n      t = x;\n      t->p = nullptr;\n    } else {\n      x->p = nullptr;\n\
    \      t = get_right(x);\n      splay(t);\n      t->r = y;\n      y->p = t;\n\
    \    }\n    return t;\n  }\n\n  Node *get_left(Node *t) const {\n    while(t->l)\
    \ t = t->l;\n    return t;\n  }\n\n  Node *get_right(Node *t) const {\n    while(t->r)\
    \ t = t->r;\n    return t;\n  }\n\n  pair< Node *, Node * > split(Node *t, int\
    \ k) {\n    if(!t) return {nullptr, nullptr};\n    push(t);\n    if(k <= count(t->l))\
    \ {\n      auto x = split(t->l, k);\n      t->l = x.second;\n      t->p = nullptr;\n\
    \      if(x.second) x.second->p = t;\n      return {x.first, update(t)};\n   \
    \ } else {\n      auto x = split(t->r, k - count(t->l) - 1);\n      t->r = x.first;\n\
    \      t->p = nullptr;\n      if(x.first) x.first->p = t;\n      return {update(t),\
    \ x.second};\n    }\n  }\n\n  template< typename ... Args >\n  Node *merge(Node\
    \ *l, Args ...rest) {\n    Node *r = merge(rest...);\n    if(!l && !r) return\
    \ nullptr;\n    if(!l) return splay(r), r;\n    if(!r) return splay(l), l;\n \
    \   splay(l), splay(r);\n    l = get_right(l);\n    splay(l);\n    l->r = r;\n\
    \    r->p = l;\n    update(l);\n    return l;\n  }\n\n  tuple< Node *, Node *,\
    \ Node * > split3(Node *t, int a, int b) {\n    splay(t);\n    auto x = split(t,\
    \ a);\n    auto y = split(x.second, b - a);\n    return make_tuple(x.first, y.first,\
    \ y.second);\n  }\n\n  virtual void push(Node *t) = 0;\n\n  virtual Node *update(Node\
    \ *t) = 0;\n\nprivate:\n\n  void rotr(Node *t) {\n    auto *x = t->p, *y = x->p;\n\
    \    if((x->l = t->r)) t->r->p = x;\n    t->r = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n  void rotl(Node *t) {\n    auto *x =\
    \ t->p, *y = x->p;\n    if((x->r = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n\
    \    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n\
    \      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\nprotected:\n\n\
    \  Node *merge(Node *l) {\n    return l;\n  }\n\n  Node *build_node(const vector<\
    \ Node * > &v) {\n    return build_node(0, v.size(), v);\n  }\n\n  Node *build_node(int\
    \ l, int r, const vector< Node * > &v) {\n    if(l + 1 >= r) return v[l];\n  \
    \  return merge(build_node(l, (l + r) >> 1, v), build_node((l + r) >> 1, r, v));\n\
    \  }\n\n  Node *push_front_node(Node *t, Node *z) {\n    if(!t) {\n      return\
    \ z;\n    } else {\n      splay(t);\n      Node *cur = get_left(t);\n      splay(cur);\n\
    \      z->p = cur;\n      cur->l = z;\n      splay(z);\n      return z;\n    }\n\
    \  }\n\n  Node *push_back_node(Node *t, Node *z) {\n    if(!t) {\n      return\
    \ z;\n    } else {\n      splay(t);\n      Node *cur = get_right(t);\n      splay(cur);\n\
    \      z->p = cur;\n      cur->r = z;\n      splay(z);\n      return z;\n    }\n\
    \  }\n\n  void insert_node(Node *&t, int k, Node *v) {\n    splay(t);\n    auto\
    \ x = split(t, k);\n    t = merge(merge(x.first, v), x.second);\n  }\n\n  void\
    \ erase_node(Node *&t, int k) {\n    splay(t);\n    auto x = split(t, k);\n  \
    \  auto y = split(x.second, 1);\n    delete y.first;\n    t = merge(x.first, y.second);\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/develop/splay-tree-base.cpp
  requiredBy: []
  timestamp: '2020-08-29 03:56:51+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-2450-3.test.cpp
  - test/verify/yosupo-dynamic-tree-vertex-add-path-sum-2.test.cpp
  - test/verify/yosupo-point-set-range-composite-3.test.cpp
  - test/verify/yosupo-dynamic-tree-vertex-set-path-composite-2.test.cpp
documentation_of: structure/develop/splay-tree-base.cpp
layout: document
redirect_from:
- /library/structure/develop/splay-tree-base.cpp
- /library/structure/develop/splay-tree-base.cpp.html
title: "Splay-Tree-Base(Splay\u6728)"
---
