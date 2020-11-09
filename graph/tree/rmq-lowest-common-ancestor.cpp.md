---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-5-c-3.test.cpp
    title: test/verify/aoj-grl-5-c-3.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    document_title: "RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148\
      )"
    links: []
  bundledCode: "#line 1 \"graph/tree/rmq-lowest-common-ancestor.cpp\"\n/**\n * @brief\
    \ RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148)\n */\ntemplate<\
    \ typename T = int >\nstruct RMQLowestCommonAncestor : Graph< T > {\npublic:\n\
    \  using Graph< T >::Graph;\n  using Graph< T >::g;\n  using F = function< int(int,\
    \ int) >;\n\n  void build(int root = 0) {\n    ord.reserve(g.size() * 2 - 1);\n\
    \    dep.reserve(g.size() * 2 - 1);\n    in.resize(g.size());\n    dfs(root, -1,\
    \ 0);\n    vector< int > vs(g.size() * 2 - 1);\n    iota(begin(vs), end(vs), 0);\n\
    \    F f = [&](int a, int b) { return dep[a] < dep[b] ? a : b; };\n    st = get_sparse_table(vs,\
    \ f);\n  }\n\n  int lca(int x, int y) const {\n    if(in[x] > in[y]) swap(x, y);\n\
    \    return x == y ? x : ord[st.fold(in[x], in[y])];\n  }\n\nprivate:\n  vector<\
    \ int > ord, dep, in;\n  SparseTable< int, F > st;\n\n  void dfs(int idx, int\
    \ par, int d) {\n    in[idx] = (int) ord.size();\n    ord.emplace_back(idx);\n\
    \    dep.emplace_back(d);\n    for(auto &to : g[idx]) {\n      if(to != par) {\n\
    \        dfs(to, idx, d + 1);\n        ord.emplace_back(idx);\n        dep.emplace_back(d);\n\
    \      }\n    }\n  }\n};\n"
  code: "/**\n * @brief RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148\
    )\n */\ntemplate< typename T = int >\nstruct RMQLowestCommonAncestor : Graph<\
    \ T > {\npublic:\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n  using\
    \ F = function< int(int, int) >;\n\n  void build(int root = 0) {\n    ord.reserve(g.size()\
    \ * 2 - 1);\n    dep.reserve(g.size() * 2 - 1);\n    in.resize(g.size());\n  \
    \  dfs(root, -1, 0);\n    vector< int > vs(g.size() * 2 - 1);\n    iota(begin(vs),\
    \ end(vs), 0);\n    F f = [&](int a, int b) { return dep[a] < dep[b] ? a : b;\
    \ };\n    st = get_sparse_table(vs, f);\n  }\n\n  int lca(int x, int y) const\
    \ {\n    if(in[x] > in[y]) swap(x, y);\n    return x == y ? x : ord[st.fold(in[x],\
    \ in[y])];\n  }\n\nprivate:\n  vector< int > ord, dep, in;\n  SparseTable< int,\
    \ F > st;\n\n  void dfs(int idx, int par, int d) {\n    in[idx] = (int) ord.size();\n\
    \    ord.emplace_back(idx);\n    dep.emplace_back(d);\n    for(auto &to : g[idx])\
    \ {\n      if(to != par) {\n        dfs(to, idx, d + 1);\n        ord.emplace_back(idx);\n\
    \        dep.emplace_back(d);\n      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/rmq-lowest-common-ancestor.cpp
  requiredBy: []
  timestamp: '2020-11-09 17:59:38+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-5-c-3.test.cpp
documentation_of: graph/tree/rmq-lowest-common-ancestor.cpp
layout: document
redirect_from:
- /library/graph/tree/rmq-lowest-common-ancestor.cpp
- /library/graph/tree/rmq-lowest-common-ancestor.cpp.html
title: "RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148)"
---
