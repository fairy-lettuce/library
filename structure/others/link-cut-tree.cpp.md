---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2450-2.test.cpp
    title: test/verify/aoj-2450-2.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-dynamic-tree-vertex-add-path-sum.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-add-path-sum.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp
    title: test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':question:'
  attributes:
    document_title: Link-Cut-Tree
    links: []
  bundledCode: "#line 1 \"structure/others/link-cut-tree.cpp\"\n/**\n * @brief Link-Cut-Tree\n\
    \ */\ntemplate< template< typename, typename > typename ST, typename Monoid =\
    \ int, typename OperatorMonoid = Monoid >\nstruct LinkCutTree : ST< Monoid, OperatorMonoid\
    \ > {\n  using LST = ST< Monoid, OperatorMonoid >;\n  using ST< Monoid, OperatorMonoid\
    \ >::ST;\n  using Node = typename LST::Node;\n\n  Node *expose(Node *t) {\n  \
    \  Node *rp = nullptr;\n    for(Node *cur = t; cur; cur = cur->p) {\n      this->splay(cur);\n\
    \      cur->r = rp;\n      this->update(cur);\n      rp = cur;\n    }\n    this->splay(t);\n\
    \    return rp;\n  }\n\n  void link(Node *child, Node *parent) {\n    expose(child);\n\
    \    expose(parent);\n    child->p = parent;\n    parent->r = child;\n    this->update(parent);\n\
    \  }\n\n  void cut(Node *child) {\n    expose(child);\n    auto *parent = child->l;\n\
    \    child->l = nullptr;\n    parent->p = nullptr;\n    this->update(child);\n\
    \  }\n\n  void evert(Node *t) {\n    expose(t);\n    this->toggle(t);\n    this->push(t);\n\
    \  }\n\n  Node *lca(Node *u, Node *v) {\n    if(get_root(u) != get_root(v)) return\
    \ nullptr;\n    expose(u);\n    return expose(v);\n  }\n\n  void set_propagate(Node\
    \ *t, const OperatorMonoid &x) {\n    expose(t);\n    LST::set_propagate(t, x);\n\
    \  }\n\n  Node *get_kth(Node *x, int k) {\n    expose(x);\n    while(x) {\n  \
    \    this->push(x);\n      if(x->r && x->r->sz > k) {\n        x = x->r;\n   \
    \   } else {\n        if(x->r) k -= x->r->sz;\n        if(k == 0) return x;\n\
    \        k -= 1;\n        x = x->l;\n      }\n    }\n    return nullptr;\n  }\n\
    \n  Node *get_root(Node *x) {\n    expose(x);\n    while(x->l) {\n      this->push(x);\n\
    \      x = x->l;\n    }\n    return x;\n  }\n\n  const Monoid &query(Node *t)\
    \ {\n    expose(t);\n    return t->sum;\n  }\n};\n"
  code: "/**\n * @brief Link-Cut-Tree\n */\ntemplate< template< typename, typename\
    \ > typename ST, typename Monoid = int, typename OperatorMonoid = Monoid >\nstruct\
    \ LinkCutTree : ST< Monoid, OperatorMonoid > {\n  using LST = ST< Monoid, OperatorMonoid\
    \ >;\n  using ST< Monoid, OperatorMonoid >::ST;\n  using Node = typename LST::Node;\n\
    \n  Node *expose(Node *t) {\n    Node *rp = nullptr;\n    for(Node *cur = t; cur;\
    \ cur = cur->p) {\n      this->splay(cur);\n      cur->r = rp;\n      this->update(cur);\n\
    \      rp = cur;\n    }\n    this->splay(t);\n    return rp;\n  }\n\n  void link(Node\
    \ *child, Node *parent) {\n    expose(child);\n    expose(parent);\n    child->p\
    \ = parent;\n    parent->r = child;\n    this->update(parent);\n  }\n\n  void\
    \ cut(Node *child) {\n    expose(child);\n    auto *parent = child->l;\n    child->l\
    \ = nullptr;\n    parent->p = nullptr;\n    this->update(child);\n  }\n\n  void\
    \ evert(Node *t) {\n    expose(t);\n    this->toggle(t);\n    this->push(t);\n\
    \  }\n\n  Node *lca(Node *u, Node *v) {\n    if(get_root(u) != get_root(v)) return\
    \ nullptr;\n    expose(u);\n    return expose(v);\n  }\n\n  void set_propagate(Node\
    \ *t, const OperatorMonoid &x) {\n    expose(t);\n    LST::set_propagate(t, x);\n\
    \  }\n\n  Node *get_kth(Node *x, int k) {\n    expose(x);\n    while(x) {\n  \
    \    this->push(x);\n      if(x->r && x->r->sz > k) {\n        x = x->r;\n   \
    \   } else {\n        if(x->r) k -= x->r->sz;\n        if(k == 0) return x;\n\
    \        k -= 1;\n        x = x->l;\n      }\n    }\n    return nullptr;\n  }\n\
    \n  Node *get_root(Node *x) {\n    expose(x);\n    while(x->l) {\n      this->push(x);\n\
    \      x = x->l;\n    }\n    return x;\n  }\n\n  const Monoid &query(Node *t)\
    \ {\n    expose(t);\n    return t->sum;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/link-cut-tree.cpp
  requiredBy: []
  timestamp: '2020-06-19 01:29:44+09:00'
  verificationStatus: LIBRARY_SOME_WA
  verifiedWith:
  - test/verify/yosupo-dynamic-tree-vertex-add-path-sum.test.cpp
  - test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp
  - test/verify/aoj-2450-2.test.cpp
documentation_of: structure/others/link-cut-tree.cpp
layout: document
redirect_from:
- /library/structure/others/link-cut-tree.cpp
- /library/structure/others/link-cut-tree.cpp.html
title: Link-Cut-Tree
---
