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
  bundledCode: "#line 1 \"structure/segment-tree/segment-tree-2d.cpp\"\ntemplate<\
    \ typename structure_t, typename get_t, typename update_t >\nstruct SegmentTree2DCompressed\
    \ {\n\n  using merge_f = function< get_t(get_t, get_t) >;\n  using range_get_f\
    \ = function< get_t(structure_t &, int, int) >;\n  using update_f = function<\
    \ void(structure_t &, int, update_t) >;\n\n  int sz;\n  vector< structure_t >\
    \ seg;\n  const merge_f f;\n  const range_get_f g;\n  const update_f h;\n  const\
    \ get_t identity;\n  vector< vector< int > > LL, RR;\n  vector< vector< int >\
    \ > beet;\n\n  SegmentTree2DCompressed(int n, const merge_f &f, const range_get_f\
    \ &g, const update_f &h, const get_t &identity)\n      : f(f), g(g), h(h), identity(identity)\
    \ {\n    sz = 1;\n    while(sz < n) sz <<= 1;\n    beet.resize(2 * sz);\n    LL.resize(2\
    \ * sz);\n    RR.resize(2 * sz);\n  }\n\n  void update(int a, int x, update_t\
    \ z, int k, int l, int r) {\n    if(r <= a || a + 1 <= l) return;\n    if(a <=\
    \ l && r <= a + 1) return h(seg[k], x, z);\n    update(a, LL[k][x], z, 2 * k +\
    \ 0, l, (l + r) >> 1);\n    update(a, RR[k][x], z, 2 * k + 1, (l + r) >> 1, r);\n\
    \    return h(seg[k], x, z);\n  }\n\n  void update(int x, int y, update_t z) {\n\
    \    y = lower_bound(begin(beet[1]), end(beet[1]), y) - begin(beet[1]);\n    return\
    \ update(x, y, z, 1, 0, sz);\n  }\n\n  get_t query(int a, int b, int x, int y,\
    \ int k, int l, int r) {\n    if(a >= r || b <= l) return identity;\n    if(a\
    \ <= l && r <= b) return g(seg[k], x, y);\n    return f(query(a, b, LL[k][x],\
    \ LL[k][y], 2 * k + 0, l, (l + r) >> 1),\n             query(a, b, RR[k][x], RR[k][y],\
    \ 2 * k + 1, (l + r) >> 1, r));\n  }\n\n  get_t query(int a, int b, int x, int\
    \ y) {\n    x = lower_bound(begin(beet[1]), end(beet[1]), x) - begin(beet[1]);\n\
    \    y = lower_bound(begin(beet[1]), end(beet[1]), y) - begin(beet[1]);\n    return\
    \ query(a, b, x, y, 1, 0, sz);\n  }\n\n  void build() {\n    for(int k = (int)\
    \ beet.size() - 1; k >= sz; k--) {\n      sort(begin(beet[k]), end(beet[k]));\n\
    \      beet[k].erase(unique(begin(beet[k]), end(beet[k])), end(beet[k]));\n  \
    \  }\n    for(int k = sz - 1; k > 0; k--) {\n      beet[k].resize(beet[2 * k +\
    \ 0].size() + beet[2 * k + 1].size());\n      merge(begin(beet[2 * k + 0]), end(beet[2\
    \ * k + 0]), begin(beet[2 * k + 1]), end(beet[2 * k + 1]), begin(beet[k]));\n\
    \      beet[k].erase(unique(begin(beet[k]), end(beet[k])), end(beet[k]));\n  \
    \    LL[k].resize(beet[k].size() + 1);\n      RR[k].resize(beet[k].size() + 1);\n\
    \      int tail1 = 0, tail2 = 0;\n      for(int i = 0; i < beet[k].size(); i++)\
    \ {\n        while(tail1 < beet[2 * k + 0].size() && beet[2 * k + 0][tail1] <\
    \ beet[k][i]) ++tail1;\n        while(tail2 < beet[2 * k + 1].size() && beet[2\
    \ * k + 1][tail2] < beet[k][i]) ++tail2;\n        LL[k][i] = tail1, RR[k][i] =\
    \ tail2;\n      }\n      LL[k][beet[k].size()] = (int) beet[2 * k + 0].size();\n\
    \      RR[k][beet[k].size()] = (int) beet[2 * k + 1].size();\n    }\n    for(int\
    \ k = 0; k < beet.size(); k++) {\n      seg.emplace_back(structure_t(beet[k].size()));\n\
    \    }\n  }\n\n  void preupdate(int x, int y) {\n    beet[x + sz].push_back(y);\n\
    \  }\n};\n"
  code: "template< typename structure_t, typename get_t, typename update_t >\nstruct\
    \ SegmentTree2DCompressed {\n\n  using merge_f = function< get_t(get_t, get_t)\
    \ >;\n  using range_get_f = function< get_t(structure_t &, int, int) >;\n  using\
    \ update_f = function< void(structure_t &, int, update_t) >;\n\n  int sz;\n  vector<\
    \ structure_t > seg;\n  const merge_f f;\n  const range_get_f g;\n  const update_f\
    \ h;\n  const get_t identity;\n  vector< vector< int > > LL, RR;\n  vector< vector<\
    \ int > > beet;\n\n  SegmentTree2DCompressed(int n, const merge_f &f, const range_get_f\
    \ &g, const update_f &h, const get_t &identity)\n      : f(f), g(g), h(h), identity(identity)\
    \ {\n    sz = 1;\n    while(sz < n) sz <<= 1;\n    beet.resize(2 * sz);\n    LL.resize(2\
    \ * sz);\n    RR.resize(2 * sz);\n  }\n\n  void update(int a, int x, update_t\
    \ z, int k, int l, int r) {\n    if(r <= a || a + 1 <= l) return;\n    if(a <=\
    \ l && r <= a + 1) return h(seg[k], x, z);\n    update(a, LL[k][x], z, 2 * k +\
    \ 0, l, (l + r) >> 1);\n    update(a, RR[k][x], z, 2 * k + 1, (l + r) >> 1, r);\n\
    \    return h(seg[k], x, z);\n  }\n\n  void update(int x, int y, update_t z) {\n\
    \    y = lower_bound(begin(beet[1]), end(beet[1]), y) - begin(beet[1]);\n    return\
    \ update(x, y, z, 1, 0, sz);\n  }\n\n  get_t query(int a, int b, int x, int y,\
    \ int k, int l, int r) {\n    if(a >= r || b <= l) return identity;\n    if(a\
    \ <= l && r <= b) return g(seg[k], x, y);\n    return f(query(a, b, LL[k][x],\
    \ LL[k][y], 2 * k + 0, l, (l + r) >> 1),\n             query(a, b, RR[k][x], RR[k][y],\
    \ 2 * k + 1, (l + r) >> 1, r));\n  }\n\n  get_t query(int a, int b, int x, int\
    \ y) {\n    x = lower_bound(begin(beet[1]), end(beet[1]), x) - begin(beet[1]);\n\
    \    y = lower_bound(begin(beet[1]), end(beet[1]), y) - begin(beet[1]);\n    return\
    \ query(a, b, x, y, 1, 0, sz);\n  }\n\n  void build() {\n    for(int k = (int)\
    \ beet.size() - 1; k >= sz; k--) {\n      sort(begin(beet[k]), end(beet[k]));\n\
    \      beet[k].erase(unique(begin(beet[k]), end(beet[k])), end(beet[k]));\n  \
    \  }\n    for(int k = sz - 1; k > 0; k--) {\n      beet[k].resize(beet[2 * k +\
    \ 0].size() + beet[2 * k + 1].size());\n      merge(begin(beet[2 * k + 0]), end(beet[2\
    \ * k + 0]), begin(beet[2 * k + 1]), end(beet[2 * k + 1]), begin(beet[k]));\n\
    \      beet[k].erase(unique(begin(beet[k]), end(beet[k])), end(beet[k]));\n  \
    \    LL[k].resize(beet[k].size() + 1);\n      RR[k].resize(beet[k].size() + 1);\n\
    \      int tail1 = 0, tail2 = 0;\n      for(int i = 0; i < beet[k].size(); i++)\
    \ {\n        while(tail1 < beet[2 * k + 0].size() && beet[2 * k + 0][tail1] <\
    \ beet[k][i]) ++tail1;\n        while(tail2 < beet[2 * k + 1].size() && beet[2\
    \ * k + 1][tail2] < beet[k][i]) ++tail2;\n        LL[k][i] = tail1, RR[k][i] =\
    \ tail2;\n      }\n      LL[k][beet[k].size()] = (int) beet[2 * k + 0].size();\n\
    \      RR[k][beet[k].size()] = (int) beet[2 * k + 1].size();\n    }\n    for(int\
    \ k = 0; k < beet.size(); k++) {\n      seg.emplace_back(structure_t(beet[k].size()));\n\
    \    }\n  }\n\n  void preupdate(int x, int y) {\n    beet[x + sz].push_back(y);\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/segment-tree-2d.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/segment-tree/segment-tree-2d.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/segment-tree-2d.cpp
- /library/structure/segment-tree/segment-tree-2d.cpp.html
title: structure/segment-tree/segment-tree-2d.cpp
---
