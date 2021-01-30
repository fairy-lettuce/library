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
  bundledCode: "#line 1 \"structure/segment-tree/segment-tree-fractional-cascading.cpp\"\
    \nstruct SegmentTreeFractionalCascading {\n  vector< vector< int > > seg;\n  vector<\
    \ vector< int > > LL, RR;\n  int sz;\n\n  SegmentTreeFractionalCascading(vector<\
    \ int > &array) {\n    sz = 1;\n    while(sz < array.size()) sz <<= 1;\n    seg.resize(2\
    \ * sz - 1);\n    LL.resize(2 * sz - 1);\n    RR.resize(2 * sz - 1);\n    for(int\
    \ k = 0; k < array.size(); k++) {\n      seg[k + sz - 1].emplace_back(array[k]);\n\
    \    }\n    for(int k = sz - 2; k >= 0; k--) {\n      seg[k].resize(seg[2 * k\
    \ + 1].size() + seg[2 * k + 2].size());\n      LL[k].resize(seg[k].size() + 1);\n\
    \      RR[k].resize(seg[k].size() + 1);\n      merge(begin(seg[2 * k + 1]), end(seg[2\
    \ * k + 1]), begin(seg[2 * k + 2]), end(seg[2 * k + 2]), begin(seg[k]));\n   \
    \   int tail1 = 0, tail2 = 0;\n      for(int i = 0; i < seg[k].size(); i++) {\n\
    \        while(tail1 < seg[2 * k + 1].size() && seg[2 * k + 1][tail1] < seg[k][i])\
    \ ++tail1;\n        while(tail2 < seg[2 * k + 2].size() && seg[2 * k + 2][tail2]\
    \ < seg[k][i]) ++tail2;\n        LL[k][i] = tail1, RR[k][i] = tail2;\n      }\n\
    \      LL[k][seg[k].size()] = (int) seg[2 * k + 1].size();\n      RR[k][seg[k].size()]\
    \ = (int) seg[2 * k + 2].size();\n    }\n  }\n\n  int query(int a, int b, int\
    \ lower, int upper, int k, int l, int r) {\n    if(a >= r || b <= l) {\n     \
    \ return (0);\n    } else if(a <= l && r <= b) {\n      return (upper - lower);\n\
    \    } else {\n      return (query(a, b, LL[k][lower], LL[k][upper], 2 * k + 1,\
    \ l, (l + r) >> 1) + query(a, b, RR[k][lower], RR[k][upper], 2 * k + 2, (l + r)\
    \ >> 1, r));\n    }\n  }\n\n  int query(int a, int b, int l, int r) {\n    l =\
    \ lower_bound(begin(seg[0]), end(seg[0]), l) - begin(seg[0]);\n    r = lower_bound(begin(seg[0]),\
    \ end(seg[0]), r) - begin(seg[0]);\n    return (query(a, b, l, r, 0, 0, sz));\n\
    \  }\n};\n"
  code: "struct SegmentTreeFractionalCascading {\n  vector< vector< int > > seg;\n\
    \  vector< vector< int > > LL, RR;\n  int sz;\n\n  SegmentTreeFractionalCascading(vector<\
    \ int > &array) {\n    sz = 1;\n    while(sz < array.size()) sz <<= 1;\n    seg.resize(2\
    \ * sz - 1);\n    LL.resize(2 * sz - 1);\n    RR.resize(2 * sz - 1);\n    for(int\
    \ k = 0; k < array.size(); k++) {\n      seg[k + sz - 1].emplace_back(array[k]);\n\
    \    }\n    for(int k = sz - 2; k >= 0; k--) {\n      seg[k].resize(seg[2 * k\
    \ + 1].size() + seg[2 * k + 2].size());\n      LL[k].resize(seg[k].size() + 1);\n\
    \      RR[k].resize(seg[k].size() + 1);\n      merge(begin(seg[2 * k + 1]), end(seg[2\
    \ * k + 1]), begin(seg[2 * k + 2]), end(seg[2 * k + 2]), begin(seg[k]));\n   \
    \   int tail1 = 0, tail2 = 0;\n      for(int i = 0; i < seg[k].size(); i++) {\n\
    \        while(tail1 < seg[2 * k + 1].size() && seg[2 * k + 1][tail1] < seg[k][i])\
    \ ++tail1;\n        while(tail2 < seg[2 * k + 2].size() && seg[2 * k + 2][tail2]\
    \ < seg[k][i]) ++tail2;\n        LL[k][i] = tail1, RR[k][i] = tail2;\n      }\n\
    \      LL[k][seg[k].size()] = (int) seg[2 * k + 1].size();\n      RR[k][seg[k].size()]\
    \ = (int) seg[2 * k + 2].size();\n    }\n  }\n\n  int query(int a, int b, int\
    \ lower, int upper, int k, int l, int r) {\n    if(a >= r || b <= l) {\n     \
    \ return (0);\n    } else if(a <= l && r <= b) {\n      return (upper - lower);\n\
    \    } else {\n      return (query(a, b, LL[k][lower], LL[k][upper], 2 * k + 1,\
    \ l, (l + r) >> 1) + query(a, b, RR[k][lower], RR[k][upper], 2 * k + 2, (l + r)\
    \ >> 1, r));\n    }\n  }\n\n  int query(int a, int b, int l, int r) {\n    l =\
    \ lower_bound(begin(seg[0]), end(seg[0]), l) - begin(seg[0]);\n    r = lower_bound(begin(seg[0]),\
    \ end(seg[0]), r) - begin(seg[0]);\n    return (query(a, b, l, r, 0, 0, sz));\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/segment-tree-fractional-cascading.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/segment-tree/segment-tree-fractional-cascading.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/segment-tree-fractional-cascading.cpp
- /library/structure/segment-tree/segment-tree-fractional-cascading.cpp.html
title: structure/segment-tree/segment-tree-fractional-cascading.cpp
---
