---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/yosupo-static-range-inversions-query.test.cpp
    title: test/verify/yosupo-static-range-inversions-query.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: Mo's Algorithm
    links: []
  bundledCode: "#line 1 \"other/mo.cpp\"\n/**\n * @brief Mo's Algorithm\n */\nstruct\
    \ Mo {\n  int n;\n  vector< pair< int, int > > lr;\n\n  explicit Mo(int n) : n(n)\
    \ {}\n\n  void add(int l, int r) { /* [l, r) */\n    lr.emplace_back(l, r);\n\
    \  }\n\n  template< typename AL, typename AR, typename EL, typename ER, typename\
    \ O >\n  void build(const AL &add_left, const AR &add_right, const EL &erase_left,\
    \ const ER &erase_right, const O &out) {\n    int q = (int) lr.size();\n    int\
    \ bs = n / min< int >(n, sqrt(q));\n    vector< int > ord(q);\n    iota(begin(ord),\
    \ end(ord), 0);\n    sort(begin(ord), end(ord), [&](int a, int b) {\n      int\
    \ ablock = lr[a].first / bs, bblock = lr[b].first / bs;\n      if(ablock != bblock)\
    \ return ablock < bblock;\n      return (ablock & 1) ? lr[a].second > lr[b].second\
    \ : lr[a].second < lr[b].second;\n    });\n    int l = 0, r = 0;\n    for(auto\
    \ idx : ord) {\n      while(l > lr[idx].first) add_left(--l);\n      while(r <\
    \ lr[idx].second) add_right(r++);\n      while(l < lr[idx].first) erase_left(l++);\n\
    \      while(r > lr[idx].second) erase_right(--r);\n      out(idx);\n    }\n \
    \ }\n\n  template< typename A, typename E, typename O >\n  void build(const A\
    \ &add, const E &erase, const O &out) {\n    build(add, add, erase, erase, out);\n\
    \  }\n};\n"
  code: "/**\n * @brief Mo's Algorithm\n */\nstruct Mo {\n  int n;\n  vector< pair<\
    \ int, int > > lr;\n\n  explicit Mo(int n) : n(n) {}\n\n  void add(int l, int\
    \ r) { /* [l, r) */\n    lr.emplace_back(l, r);\n  }\n\n  template< typename AL,\
    \ typename AR, typename EL, typename ER, typename O >\n  void build(const AL &add_left,\
    \ const AR &add_right, const EL &erase_left, const ER &erase_right, const O &out)\
    \ {\n    int q = (int) lr.size();\n    int bs = n / min< int >(n, sqrt(q));\n\
    \    vector< int > ord(q);\n    iota(begin(ord), end(ord), 0);\n    sort(begin(ord),\
    \ end(ord), [&](int a, int b) {\n      int ablock = lr[a].first / bs, bblock =\
    \ lr[b].first / bs;\n      if(ablock != bblock) return ablock < bblock;\n    \
    \  return (ablock & 1) ? lr[a].second > lr[b].second : lr[a].second < lr[b].second;\n\
    \    });\n    int l = 0, r = 0;\n    for(auto idx : ord) {\n      while(l > lr[idx].first)\
    \ add_left(--l);\n      while(r < lr[idx].second) add_right(r++);\n      while(l\
    \ < lr[idx].first) erase_left(l++);\n      while(r > lr[idx].second) erase_right(--r);\n\
    \      out(idx);\n    }\n  }\n\n  template< typename A, typename E, typename O\
    \ >\n  void build(const A &add, const E &erase, const O &out) {\n    build(add,\
    \ add, erase, erase, out);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/mo.cpp
  requiredBy: []
  timestamp: '2020-08-12 02:55:35+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/yosupo-static-range-inversions-query.test.cpp
documentation_of: other/mo.cpp
layout: document
redirect_from:
- /library/other/mo.cpp
- /library/other/mo.cpp.html
title: Mo's Algorithm
---
