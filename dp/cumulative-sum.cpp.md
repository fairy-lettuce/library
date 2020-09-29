---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-static-range-sum.test.cpp
    title: test/verify/yosupo-static-range-sum.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/cumulative-sum.md
    document_title: "Cumulative-Sum(\u4E00\u6B21\u5143\u7D2F\u7A4D\u548C)"
    links: []
  bundledCode: "#line 1 \"dp/cumulative-sum.cpp\"\n/**\n * @brief Cumulative-Sum(\u4E00\
    \u6B21\u5143\u7D2F\u7A4D\u548C)\n * @docs docs/cumulative-sum.md\n */\ntemplate<\
    \ class T >\nstruct CumulativeSum {\n  vector< T > data;\n\n  CumulativeSum()\
    \ = default;\n\n  explicit CumulativeSum(size_t sz) : data(sz, 0) {}\n\n  void\
    \ add(int k, const T &x) {\n    data[k] += x;\n  }\n\n  void build() {\n    for(int\
    \ i = 1; i < data.size(); i++) {\n      data[i] += data[i - 1];\n    }\n  }\n\n\
    \  T query(int k) const {\n    if(k < 0) return 0;\n    return data[min(k, (int)\
    \ data.size() - 1)];\n  }\n};\n"
  code: "/**\n * @brief Cumulative-Sum(\u4E00\u6B21\u5143\u7D2F\u7A4D\u548C)\n * @docs\
    \ docs/cumulative-sum.md\n */\ntemplate< class T >\nstruct CumulativeSum {\n \
    \ vector< T > data;\n\n  CumulativeSum() = default;\n\n  explicit CumulativeSum(size_t\
    \ sz) : data(sz, 0) {}\n\n  void add(int k, const T &x) {\n    data[k] += x;\n\
    \  }\n\n  void build() {\n    for(int i = 1; i < data.size(); i++) {\n      data[i]\
    \ += data[i - 1];\n    }\n  }\n\n  T query(int k) const {\n    if(k < 0) return\
    \ 0;\n    return data[min(k, (int) data.size() - 1)];\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: dp/cumulative-sum.cpp
  requiredBy: []
  timestamp: '2020-02-20 22:23:04+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-static-range-sum.test.cpp
documentation_of: dp/cumulative-sum.cpp
layout: document
redirect_from:
- /library/dp/cumulative-sum.cpp
- /library/dp/cumulative-sum.cpp.html
title: "Cumulative-Sum(\u4E00\u6B21\u5143\u7D2F\u7A4D\u548C)"
---
## 概要

$1$ 次元の累積和. 前計算として事前に累積和をとることで, 区間の和を $O(1)$ で求めることが出来る.

* `add(k, x)`: 要素 `k` に値 `x` を加える.
* `build()`: 累積和を構築する.
* `query(k)`: 区間 $[0, k]$ の和を求める(閉区間なので注意).

## 計算量

* `add(k, x)`: $O(1)$
* `build()`: $O(N)$
* `query(k)`: $O(1)$
