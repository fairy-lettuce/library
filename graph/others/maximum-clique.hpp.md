---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-maximum-independent-set-2.test.cpp
    title: test/verify/yosupo-maximum-independent-set-2.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Maximum Clique(\u6700\u5927\u30AF\u30EA\u30FC\u30AF)"
    links: []
  bundledCode: "#line 2 \"graph/others/maximum-clique.hpp\"\n\n/**\n * @brief Maximum\
    \ Clique(\u6700\u5927\u30AF\u30EA\u30FC\u30AF)\n */\ntemplate< int V >\nstruct\
    \ MaximumClique {\n  using B = bitset< V >;\n  vector< B > g, col_buf;\n\n  struct\
    \ P {\n    int idx, col, deg;\n\n    P(int idx, int col, int deg) : idx(idx),\
    \ col(col), deg(deg) {}\n  };\n\n  MaximumClique() = default;\n\n  explicit MaximumClique(int\
    \ N) : g(N), col_buf(N) {}\n\n  void add_edge(int a, int b) {\n    g[a].set(b);\n\
    \    g[b].set(a);\n  }\n\n  vector< int > now, clique;\n\n  void dfs(vector< P\
    \ > &rem) {\n    if(clique.size() < now.size()) clique = now;\n    sort(begin(rem),\
    \ end(rem), [](const P &a, const P &b) {\n      return a.deg > b.deg;\n    });\n\
    \    int max_c = 1;\n    for(auto &p : rem) {\n      p.col = 0;\n      while((g[p.idx]\
    \ & col_buf[p.col]).any()) ++p.col;\n      max_c = max(max_c, p.idx + 1);\n  \
    \    col_buf[p.col].set(p.idx);\n    }\n    for(int i = 0; i < max_c; i++) col_buf[i].reset();\n\
    \    sort(begin(rem), end(rem), [&](const P &a, const P &b) {\n      return a.col\
    \ < b.col;\n    });\n    for(; !rem.empty(); rem.pop_back()) {\n      auto &p\
    \ = rem.back();\n      if(now.size() + p.col + 1 <= clique.size()) break;\n  \
    \    vector< P > nrem;\n      B bs;\n      for(auto &q : rem) {\n        if(g[p.idx][q.idx])\
    \ {\n          nrem.emplace_back(q.idx, -1, 0);\n          bs.set(q.idx);\n  \
    \      }\n      }\n      for(auto &q : nrem) {\n        q.deg = (bs & g[q.idx]).count();\n\
    \      }\n      now.emplace_back(p.idx);\n      dfs(nrem);\n      now.pop_back();\n\
    \    }\n  }\n\n  vector< int > solve() {\n    vector< P > remark;\n    for(size_t\
    \ i = 0; i < g.size(); i++) {\n      remark.emplace_back(i, -1, (int) g[i].size());\n\
    \    }\n    dfs(remark);\n    return clique;\n  }\n};\n"
  code: "#pragma once\n\n/**\n * @brief Maximum Clique(\u6700\u5927\u30AF\u30EA\u30FC\
    \u30AF)\n */\ntemplate< int V >\nstruct MaximumClique {\n  using B = bitset< V\
    \ >;\n  vector< B > g, col_buf;\n\n  struct P {\n    int idx, col, deg;\n\n  \
    \  P(int idx, int col, int deg) : idx(idx), col(col), deg(deg) {}\n  };\n\n  MaximumClique()\
    \ = default;\n\n  explicit MaximumClique(int N) : g(N), col_buf(N) {}\n\n  void\
    \ add_edge(int a, int b) {\n    g[a].set(b);\n    g[b].set(a);\n  }\n\n  vector<\
    \ int > now, clique;\n\n  void dfs(vector< P > &rem) {\n    if(clique.size() <\
    \ now.size()) clique = now;\n    sort(begin(rem), end(rem), [](const P &a, const\
    \ P &b) {\n      return a.deg > b.deg;\n    });\n    int max_c = 1;\n    for(auto\
    \ &p : rem) {\n      p.col = 0;\n      while((g[p.idx] & col_buf[p.col]).any())\
    \ ++p.col;\n      max_c = max(max_c, p.idx + 1);\n      col_buf[p.col].set(p.idx);\n\
    \    }\n    for(int i = 0; i < max_c; i++) col_buf[i].reset();\n    sort(begin(rem),\
    \ end(rem), [&](const P &a, const P &b) {\n      return a.col < b.col;\n    });\n\
    \    for(; !rem.empty(); rem.pop_back()) {\n      auto &p = rem.back();\n    \
    \  if(now.size() + p.col + 1 <= clique.size()) break;\n      vector< P > nrem;\n\
    \      B bs;\n      for(auto &q : rem) {\n        if(g[p.idx][q.idx]) {\n    \
    \      nrem.emplace_back(q.idx, -1, 0);\n          bs.set(q.idx);\n        }\n\
    \      }\n      for(auto &q : nrem) {\n        q.deg = (bs & g[q.idx]).count();\n\
    \      }\n      now.emplace_back(p.idx);\n      dfs(nrem);\n      now.pop_back();\n\
    \    }\n  }\n\n  vector< int > solve() {\n    vector< P > remark;\n    for(size_t\
    \ i = 0; i < g.size(); i++) {\n      remark.emplace_back(i, -1, (int) g[i].size());\n\
    \    }\n    dfs(remark);\n    return clique;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/maximum-clique.hpp
  requiredBy: []
  timestamp: '2021-07-21 02:10:43+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-maximum-independent-set-2.test.cpp
documentation_of: graph/others/maximum-clique.hpp
layout: document
redirect_from:
- /library/graph/others/maximum-clique.hpp
- /library/graph/others/maximum-clique.hpp.html
title: "Maximum Clique(\u6700\u5927\u30AF\u30EA\u30FC\u30AF)"
---
