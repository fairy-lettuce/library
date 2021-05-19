---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: Euler-Tour-Tree
    links: []
  bundledCode: "#line 1 \"structure/lct/euler-tour-tree.cpp\"\n/**\n * @brief Euler-Tour-Tree\n\
    \ */\ntemplate< typename T >\nstruct EulerTourTree {\n\nprivate:\n\n  struct Node\
    \ {\n    Node *l, *r, *p;\n    size_t sz;\n\n    explicit Node() : sz(1), l(nullptr),\
    \ r(nullptr), p(nullptr) {}\n\n    bool is_root() const {\n      return not p\
    \ or (p->l != this and p->r != this);\n    }\n  };\n\n  using NP = Node *;\n\n\
    \  NP update(NP t) {\n    t->sz = 1;\n    if(t->l) t->sz += t->l->sz;\n    if(t->r)\
    \ t->sz += t->r->sz;\n    return t;\n  }\n\n  void rotr(NP t) {\n    NP x = t->p,\
    \ y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n    t->r = x, x->p = t;\n   \
    \ update(x), update(t);\n    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n\
    \      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\n  void rotl(NP\
    \ t) {\n    NP x = t->p, y = x->p;\n    if((x->r = t->l)) t->l->p = x;\n    t->l\
    \ = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l\
    \ == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\
    \n  void splay(NP t) {\n    while(not t->is_root()) {\n      NP q = t->p;\n  \
    \    if(q->is_root()) {\n        if(q->l == t) rotr(t);\n        else rotl(t);\n\
    \      } else {\n        NP r = q->p;\n        if(r->l == q) {\n          if(q->l\
    \ == t) rotr(q), rotr(t);\n          else rotl(t), rotr(t);\n        } else {\n\
    \          if(q->r == t) rotl(q), rotl(t);\n          else rotr(t), rotl(t);\n\
    \        }\n      }\n    }\n  }\n\n  NP splay_front(NP t) {\n    splay(t);\n \
    \   while(t->l) t = t->l;\n    splay(t);\n    return t;\n  }\n\n  NP splay_back(NP\
    \ t) {\n    splay(t);\n    while(t->r) t = t->r;\n    splay(t);\n    return t;\n\
    \  }\n\n  template< typename... Args >\n  NP merge(NP p, Args... args) {\n   \
    \ return merge(p, merge(args...));\n  }\n\n  NP merge(NP l, NP r) {\n    if(!l\
    \ && !r) return nullptr;\n    if(!l) return splay(r), r;\n    if(!r) return splay(l),\
    \ l;\n    splay(l), splay(r);\n    l = splay_back(l);\n    l->r = r;\n    r->p\
    \ = l;\n    update(l);\n    return l;\n  }\n\n\n  NP alloc() {\n    return new\
    \ Node();\n  }\n\n  NP reroot(NP t) {\n    splay(t);\n    NP l = t->l;\n    if(not\
    \ l) return t;\n    t->l = nullptr;\n    update(t);\n    return merge(l, t);\n\
    \  }\n\n  NP link(NP u, NP v, NP e1, NP e2) {\n    u = reroot(u);\n    v = reroot(v);\n\
    \    return merge(u, e1, v, e2);\n  }\n\n  NP cut(NP e1, NP e2) {\n    splay(e1);\n\
    \    splay(e2);\n    NP p = e1->p;\n    bool is_r;\n    if(p != e2) {\n      is_r\
    \ = p == e2->r;\n      p->p = nullptr;\n      if(e1 == p->l) rotr(e1);\n     \
    \ else rotl(e1);\n    } else {\n      is_r = e1 == e2->r;\n    }\n    if(e1->l)\
    \ {\n      e1->l->p = nullptr;\n    }\n    if(e1->r) {\n      e1->r->p = nullptr;\n\
    \    }\n    if(is_r) {\n      if(e2->l) e2->l->p = nullptr;\n      return merge(e2->l,\
    \ e1->r);\n    } else {\n      if(e2->r) e2->r->p = nullptr;\n      return merge(e1->l,\
    \ e2->r);\n    }\n  }\n\n  bool is_connected(NP u, NP v) {\n    splay(u);\n  \
    \  splay(v);\n    return u->p != nullptr;\n  }\n\n  vector< unordered_map< int,\
    \ NP > > ptr;\n\n  NP get_node(int l, int r) {\n    if(ptr[l].find(r)) {\n   \
    \   ptr[l][r] = alloc();\n    }\n    return ptr[l][r];\n  }\n\npublic:\n  EulerTourTree()\
    \ = default;\n\n  explicit EulerTourTree(int n) : ptr(n) {}\n\n  void reroot(int\
    \ k) {\n    reroot(get_node(k, k));\n  }\n\n  void link(int u, int v) {\n    ptr[u][v]\
    \ = alloc();\n    ptr[v][u] = alloc();\n    link(get_node(u, u), get_node(v, v),\
    \ ptr[u][v], ptr[v][u]);\n  }\n\n  void cut(int u, int v) {\n    auto it1 = ptr[u].find(v);\n\
    \    auto it2 = ptr[v].find(u);\n    cut(it1, it2);\n    ptr[u].erase(it1);\n\
    \    ptr[v].erase(it2);\n  }\n\n  bool is_conneced(int u, int v) {\n    return\
    \ is_connected(get_node(u, u), get_node(v, v));\n  }\n};\n"
  code: "/**\n * @brief Euler-Tour-Tree\n */\ntemplate< typename T >\nstruct EulerTourTree\
    \ {\n\nprivate:\n\n  struct Node {\n    Node *l, *r, *p;\n    size_t sz;\n\n \
    \   explicit Node() : sz(1), l(nullptr), r(nullptr), p(nullptr) {}\n\n    bool\
    \ is_root() const {\n      return not p or (p->l != this and p->r != this);\n\
    \    }\n  };\n\n  using NP = Node *;\n\n  NP update(NP t) {\n    t->sz = 1;\n\
    \    if(t->l) t->sz += t->l->sz;\n    if(t->r) t->sz += t->r->sz;\n    return\
    \ t;\n  }\n\n  void rotr(NP t) {\n    NP x = t->p, y = x->p;\n    if((x->l = t->r))\
    \ t->r->p = x;\n    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p\
    \ = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n    \
    \  update(y);\n    }\n  }\n\n  void rotl(NP t) {\n    NP x = t->p, y = x->p;\n\
    \    if((x->r = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n  void splay(NP t) {\n    while(not t->is_root())\
    \ {\n      NP q = t->p;\n      if(q->is_root()) {\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        NP r = q->p;\n        if(r->l\
    \ == q) {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t),\
    \ rotr(t);\n        } else {\n          if(q->r == t) rotl(q), rotl(t);\n    \
    \      else rotr(t), rotl(t);\n        }\n      }\n    }\n  }\n\n  NP splay_front(NP\
    \ t) {\n    splay(t);\n    while(t->l) t = t->l;\n    splay(t);\n    return t;\n\
    \  }\n\n  NP splay_back(NP t) {\n    splay(t);\n    while(t->r) t = t->r;\n  \
    \  splay(t);\n    return t;\n  }\n\n  template< typename... Args >\n  NP merge(NP\
    \ p, Args... args) {\n    return merge(p, merge(args...));\n  }\n\n  NP merge(NP\
    \ l, NP r) {\n    if(!l && !r) return nullptr;\n    if(!l) return splay(r), r;\n\
    \    if(!r) return splay(l), l;\n    splay(l), splay(r);\n    l = splay_back(l);\n\
    \    l->r = r;\n    r->p = l;\n    update(l);\n    return l;\n  }\n\n\n  NP alloc()\
    \ {\n    return new Node();\n  }\n\n  NP reroot(NP t) {\n    splay(t);\n    NP\
    \ l = t->l;\n    if(not l) return t;\n    t->l = nullptr;\n    update(t);\n  \
    \  return merge(l, t);\n  }\n\n  NP link(NP u, NP v, NP e1, NP e2) {\n    u =\
    \ reroot(u);\n    v = reroot(v);\n    return merge(u, e1, v, e2);\n  }\n\n  NP\
    \ cut(NP e1, NP e2) {\n    splay(e1);\n    splay(e2);\n    NP p = e1->p;\n   \
    \ bool is_r;\n    if(p != e2) {\n      is_r = p == e2->r;\n      p->p = nullptr;\n\
    \      if(e1 == p->l) rotr(e1);\n      else rotl(e1);\n    } else {\n      is_r\
    \ = e1 == e2->r;\n    }\n    if(e1->l) {\n      e1->l->p = nullptr;\n    }\n \
    \   if(e1->r) {\n      e1->r->p = nullptr;\n    }\n    if(is_r) {\n      if(e2->l)\
    \ e2->l->p = nullptr;\n      return merge(e2->l, e1->r);\n    } else {\n     \
    \ if(e2->r) e2->r->p = nullptr;\n      return merge(e1->l, e2->r);\n    }\n  }\n\
    \n  bool is_connected(NP u, NP v) {\n    splay(u);\n    splay(v);\n    return\
    \ u->p != nullptr;\n  }\n\n  vector< unordered_map< int, NP > > ptr;\n\n  NP get_node(int\
    \ l, int r) {\n    if(ptr[l].find(r)) {\n      ptr[l][r] = alloc();\n    }\n \
    \   return ptr[l][r];\n  }\n\npublic:\n  EulerTourTree() = default;\n\n  explicit\
    \ EulerTourTree(int n) : ptr(n) {}\n\n  void reroot(int k) {\n    reroot(get_node(k,\
    \ k));\n  }\n\n  void link(int u, int v) {\n    ptr[u][v] = alloc();\n    ptr[v][u]\
    \ = alloc();\n    link(get_node(u, u), get_node(v, v), ptr[u][v], ptr[v][u]);\n\
    \  }\n\n  void cut(int u, int v) {\n    auto it1 = ptr[u].find(v);\n    auto it2\
    \ = ptr[v].find(u);\n    cut(it1, it2);\n    ptr[u].erase(it1);\n    ptr[v].erase(it2);\n\
    \  }\n\n  bool is_conneced(int u, int v) {\n    return is_connected(get_node(u,\
    \ u), get_node(v, v));\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/lct/euler-tour-tree.cpp
  requiredBy: []
  timestamp: '2021-05-19 22:08:50+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/lct/euler-tour-tree.cpp
layout: document
redirect_from:
- /library/structure/lct/euler-tour-tree.cpp
- /library/structure/lct/euler-tour-tree.cpp.html
title: Euler-Tour-Tree
---
