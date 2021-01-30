---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/convex-hull-trick/li-chao-tree.cpp\"\ntemplate<\
    \ typename T >\nstruct LiChaoTree {\n  struct Line {\n    T a, b;\n\n    Line(T\
    \ a, T b) : a(a), b(b) {}\n\n    inline T get(T x) const { return a * x + b; }\n\
    \n    inline bool over(const Line &b, const T &x) const {\n      return get(x)\
    \ < b.get(x);\n    }\n  };\n\n  vector< T > xs;\n  vector< Line > seg;\n  int\
    \ sz;\n\n  LiChaoTree(const vector< T > &x, T INF) : xs(x) {\n    sz = 1;\n  \
    \  while(sz < xs.size()) sz <<= 1;\n    while(xs.size() < sz) xs.push_back(xs.back()\
    \ + 1);\n    seg.assign(2 * sz - 1, Line(0, INF));\n  }\n\n  void update(Line\
    \ &x, int k, int l, int r) {\n    int mid = (l + r) >> 1;\n    auto latte = x.over(seg[k],\
    \ xs[l]), malta = x.over(seg[k], xs[mid]);\n    if(malta) swap(seg[k], x);\n \
    \   if(l + 1 >= r) return;\n    else if(latte != malta) update(x, 2 * k + 1, l,\
    \ mid);\n    else update(x, 2 * k + 2, mid, r);\n  }\n\n  void update(T a, T b)\
    \ { // ax+b\n    Line l(a, b);\n    update(l, 0, 0, sz);\n  }\n\n  T query(int\
    \ k) { // xs[k]\n    const T x = xs[k];\n    k += sz - 1;\n    T ret = seg[k].get(x);\n\
    \    while(k > 0) {\n      k = (k - 1) >> 1;\n      ret = min(ret, seg[k].get(x));\n\
    \    }\n    return ret;\n  }\n};\n"
  code: "template< typename T >\nstruct LiChaoTree {\n  struct Line {\n    T a, b;\n\
    \n    Line(T a, T b) : a(a), b(b) {}\n\n    inline T get(T x) const { return a\
    \ * x + b; }\n\n    inline bool over(const Line &b, const T &x) const {\n    \
    \  return get(x) < b.get(x);\n    }\n  };\n\n  vector< T > xs;\n  vector< Line\
    \ > seg;\n  int sz;\n\n  LiChaoTree(const vector< T > &x, T INF) : xs(x) {\n \
    \   sz = 1;\n    while(sz < xs.size()) sz <<= 1;\n    while(xs.size() < sz) xs.push_back(xs.back()\
    \ + 1);\n    seg.assign(2 * sz - 1, Line(0, INF));\n  }\n\n  void update(Line\
    \ &x, int k, int l, int r) {\n    int mid = (l + r) >> 1;\n    auto latte = x.over(seg[k],\
    \ xs[l]), malta = x.over(seg[k], xs[mid]);\n    if(malta) swap(seg[k], x);\n \
    \   if(l + 1 >= r) return;\n    else if(latte != malta) update(x, 2 * k + 1, l,\
    \ mid);\n    else update(x, 2 * k + 2, mid, r);\n  }\n\n  void update(T a, T b)\
    \ { // ax+b\n    Line l(a, b);\n    update(l, 0, 0, sz);\n  }\n\n  T query(int\
    \ k) { // xs[k]\n    const T x = xs[k];\n    k += sz - 1;\n    T ret = seg[k].get(x);\n\
    \    while(k > 0) {\n      k = (k - 1) >> 1;\n      ret = min(ret, seg[k].get(x));\n\
    \    }\n    return ret;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/convex-hull-trick/li-chao-tree.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/convex-hull-trick/li-chao-tree.cpp
layout: document
redirect_from:
- /library/structure/convex-hull-trick/li-chao-tree.cpp
- /library/structure/convex-hull-trick/li-chao-tree.cpp.html
title: structure/convex-hull-trick/li-chao-tree.cpp
---
