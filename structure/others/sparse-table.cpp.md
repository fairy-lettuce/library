---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-staticrmq.test.cpp
    title: test/verify/yosupo-staticrmq.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    _deprecated_at_docs: docs/sparse-table.md
    document_title: "Sparse-Table(\u30B9\u30D1\u30FC\u30B9\u30C6\u30FC\u30D6\u30EB\
      )"
    links: []
  bundledCode: "#line 1 \"structure/others/sparse-table.cpp\"\n/**\n * @brief Sparse-Table(\u30B9\
    \u30D1\u30FC\u30B9\u30C6\u30FC\u30D6\u30EB)\n * @docs docs/sparse-table.md\n */\n\
    template< typename T >\nstruct SparseTable {\n  vector< vector< T > > st;\n  vector<\
    \ int > lookup;\n\n  explicit SparseTable(const vector< T > &v) {\n    int b =\
    \ 0;\n    while((1 << b) <= v.size()) ++b;\n    st.assign(b, vector< T >(1 <<\
    \ b));\n    for(int i = 0; i < v.size(); i++) {\n      st[0][i] = v[i];\n    }\n\
    \    for(int i = 1; i < b; i++) {\n      for(int j = 0; j + (1 << i) <= (1 <<\
    \ b); j++) {\n        st[i][j] = min(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);\n\
    \      }\n    }\n    lookup.resize(v.size() + 1);\n    for(int i = 2; i < lookup.size();\
    \ i++) {\n      lookup[i] = lookup[i >> 1] + 1;\n    }\n  }\n\n  inline T query(int\
    \ l, int r) const {\n    int b = lookup[r - l];\n    return min(st[b][l], st[b][r\
    \ - (1 << b)]);\n  }\n};\n"
  code: "/**\n * @brief Sparse-Table(\u30B9\u30D1\u30FC\u30B9\u30C6\u30FC\u30D6\u30EB\
    )\n * @docs docs/sparse-table.md\n */\ntemplate< typename T >\nstruct SparseTable\
    \ {\n  vector< vector< T > > st;\n  vector< int > lookup;\n\n  explicit SparseTable(const\
    \ vector< T > &v) {\n    int b = 0;\n    while((1 << b) <= v.size()) ++b;\n  \
    \  st.assign(b, vector< T >(1 << b));\n    for(int i = 0; i < v.size(); i++) {\n\
    \      st[0][i] = v[i];\n    }\n    for(int i = 1; i < b; i++) {\n      for(int\
    \ j = 0; j + (1 << i) <= (1 << b); j++) {\n        st[i][j] = min(st[i - 1][j],\
    \ st[i - 1][j + (1 << (i - 1))]);\n      }\n    }\n    lookup.resize(v.size()\
    \ + 1);\n    for(int i = 2; i < lookup.size(); i++) {\n      lookup[i] = lookup[i\
    \ >> 1] + 1;\n    }\n  }\n\n  inline T query(int l, int r) const {\n    int b\
    \ = lookup[r - l];\n    return min(st[b][l], st[b][r - (1 << b)]);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/sparse-table.cpp
  requiredBy: []
  timestamp: '2020-02-20 22:23:04+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-staticrmq.test.cpp
documentation_of: structure/others/sparse-table.cpp
layout: document
redirect_from:
- /library/structure/others/sparse-table.cpp
- /library/structure/others/sparse-table.cpp.html
title: "Sparse-Table(\u30B9\u30D1\u30FC\u30B9\u30C6\u30FC\u30D6\u30EB)"
---
## 概要

更新がない場合の区間の最小値を, 前計算 $O(n \log n)$, クエリ $O(1)$ で処理する.

* `SparseTable(v)`: 配列 `v` で初期化する.
* `query(l, r)`: 区間 $[l, r)$ の最小値を求める.

## 計算量

* `SparseTable(v)`: $O(N \log N)$
* `query(l, r)`: $O(1)$
