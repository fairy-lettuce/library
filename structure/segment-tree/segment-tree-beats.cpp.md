---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"structure/segment-tree/segment-tree-beats.cpp\"\ntemplate<\
    \ typename Monoid, typename OperatorMonoid = Monoid >\nstruct SegmentTreeBeats\
    \ {\n  using F = function< Monoid(Monoid, Monoid) >;\n  using G = function< Monoid(Monoid,\
    \ OperatorMonoid) >;\n  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid)\
    \ >;\n\n  int sz, height;\n  vector< Monoid > data;\n  vector< OperatorMonoid\
    \ > lazy;\n  const F f;\n  const G g;\n  const H h;\n  const Monoid M1;\n  const\
    \ OperatorMonoid OM0;\n\n\n  SegmentTreeBeats(int n, const F f, const G g, const\
    \ H h,\n                   const Monoid &M1, const OperatorMonoid OM0)\n     \
    \ : f(f), g(g), h(h), M1(M1), OM0(OM0) {\n    sz = 1;\n    height = 0;\n    while(sz\
    \ < n) sz <<= 1, height++;\n    data.assign(2 * sz, M1);\n    lazy.assign(2 *\
    \ sz, OM0);\n  }\n\n  void set(int k, const Monoid &x) {\n    data[k + sz] = x;\n\
    \  }\n\n  void build() {\n    for(int k = sz - 1; k > 0; k--) {\n      data[k]\
    \ = f(data[2 * k + 0], data[2 * k + 1]);\n    }\n  }\n\n  inline void propagate(int\
    \ k) {\n    if(lazy[k] != OM0) {\n      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);\n\
    \      lazy[2 * k + 1] = h(lazy[2 * k + 1], lazy[k]);\n      data[k] = reflect(k);\n\
    \      lazy[k] = OM0;\n    }\n  }\n\n  inline Monoid reflect(int k) {\n    return\
    \ lazy[k] == OM0 ? data[k] : g(data[k], lazy[k]);\n  }\n\n  inline void recalc(int\
    \ k) {\n    while(k >>= 1) data[k] = f(reflect(2 * k + 0), reflect(2 * k + 1));\n\
    \  }\n\n  inline void thrust(int k) {\n    for(int i = height; i > 0; i--) propagate(k\
    \ >> i);\n  }\n\n  void update(int a, int b, const OperatorMonoid &x) {\n    thrust(a\
    \ += sz);\n    thrust(b += sz - 1);\n    for(int l = a, r = b + 1; l < r; l >>=\
    \ 1, r >>= 1) {\n      if(l & 1) lazy[l] = h(lazy[l], x), ++l;\n      if(r & 1)\
    \ --r, lazy[r] = h(lazy[r], x);\n    }\n    recalc(a);\n    recalc(b);\n  }\n\n\
    \  Monoid query(int a, int b) {\n    thrust(a += sz);\n    thrust(b += sz - 1);\n\
    \    Monoid L = M1, R = M1;\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>=\
    \ 1) {\n      if(l & 1) L = f(L, reflect(l++));\n      if(r & 1) R = f(reflect(--r),\
    \ R);\n    }\n    return f(L, R);\n  }\n\n  Monoid operator[](const int &k) {\n\
    \    return query(k, k + 1);\n  }\n\n  template< typename Uku, typename Check,\
    \ typename Func, typename X >\n  void update_beats_subtree(int k, const X &x,\
    \ const Uku &uku, const Check &check, const Func &func) {\n    if(k >= sz) {\n\
    \      auto v = reflect(k);\n      if(uku(v, x)) return;\n      if(check(v)) lazy[k]\
    \ = func(v, x);\n      return;\n    }\n    propagate(k);\n    if(uku(data[k],\
    \ x)) return;\n    if(check(data[k])) {\n      lazy[k] = func(data[k], x);\n \
    \     return;\n    }\n    update_beats_subtree(k * 2 + 0, x, uku, check, func);\n\
    \    update_beats_subtree(k * 2 + 1, x, uku, check, func);\n    data[k] = f(reflect(2\
    \ * k + 0), reflect(2 * k + 1));\n  }\n\n  template< typename Uku, typename Check,\
    \ typename Func, typename X >\n  void update_beats(int a, int b, const X &x, const\
    \ Uku &uku, const Check &check, const Func &func) {\n    thrust(a += sz);\n  \
    \  thrust(b += sz - 1);\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1)\
    \ {\n      if(l & 1) update_beats_subtree(l++, x, uku, check, func);\n      if(r\
    \ & 1) update_beats_subtree(--r, x, uku, check, func);\n    }\n    recalc(a);\n\
    \    recalc(b);\n  }\n};\n"
  code: "template< typename Monoid, typename OperatorMonoid = Monoid >\nstruct SegmentTreeBeats\
    \ {\n  using F = function< Monoid(Monoid, Monoid) >;\n  using G = function< Monoid(Monoid,\
    \ OperatorMonoid) >;\n  using H = function< OperatorMonoid(OperatorMonoid, OperatorMonoid)\
    \ >;\n\n  int sz, height;\n  vector< Monoid > data;\n  vector< OperatorMonoid\
    \ > lazy;\n  const F f;\n  const G g;\n  const H h;\n  const Monoid M1;\n  const\
    \ OperatorMonoid OM0;\n\n\n  SegmentTreeBeats(int n, const F f, const G g, const\
    \ H h,\n                   const Monoid &M1, const OperatorMonoid OM0)\n     \
    \ : f(f), g(g), h(h), M1(M1), OM0(OM0) {\n    sz = 1;\n    height = 0;\n    while(sz\
    \ < n) sz <<= 1, height++;\n    data.assign(2 * sz, M1);\n    lazy.assign(2 *\
    \ sz, OM0);\n  }\n\n  void set(int k, const Monoid &x) {\n    data[k + sz] = x;\n\
    \  }\n\n  void build() {\n    for(int k = sz - 1; k > 0; k--) {\n      data[k]\
    \ = f(data[2 * k + 0], data[2 * k + 1]);\n    }\n  }\n\n  inline void propagate(int\
    \ k) {\n    if(lazy[k] != OM0) {\n      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);\n\
    \      lazy[2 * k + 1] = h(lazy[2 * k + 1], lazy[k]);\n      data[k] = reflect(k);\n\
    \      lazy[k] = OM0;\n    }\n  }\n\n  inline Monoid reflect(int k) {\n    return\
    \ lazy[k] == OM0 ? data[k] : g(data[k], lazy[k]);\n  }\n\n  inline void recalc(int\
    \ k) {\n    while(k >>= 1) data[k] = f(reflect(2 * k + 0), reflect(2 * k + 1));\n\
    \  }\n\n  inline void thrust(int k) {\n    for(int i = height; i > 0; i--) propagate(k\
    \ >> i);\n  }\n\n  void update(int a, int b, const OperatorMonoid &x) {\n    thrust(a\
    \ += sz);\n    thrust(b += sz - 1);\n    for(int l = a, r = b + 1; l < r; l >>=\
    \ 1, r >>= 1) {\n      if(l & 1) lazy[l] = h(lazy[l], x), ++l;\n      if(r & 1)\
    \ --r, lazy[r] = h(lazy[r], x);\n    }\n    recalc(a);\n    recalc(b);\n  }\n\n\
    \  Monoid query(int a, int b) {\n    thrust(a += sz);\n    thrust(b += sz - 1);\n\
    \    Monoid L = M1, R = M1;\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>=\
    \ 1) {\n      if(l & 1) L = f(L, reflect(l++));\n      if(r & 1) R = f(reflect(--r),\
    \ R);\n    }\n    return f(L, R);\n  }\n\n  Monoid operator[](const int &k) {\n\
    \    return query(k, k + 1);\n  }\n\n  template< typename Uku, typename Check,\
    \ typename Func, typename X >\n  void update_beats_subtree(int k, const X &x,\
    \ const Uku &uku, const Check &check, const Func &func) {\n    if(k >= sz) {\n\
    \      auto v = reflect(k);\n      if(uku(v, x)) return;\n      if(check(v)) lazy[k]\
    \ = func(v, x);\n      return;\n    }\n    propagate(k);\n    if(uku(data[k],\
    \ x)) return;\n    if(check(data[k])) {\n      lazy[k] = func(data[k], x);\n \
    \     return;\n    }\n    update_beats_subtree(k * 2 + 0, x, uku, check, func);\n\
    \    update_beats_subtree(k * 2 + 1, x, uku, check, func);\n    data[k] = f(reflect(2\
    \ * k + 0), reflect(2 * k + 1));\n  }\n\n  template< typename Uku, typename Check,\
    \ typename Func, typename X >\n  void update_beats(int a, int b, const X &x, const\
    \ Uku &uku, const Check &check, const Func &func) {\n    thrust(a += sz);\n  \
    \  thrust(b += sz - 1);\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1)\
    \ {\n      if(l & 1) update_beats_subtree(l++, x, uku, check, func);\n      if(r\
    \ & 1) update_beats_subtree(--r, x, uku, check, func);\n    }\n    recalc(a);\n\
    \    recalc(b);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/segment-tree-beats.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/segment-tree/segment-tree-beats.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/segment-tree-beats.cpp
- /library/structure/segment-tree/segment-tree-beats.cpp.html
title: structure/segment-tree/segment-tree-beats.cpp
---
