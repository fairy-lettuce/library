---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-2450.test.cpp
    title: test/verify/aoj-2450.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-range-affine-range-sum.test.cpp
    title: test/verify/yosupo-range-affine-range-sum.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/lazy-segment-tree.md
    document_title: "Lazy-Segment-Tree(\u9045\u5EF6\u4F1D\u642C\u30BB\u30B0\u30E1\u30F3\
      \u30C8\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/segment-tree/lazy-segment-tree.cpp\"\n/**\n *\
    \ @brief Lazy-Segment-Tree(\u9045\u5EF6\u4F1D\u642C\u30BB\u30B0\u30E1\u30F3\u30C8\
    \u6728)\n * @docs docs/lazy-segment-tree.md\n */\ntemplate< typename Monoid, typename\
    \ OperatorMonoid, typename F, typename G, typename H >\nstruct LazySegmentTree\
    \ {\n  int sz, height;\n  vector< Monoid > data;\n  vector< OperatorMonoid > lazy;\n\
    \  const F f;\n  const G g;\n  const H h;\n  const Monoid M1;\n  const OperatorMonoid\
    \ OM0;\n\n  LazySegmentTree(int n, const F f, const G g, const H h,\n        \
    \          const Monoid &M1, const OperatorMonoid OM0)\n      : f(f), g(g), h(h),\
    \ M1(M1), OM0(OM0) {\n    sz = 1;\n    height = 0;\n    while(sz < n) sz <<= 1,\
    \ height++;\n    data.assign(2 * sz, M1);\n    lazy.assign(2 * sz, OM0);\n  }\n\
    \n  void set(int k, const Monoid &x) {\n    data[k + sz] = x;\n  }\n\n  void build()\
    \ {\n    for(int k = sz - 1; k > 0; k--) {\n      data[k] = f(data[2 * k + 0],\
    \ data[2 * k + 1]);\n    }\n  }\n\n  inline void propagate(int k) {\n    if(lazy[k]\
    \ != OM0) {\n      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);\n      lazy[2\
    \ * k + 1] = h(lazy[2 * k + 1], lazy[k]);\n      data[k] = apply(k);\n      lazy[k]\
    \ = OM0;\n    }\n  }\n\n  inline Monoid apply(int k) {\n    return lazy[k] ==\
    \ OM0 ? data[k] : g(data[k], lazy[k]);\n  }\n\n  inline void recalc(int k) {\n\
    \    while(k >>= 1) data[k] = f(apply(2 * k + 0), apply(2 * k + 1));\n  }\n\n\
    \  inline void thrust(int k) {\n    for(int i = height; i > 0; i--) propagate(k\
    \ >> i);\n  }\n\n  void update(int a, int b, const OperatorMonoid &x) {\n    if(a\
    \ >= b) return;\n    thrust(a += sz);\n    thrust(b += sz - 1);\n    for(int l\
    \ = a, r = b + 1; l < r; l >>= 1, r >>= 1) {\n      if(l & 1) lazy[l] = h(lazy[l],\
    \ x), ++l;\n      if(r & 1) --r, lazy[r] = h(lazy[r], x);\n    }\n    recalc(a);\n\
    \    recalc(b);\n  }\n\n  Monoid query(int a, int b) {\n    if(a >= b) return\
    \ M1;\n    thrust(a += sz);\n    thrust(b += sz - 1);\n    Monoid L = M1, R =\
    \ M1;\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1) {\n      if(l &\
    \ 1) L = f(L, apply(l++));\n      if(r & 1) R = f(apply(--r), R);\n    }\n   \
    \ return f(L, R);\n  }\n\n  Monoid operator[](const int &k) {\n    return query(k,\
    \ k + 1);\n  }\n\n  template< typename C >\n  int find_subtree(int a, const C\
    \ &check, Monoid &M, bool type) {\n    while(a < sz) {\n      propagate(a);\n\
    \      Monoid nxt = type ? f(apply(2 * a + type), M) : f(M, apply(2 * a + type));\n\
    \      if(check(nxt)) a = 2 * a + type;\n      else M = nxt, a = 2 * a + 1 - type;\n\
    \    }\n    return a - sz;\n  }\n\n  template< typename C >\n  int find_first(int\
    \ a, const C &check) {\n    Monoid L = M1;\n    if(a <= 0) {\n      if(check(f(L,\
    \ apply(1)))) return find_subtree(1, check, L, false);\n      return -1;\n   \
    \ }\n    thrust(a + sz);\n    int b = sz;\n    for(a += sz, b += sz; a < b; a\
    \ >>= 1, b >>= 1) {\n      if(a & 1) {\n        Monoid nxt = f(L, apply(a));\n\
    \        if(check(nxt)) return find_subtree(a, check, L, false);\n        L =\
    \ nxt;\n        ++a;\n      }\n    }\n    return -1;\n  }\n  \n  template< typename\
    \ C >\n  int find_last(int b, const C &check) {\n    Monoid R = M1;\n    if(b\
    \ >= sz) {\n      if(check(f(apply(1), R))) return find_subtree(1, check, R, true);\n\
    \      return -1;\n    }\n    thrust(b + sz - 1);\n    int a = sz;\n    for(b\
    \ += sz; a < b; a >>= 1, b >>= 1) {\n      if(b & 1) {\n        Monoid nxt = f(apply(--b),\
    \ R);\n        if(check(nxt)) return find_subtree(b, check, R, true);\n      \
    \  R = nxt;\n      }\n    }\n    return -1;\n  }\n};\n\ntemplate< typename Monoid,\
    \ typename OperatorMonoid, typename F, typename G, typename H >\nLazySegmentTree<\
    \ Monoid, OperatorMonoid, F, G, H > get_lazy_segment_tree\n    (int N, const F\
    \ &f, const G &g, const H &h, const Monoid &M1, const OperatorMonoid &OM0) {\n\
    \  return {N, f, g, h, M1, OM0};\n}\n"
  code: "/**\n * @brief Lazy-Segment-Tree(\u9045\u5EF6\u4F1D\u642C\u30BB\u30B0\u30E1\
    \u30F3\u30C8\u6728)\n * @docs docs/lazy-segment-tree.md\n */\ntemplate< typename\
    \ Monoid, typename OperatorMonoid, typename F, typename G, typename H >\nstruct\
    \ LazySegmentTree {\n  int sz, height;\n  vector< Monoid > data;\n  vector< OperatorMonoid\
    \ > lazy;\n  const F f;\n  const G g;\n  const H h;\n  const Monoid M1;\n  const\
    \ OperatorMonoid OM0;\n\n  LazySegmentTree(int n, const F f, const G g, const\
    \ H h,\n                  const Monoid &M1, const OperatorMonoid OM0)\n      :\
    \ f(f), g(g), h(h), M1(M1), OM0(OM0) {\n    sz = 1;\n    height = 0;\n    while(sz\
    \ < n) sz <<= 1, height++;\n    data.assign(2 * sz, M1);\n    lazy.assign(2 *\
    \ sz, OM0);\n  }\n\n  void set(int k, const Monoid &x) {\n    data[k + sz] = x;\n\
    \  }\n\n  void build() {\n    for(int k = sz - 1; k > 0; k--) {\n      data[k]\
    \ = f(data[2 * k + 0], data[2 * k + 1]);\n    }\n  }\n\n  inline void propagate(int\
    \ k) {\n    if(lazy[k] != OM0) {\n      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);\n\
    \      lazy[2 * k + 1] = h(lazy[2 * k + 1], lazy[k]);\n      data[k] = apply(k);\n\
    \      lazy[k] = OM0;\n    }\n  }\n\n  inline Monoid apply(int k) {\n    return\
    \ lazy[k] == OM0 ? data[k] : g(data[k], lazy[k]);\n  }\n\n  inline void recalc(int\
    \ k) {\n    while(k >>= 1) data[k] = f(apply(2 * k + 0), apply(2 * k + 1));\n\
    \  }\n\n  inline void thrust(int k) {\n    for(int i = height; i > 0; i--) propagate(k\
    \ >> i);\n  }\n\n  void update(int a, int b, const OperatorMonoid &x) {\n    if(a\
    \ >= b) return;\n    thrust(a += sz);\n    thrust(b += sz - 1);\n    for(int l\
    \ = a, r = b + 1; l < r; l >>= 1, r >>= 1) {\n      if(l & 1) lazy[l] = h(lazy[l],\
    \ x), ++l;\n      if(r & 1) --r, lazy[r] = h(lazy[r], x);\n    }\n    recalc(a);\n\
    \    recalc(b);\n  }\n\n  Monoid query(int a, int b) {\n    if(a >= b) return\
    \ M1;\n    thrust(a += sz);\n    thrust(b += sz - 1);\n    Monoid L = M1, R =\
    \ M1;\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1) {\n      if(l &\
    \ 1) L = f(L, apply(l++));\n      if(r & 1) R = f(apply(--r), R);\n    }\n   \
    \ return f(L, R);\n  }\n\n  Monoid operator[](const int &k) {\n    return query(k,\
    \ k + 1);\n  }\n\n  template< typename C >\n  int find_subtree(int a, const C\
    \ &check, Monoid &M, bool type) {\n    while(a < sz) {\n      propagate(a);\n\
    \      Monoid nxt = type ? f(apply(2 * a + type), M) : f(M, apply(2 * a + type));\n\
    \      if(check(nxt)) a = 2 * a + type;\n      else M = nxt, a = 2 * a + 1 - type;\n\
    \    }\n    return a - sz;\n  }\n\n  template< typename C >\n  int find_first(int\
    \ a, const C &check) {\n    Monoid L = M1;\n    if(a <= 0) {\n      if(check(f(L,\
    \ apply(1)))) return find_subtree(1, check, L, false);\n      return -1;\n   \
    \ }\n    thrust(a + sz);\n    int b = sz;\n    for(a += sz, b += sz; a < b; a\
    \ >>= 1, b >>= 1) {\n      if(a & 1) {\n        Monoid nxt = f(L, apply(a));\n\
    \        if(check(nxt)) return find_subtree(a, check, L, false);\n        L =\
    \ nxt;\n        ++a;\n      }\n    }\n    return -1;\n  }\n  \n  template< typename\
    \ C >\n  int find_last(int b, const C &check) {\n    Monoid R = M1;\n    if(b\
    \ >= sz) {\n      if(check(f(apply(1), R))) return find_subtree(1, check, R, true);\n\
    \      return -1;\n    }\n    thrust(b + sz - 1);\n    int a = sz;\n    for(b\
    \ += sz; a < b; a >>= 1, b >>= 1) {\n      if(b & 1) {\n        Monoid nxt = f(apply(--b),\
    \ R);\n        if(check(nxt)) return find_subtree(b, check, R, true);\n      \
    \  R = nxt;\n      }\n    }\n    return -1;\n  }\n};\n\ntemplate< typename Monoid,\
    \ typename OperatorMonoid, typename F, typename G, typename H >\nLazySegmentTree<\
    \ Monoid, OperatorMonoid, F, G, H > get_lazy_segment_tree\n    (int N, const F\
    \ &f, const G &g, const H &h, const Monoid &M1, const OperatorMonoid &OM0) {\n\
    \  return {N, f, g, h, M1, OM0};\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/lazy-segment-tree.cpp
  requiredBy: []
  timestamp: '2020-09-08 00:34:41+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-2450.test.cpp
  - test/verify/yosupo-range-affine-range-sum.test.cpp
documentation_of: structure/segment-tree/lazy-segment-tree.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/lazy-segment-tree.cpp
- /library/structure/segment-tree/lazy-segment-tree.cpp.html
title: "Lazy-Segment-Tree(\u9045\u5EF6\u4F1D\u642C\u30BB\u30B0\u30E1\u30F3\u30C8\u6728\
  )"
---
## 概要

遅延伝搬を用いることで, 区間に対する更新が可能になる. コンストラクタに対し追加で作用素モノイドの情報も与える.

## 使い方

* `LazySegmentTree(n, f, g, h, M1, OM0)`: サイズ `n` で初期化する. ここで `f` は2つの区間の要素をマージする二項演算, `g` は要素と作用素をマージする二項演算, `h` は作用素同士をマージする二項演算, `M1` はモノイドの単位元, `OM0` は作用素の単位元である.
* `set(k, x)`: `k` 番目の要素に `x` を代入する.
* `build()`: セグメント木を構築する.
* `query(a, b)`: 区間 $[a, b)$ に対して二項演算した結果を返す.
* `update(a, b, x)`: 区間 $[a, b)$ に対して作用素 `x` を適用する.
* `operator[k]`: `k` 番目の要素を返す.
* `find_first(a, check)`: $[a,x)$ が `check` を満たす最初の要素位置 $x$ を返す.
* `find_last(b, check)`: $[x,b)$ が `check` を満たす最後の要素位置 $x$ を返す.

`auto seg = get_lazy_segment_tree(N, f, g, h, M1, OM0);` のようにすると `decltype(f)` などを用いなくてすむ.

## 計算量

* `set(k, x)`: $O(1)$
* `build()`: $O(N)$
* クエリ: $O(\log N)$
