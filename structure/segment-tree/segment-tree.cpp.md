---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dsl-2-a.test.cpp
    title: test/verify/aoj-dsl-2-a.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yukicoder-650.test.cpp
    title: test/verify/yukicoder-650.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/segment-tree.md
    document_title: "Segment Tree(\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)"
    links: []
  bundledCode: "#line 1 \"structure/segment-tree/segment-tree.cpp\"\n/**\n * @brief\
    \ Segment Tree(\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)\n * @docs docs/segment-tree.md\n\
    \ */\ntemplate< typename Monoid, typename F >\nstruct SegmentTree {\n  int n,\
    \ sz;\n  vector< Monoid > seg;\n\n  const F f;\n  const Monoid M1;\n  \n  SegmentTree(int\
    \ n, const F f, const Monoid &M1) : n(n), f(f), M1(M1) {\n    sz = 1;\n    while(sz\
    \ < n) sz <<= 1;\n    seg.assign(2 * sz, M1);\n  }\n\n  void set(int k, const\
    \ Monoid &x) {\n    seg[k + sz] = x;\n  }\n\n  void build() {\n    for(int k =\
    \ sz - 1; k > 0; k--) {\n      seg[k] = f(seg[2 * k + 0], seg[2 * k + 1]);\n \
    \   }\n  }\n\n  void update(int k, const Monoid &x) {\n    k += sz;\n    seg[k]\
    \ = x;\n    while(k >>= 1) {\n      seg[k] = f(seg[2 * k + 0], seg[2 * k + 1]);\n\
    \    }\n  }\n\n  Monoid prod(int a, int b) {\n    Monoid L = M1, R = M1;\n   \
    \ for(a += sz, b += sz; a < b; a >>= 1, b >>= 1) {\n      if(a & 1) L = f(L, seg[a++]);\n\
    \      if(b & 1) R = f(seg[--b], R);\n    }\n    return f(L, R);\n  }\n\n  Monoid\
    \ all_prod() {\n    return seg[1];\n  }\n\n  Monoid operator[](const int &k) const\
    \ {\n    return seg[k + sz];\n  }\n\n  template< typename C >\n  int find_subtree(int\
    \ a, const C &check, Monoid &M, bool type) {\n    while(a < sz) {\n      Monoid\
    \ nxt = type ? f(seg[2 * a + type], M) : f(M, seg[2 * a + type]);\n      if(check(nxt))\
    \ a = 2 * a + type;\n      else M = nxt, a = 2 * a + 1 - type;\n    }\n    return\
    \ a - sz;\n  }\n\n  template< typename C >\n  int find_first(int a, const C &check)\
    \ {\n    Monoid L = M1;\n    if(a <= 0) {\n      if(check(f(L, seg[1]))) return\
    \ find_subtree(1, check, L, false);\n      return n;\n    }\n    int b = sz;\n\
    \    for(a += sz, b += sz; a < b; a >>= 1, b >>= 1) {\n      if(a & 1) {\n   \
    \     Monoid nxt = f(L, seg[a]);\n        if(check(nxt)) return find_subtree(a,\
    \ check, L, false);\n        L = nxt;\n        ++a;\n      }\n    }\n    return\
    \ n;\n  }\n\n  template< typename C >\n  int find_last(int b, const C &check)\
    \ {\n    Monoid R = M1;\n    if(b >= sz) {\n      if(check(f(seg[1], R))) return\
    \ find_subtree(1, check, R, true);\n      return -1;\n    }\n    int a = sz;\n\
    \    for(b += sz; a < b; a >>= 1, b >>= 1) {\n      if(b & 1) {\n        Monoid\
    \ nxt = f(seg[--b], R);\n        if(check(nxt)) return find_subtree(b, check,\
    \ R, true);\n        R = nxt;\n      }\n    }\n    return -1;\n  }\n};\n\ntemplate<\
    \ typename Monoid, typename F >\nSegmentTree< Monoid, F > get_segment_tree(int\
    \ N, const F& f, const Monoid& M1) {\n  return {N, f, M1};\n}\n"
  code: "/**\n * @brief Segment Tree(\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)\n * @docs\
    \ docs/segment-tree.md\n */\ntemplate< typename Monoid, typename F >\nstruct SegmentTree\
    \ {\n  int n, sz;\n  vector< Monoid > seg;\n\n  const F f;\n  const Monoid M1;\n\
    \  \n  SegmentTree(int n, const F f, const Monoid &M1) : n(n), f(f), M1(M1) {\n\
    \    sz = 1;\n    while(sz < n) sz <<= 1;\n    seg.assign(2 * sz, M1);\n  }\n\n\
    \  void set(int k, const Monoid &x) {\n    seg[k + sz] = x;\n  }\n\n  void build()\
    \ {\n    for(int k = sz - 1; k > 0; k--) {\n      seg[k] = f(seg[2 * k + 0], seg[2\
    \ * k + 1]);\n    }\n  }\n\n  void update(int k, const Monoid &x) {\n    k +=\
    \ sz;\n    seg[k] = x;\n    while(k >>= 1) {\n      seg[k] = f(seg[2 * k + 0],\
    \ seg[2 * k + 1]);\n    }\n  }\n\n  Monoid prod(int a, int b) {\n    Monoid L\
    \ = M1, R = M1;\n    for(a += sz, b += sz; a < b; a >>= 1, b >>= 1) {\n      if(a\
    \ & 1) L = f(L, seg[a++]);\n      if(b & 1) R = f(seg[--b], R);\n    }\n    return\
    \ f(L, R);\n  }\n\n  Monoid all_prod() {\n    return seg[1];\n  }\n\n  Monoid\
    \ operator[](const int &k) const {\n    return seg[k + sz];\n  }\n\n  template<\
    \ typename C >\n  int find_subtree(int a, const C &check, Monoid &M, bool type)\
    \ {\n    while(a < sz) {\n      Monoid nxt = type ? f(seg[2 * a + type], M) :\
    \ f(M, seg[2 * a + type]);\n      if(check(nxt)) a = 2 * a + type;\n      else\
    \ M = nxt, a = 2 * a + 1 - type;\n    }\n    return a - sz;\n  }\n\n  template<\
    \ typename C >\n  int find_first(int a, const C &check) {\n    Monoid L = M1;\n\
    \    if(a <= 0) {\n      if(check(f(L, seg[1]))) return find_subtree(1, check,\
    \ L, false);\n      return n;\n    }\n    int b = sz;\n    for(a += sz, b += sz;\
    \ a < b; a >>= 1, b >>= 1) {\n      if(a & 1) {\n        Monoid nxt = f(L, seg[a]);\n\
    \        if(check(nxt)) return find_subtree(a, check, L, false);\n        L =\
    \ nxt;\n        ++a;\n      }\n    }\n    return n;\n  }\n\n  template< typename\
    \ C >\n  int find_last(int b, const C &check) {\n    Monoid R = M1;\n    if(b\
    \ >= sz) {\n      if(check(f(seg[1], R))) return find_subtree(1, check, R, true);\n\
    \      return -1;\n    }\n    int a = sz;\n    for(b += sz; a < b; a >>= 1, b\
    \ >>= 1) {\n      if(b & 1) {\n        Monoid nxt = f(seg[--b], R);\n        if(check(nxt))\
    \ return find_subtree(b, check, R, true);\n        R = nxt;\n      }\n    }\n\
    \    return -1;\n  }\n};\n\ntemplate< typename Monoid, typename F >\nSegmentTree<\
    \ Monoid, F > get_segment_tree(int N, const F& f, const Monoid& M1) {\n  return\
    \ {N, f, M1};\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/segment-tree.cpp
  requiredBy: []
  timestamp: '2021-08-28 02:59:12+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yukicoder-650.test.cpp
  - test/verify/aoj-dsl-2-a.test.cpp
documentation_of: structure/segment-tree/segment-tree.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/segment-tree.cpp
- /library/structure/segment-tree/segment-tree.cpp.html
title: "Segment Tree(\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)"
---
## 概要

完全二分木である. モノイドについて区間に対する演算が $O(\log N)$ で処理できる.

モノイドは次の条件を満たす代数的構造である.

* 結合律を満たす. つまり $S$ の各元 $a, b, c$ に対して, $(a \cdot b) \cdot c = a \cdot (b \cdot c)$ が満たされる.
* 単位元をもつ. つまり $S$ の任意の元 $a$ をとってきたときに $a \cdot e = e \cdot a = a$ なる $e$ が存在する.

実装では木を 1-indexed の配列で表現している. ノード $k$ について, 親ノードは $\frac k 2$, 子ノードは $2k$, $2k+1$ である.

## 使い方

* `SegmentTree(n, f, M1)`: サイズ `n` で初期化する. ここで `f` は2つの区間の要素をマージする二項演算, `M1` はモノイドの単位元である. $O(n)$
* `set(k, x)`: `k` 番目の要素に `x` を代入する. $O(1)$
* `build()`: セグメント木を構築する. $O(n)$
* `prod(a, b)`: 区間 $[a, b)$ に対して二項演算した結果を返す. $O(\log n)$
* `all_prod()`: 全体を二項演算した結果を返す. $O(1)$
* `update(k, x)`: `k` 番目の要素を `x` に変更する. $O(\log n)$
* `operator[k]`: `k` 番目の要素を返す. $O(1)$
* `find_first(a, check)`: $[a, x)$ が `check` を満たす最初の要素位置 $x$ を返す. 存在しないとき $n$ を返す. $O(\log n)$
* `find_last(b, check)`: $[x, b)$ が `check` を満たす最後の要素位置 $x$ を返す. 存在しないとき $-1$ を返す. $(\log n)$
