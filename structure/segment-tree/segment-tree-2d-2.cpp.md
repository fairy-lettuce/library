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
  bundledCode: "#line 1 \"structure/segment-tree/segment-tree-2d-2.cpp\"\ntemplate<\
    \ typename structure_t, typename get_t, typename update_t >\nstruct SegmentTree2D\
    \ {\n  using merge_f = function< get_t(get_t, get_t) >;\n  using get_t = function<\
    \ get_t(structure_t &, int) >;\n  using range_update_f = function< get_t(structure_t\
    \ &, int, int, update_t) >;\n\n  int sz;\n  vector< structure_t > seg;\n  const\
    \ merge_f &f;\n  const get_t &g;\n  const range_update_f &h;\n\n  SegmentTree2D(int\
    \ n, const merge_f &f, const get_t &g, const range_update_f &h) : f(f), g(g),\
    \ h(h) {\n    sz = 1;\n    while(sz < n) sz <<= 1;\n    seg.resize(2 * sz - 1);\n\
    \  }\n\n  void update(int a, int b, int lower, int upper, update_t x, int k, int\
    \ l, int r) {\n    if(r <= a || b <= l) {\n      return;\n    } else if(a <= l\
    \ && r <= b) {\n      g(seg[k], lower, upper, x);\n    } else {\n      update(a,\
    \ b, lower, upper, x, 2 * k + 1, l, (l + r) >> 1);\n      update(a, b, lower,\
    \ upper, x, 2 * k + 2, (l + r) >> 1, r);\n    }\n  }\n\n  void update(int a, int\
    \ b, int l, int r, update_t x) {\n    update(a, b, l, r, x, 0, 0, sz);\n  }\n\n\
    \  get_t get(int x, int y) {\n    x += sz - 1;\n    get_t ret = g(seg[x], y);\n\
    \    while(x > 0) {\n      x = (x - 1) >> 1;\n      ret = f(ret, g(seg[x], y));\n\
    \    }\n  }\n};\n"
  code: "template< typename structure_t, typename get_t, typename update_t >\nstruct\
    \ SegmentTree2D {\n  using merge_f = function< get_t(get_t, get_t) >;\n  using\
    \ get_t = function< get_t(structure_t &, int) >;\n  using range_update_f = function<\
    \ get_t(structure_t &, int, int, update_t) >;\n\n  int sz;\n  vector< structure_t\
    \ > seg;\n  const merge_f &f;\n  const get_t &g;\n  const range_update_f &h;\n\
    \n  SegmentTree2D(int n, const merge_f &f, const get_t &g, const range_update_f\
    \ &h) : f(f), g(g), h(h) {\n    sz = 1;\n    while(sz < n) sz <<= 1;\n    seg.resize(2\
    \ * sz - 1);\n  }\n\n  void update(int a, int b, int lower, int upper, update_t\
    \ x, int k, int l, int r) {\n    if(r <= a || b <= l) {\n      return;\n    }\
    \ else if(a <= l && r <= b) {\n      g(seg[k], lower, upper, x);\n    } else {\n\
    \      update(a, b, lower, upper, x, 2 * k + 1, l, (l + r) >> 1);\n      update(a,\
    \ b, lower, upper, x, 2 * k + 2, (l + r) >> 1, r);\n    }\n  }\n\n  void update(int\
    \ a, int b, int l, int r, update_t x) {\n    update(a, b, l, r, x, 0, 0, sz);\n\
    \  }\n\n  get_t get(int x, int y) {\n    x += sz - 1;\n    get_t ret = g(seg[x],\
    \ y);\n    while(x > 0) {\n      x = (x - 1) >> 1;\n      ret = f(ret, g(seg[x],\
    \ y));\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/segment-tree-2d-2.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/segment-tree/segment-tree-2d-2.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/segment-tree-2d-2.cpp
- /library/structure/segment-tree/segment-tree-2d-2.cpp.html
title: structure/segment-tree/segment-tree-2d-2.cpp
---
