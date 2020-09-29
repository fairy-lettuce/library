---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-1508.test.cpp
    title: test/verify/aoj-1508.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/bbst/randomized-binary-search-tree.cpp\"\ntemplate<\
    \ typename T >\nclass RandomizedBinarySearchTree {\n\n  using F = function< T(T,\
    \ T) >;\n\nprivate:\n\n  struct Node {\n    Node *l, *r;\n    size_t cnt;\n  \
    \  T key, sum;\n\n    Node() = default;\n\n    Node(const T &k) : cnt(1), key(k),\
    \ sum(k), l(nullptr), r(nullptr) {}\n  };\n\n  inline int xor128() {\n    static\
    \ int x = 123456789;\n    static int y = 362436069;\n    static int z = 521288629;\n\
    \    static int w = 88675123;\n    int t;\n\n    t = x ^ (x << 11);\n    x = y;\n\
    \    y = z;\n    z = w;\n    return w = (w ^ (w >> 19)) ^ (t ^ (t >> 8));\n  }\n\
    \n  Node *build(int l, int r, const vector< T > &v) {\n    if(l + 1 >= r) return\
    \ alloc(v[l]);\n    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1,\
    \ r, v));\n  }\n\n  void dump(Node *t, typename vector< T >::iterator &it) const\
    \ {\n    if(!t) return;\n    dump(t->l, it);\n    *it = t->key;\n    dump(t->r,\
    \ ++it);\n  }\n\n  inline size_t count(const Node *t) const {\n    return t ?\
    \ t->cnt : 0;\n  }\n\n  inline T sum(const Node *t) const {\n    return t ? t->sum\
    \ : e;\n  }\n\n  inline Node *update(Node *t) {\n    t->cnt = count(t->l) + count(t->r)\
    \ + 1;\n    t->sum = f(f(sum(t->l), t->key), sum(t->r));\n    return t;\n  }\n\
    \n  vector< Node > pool;\n  int ptr;\n  const F f;\n  const T e;\n\npublic:\n\n\
    \  RandomizedBinarySearchTree(size_t sz, const F &f, const T &e) : pool(sz), f(f),\
    \ ptr(0), e(e) {}\n\n  inline Node *alloc(const T &v) {\n    return &(pool[ptr++]\
    \ = Node(v));\n  }\n\n  Node *merge(Node *l, Node *r) {\n    if(!l || !r) return\
    \ l ? l : r;\n    if(xor128() % (l->cnt + r->cnt) < l->cnt) {\n      l->r = merge(l->r,\
    \ r);\n      return update(l);\n    } else {\n      r->l = merge(l, r->l);\n \
    \     return update(r);\n    }\n  }\n\n  template< typename... Args >\n  Node\
    \ *merge(Node *p, Args... args) {\n    return merge(p, merge(args...));\n  }\n\
    \n  pair< Node *, Node * > split(Node *t, int k) {\n    if(!t) return {t, t};\n\
    \    if(k <= count(t->l)) {\n      auto s = split(t->l, k);\n      t->l = s.second;\n\
    \      return {s.first, update(t)};\n    } else {\n      auto s = split(t->r,\
    \ k - count(t->l) - 1);\n      t->r = s.first;\n      return {update(t), s.second};\n\
    \    }\n  }\n\n  Node *build(const vector< T > &v) {\n    ptr = 0;\n    return\
    \ build(0, (int) v.size(), v);\n  }\n\n  vector< T > dump(Node *t) const {\n \
    \   vector< T > v(count(t));\n    auto it = begin(v);\n    dump(t, it);\n    return\
    \ v;\n  }\n\n  string to_string(Node *r) {\n    auto s = dump(r);\n    string\
    \ ret;\n    for(int i = 0; i < s.size(); i++) ret += std::to_string(s[i]) + \"\
    , \";\n    return ret;\n  }\n\n  void insert(Node *&t, int k, const T &v) {\n\
    \    auto x = split(t, k);\n    t = merge(merge(x.first, alloc(v)), x.second);\n\
    \  }\n\n  void push_front(Node *&t, const T &v) {\n    t = merge(alloc(v), t);\n\
    \  }\n\n  void push_back(Node *&t, const T &v) {\n    t = merge(t, alloc(v));\n\
    \  }\n\n  T pop_front(Node *&t) {\n    auto ret = split(t, 1);\n    t = ret.second;\n\
    \    return ret.first->key;\n  }\n\n  T pop_back(Node *&t) {\n    auto ret = split(t,\
    \ count(t) - 1);\n    t = ret.first;\n    return ret.second->key;\n  }\n\n  void\
    \ erase(Node *&t, int k) {\n    auto x = split(t, k);\n    t = merge(x.first,\
    \ split(x.second, 1).second);\n  }\n\n  T query(Node *&t, int a, int b) {\n  \
    \  auto x = split(t, a);\n    auto y = split(x.second, b - a);\n    auto ret =\
    \ sum(y.first);\n    t = merge(x.first, merge(y.first, y.second));\n    return\
    \ ret;\n  }\n\n  tuple< Node *, Node *, Node * > split3(Node *t, int a, int b)\
    \ {\n    auto x = split(t, a);\n    auto y = split(x.second, b - a);\n    return\
    \ make_tuple(x.first, y.first, y.second);\n  }\n\n  void set_element(Node *&t,\
    \ int k, const T &x) {\n    if(k < count(t->l)) set_element(t->l, k, x);\n   \
    \ else if(k == count(t->l)) t->key = t->sum = x;\n    else set_element(t->r, k\
    \ - count(t->l) - 1, x);\n    t = update(t);\n  }\n\n  size_t size(Node *t) const\
    \ {\n    return count(t);\n  }\n\n  bool empty(Node *t) const {\n    return !t;\n\
    \  }\n};\n\n"
  code: "template< typename T >\nclass RandomizedBinarySearchTree {\n\n  using F =\
    \ function< T(T, T) >;\n\nprivate:\n\n  struct Node {\n    Node *l, *r;\n    size_t\
    \ cnt;\n    T key, sum;\n\n    Node() = default;\n\n    Node(const T &k) : cnt(1),\
    \ key(k), sum(k), l(nullptr), r(nullptr) {}\n  };\n\n  inline int xor128() {\n\
    \    static int x = 123456789;\n    static int y = 362436069;\n    static int\
    \ z = 521288629;\n    static int w = 88675123;\n    int t;\n\n    t = x ^ (x <<\
    \ 11);\n    x = y;\n    y = z;\n    z = w;\n    return w = (w ^ (w >> 19)) ^ (t\
    \ ^ (t >> 8));\n  }\n\n  Node *build(int l, int r, const vector< T > &v) {\n \
    \   if(l + 1 >= r) return alloc(v[l]);\n    return merge(build(l, (l + r) >> 1,\
    \ v), build((l + r) >> 1, r, v));\n  }\n\n  void dump(Node *t, typename vector<\
    \ T >::iterator &it) const {\n    if(!t) return;\n    dump(t->l, it);\n    *it\
    \ = t->key;\n    dump(t->r, ++it);\n  }\n\n  inline size_t count(const Node *t)\
    \ const {\n    return t ? t->cnt : 0;\n  }\n\n  inline T sum(const Node *t) const\
    \ {\n    return t ? t->sum : e;\n  }\n\n  inline Node *update(Node *t) {\n   \
    \ t->cnt = count(t->l) + count(t->r) + 1;\n    t->sum = f(f(sum(t->l), t->key),\
    \ sum(t->r));\n    return t;\n  }\n\n  vector< Node > pool;\n  int ptr;\n  const\
    \ F f;\n  const T e;\n\npublic:\n\n  RandomizedBinarySearchTree(size_t sz, const\
    \ F &f, const T &e) : pool(sz), f(f), ptr(0), e(e) {}\n\n  inline Node *alloc(const\
    \ T &v) {\n    return &(pool[ptr++] = Node(v));\n  }\n\n  Node *merge(Node *l,\
    \ Node *r) {\n    if(!l || !r) return l ? l : r;\n    if(xor128() % (l->cnt +\
    \ r->cnt) < l->cnt) {\n      l->r = merge(l->r, r);\n      return update(l);\n\
    \    } else {\n      r->l = merge(l, r->l);\n      return update(r);\n    }\n\
    \  }\n\n  template< typename... Args >\n  Node *merge(Node *p, Args... args) {\n\
    \    return merge(p, merge(args...));\n  }\n\n  pair< Node *, Node * > split(Node\
    \ *t, int k) {\n    if(!t) return {t, t};\n    if(k <= count(t->l)) {\n      auto\
    \ s = split(t->l, k);\n      t->l = s.second;\n      return {s.first, update(t)};\n\
    \    } else {\n      auto s = split(t->r, k - count(t->l) - 1);\n      t->r =\
    \ s.first;\n      return {update(t), s.second};\n    }\n  }\n\n  Node *build(const\
    \ vector< T > &v) {\n    ptr = 0;\n    return build(0, (int) v.size(), v);\n \
    \ }\n\n  vector< T > dump(Node *t) const {\n    vector< T > v(count(t));\n   \
    \ auto it = begin(v);\n    dump(t, it);\n    return v;\n  }\n\n  string to_string(Node\
    \ *r) {\n    auto s = dump(r);\n    string ret;\n    for(int i = 0; i < s.size();\
    \ i++) ret += std::to_string(s[i]) + \", \";\n    return ret;\n  }\n\n  void insert(Node\
    \ *&t, int k, const T &v) {\n    auto x = split(t, k);\n    t = merge(merge(x.first,\
    \ alloc(v)), x.second);\n  }\n\n  void push_front(Node *&t, const T &v) {\n  \
    \  t = merge(alloc(v), t);\n  }\n\n  void push_back(Node *&t, const T &v) {\n\
    \    t = merge(t, alloc(v));\n  }\n\n  T pop_front(Node *&t) {\n    auto ret =\
    \ split(t, 1);\n    t = ret.second;\n    return ret.first->key;\n  }\n\n  T pop_back(Node\
    \ *&t) {\n    auto ret = split(t, count(t) - 1);\n    t = ret.first;\n    return\
    \ ret.second->key;\n  }\n\n  void erase(Node *&t, int k) {\n    auto x = split(t,\
    \ k);\n    t = merge(x.first, split(x.second, 1).second);\n  }\n\n  T query(Node\
    \ *&t, int a, int b) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    auto ret = sum(y.first);\n    t = merge(x.first, merge(y.first,\
    \ y.second));\n    return ret;\n  }\n\n  tuple< Node *, Node *, Node * > split3(Node\
    \ *t, int a, int b) {\n    auto x = split(t, a);\n    auto y = split(x.second,\
    \ b - a);\n    return make_tuple(x.first, y.first, y.second);\n  }\n\n  void set_element(Node\
    \ *&t, int k, const T &x) {\n    if(k < count(t->l)) set_element(t->l, k, x);\n\
    \    else if(k == count(t->l)) t->key = t->sum = x;\n    else set_element(t->r,\
    \ k - count(t->l) - 1, x);\n    t = update(t);\n  }\n\n  size_t size(Node *t)\
    \ const {\n    return count(t);\n  }\n\n  bool empty(Node *t) const {\n    return\
    \ !t;\n  }\n};\n\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/randomized-binary-search-tree.cpp
  requiredBy: []
  timestamp: '2020-01-02 23:04:20+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-1508.test.cpp
documentation_of: structure/bbst/randomized-binary-search-tree.cpp
layout: document
redirect_from:
- /library/structure/bbst/randomized-binary-search-tree.cpp
- /library/structure/bbst/randomized-binary-search-tree.cpp.html
title: structure/bbst/randomized-binary-search-tree.cpp
---
