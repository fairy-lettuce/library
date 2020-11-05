---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-5-c-3.test.cpp
    title: test/verify/aoj-grl-5-c-3.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148\
      )"
    links: []
  bundledCode: "#line 1 \"graph/tree/rmq-lowest-common-ancestor.cpp\"\n/**\n * @brief\
    \ RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148)\n */\ntemplate<\
    \ typename T = int >\nstruct RMQLowestCommonAncestor : Graph< T > {\npublic:\n\
    \  using Graph< T >::Graph;\n  using Graph< T >::g;\n\n  void build(int root =\
    \ 0) {\n    ord.reserve(g.size() * 2 - 1);\n    dep.reserve(g.size() * 2 - 1);\n\
    \    in.resize(g.size());\n    dfs(root, -1, 0);\n    build_sparse_table();\n\
    \  }\n\n  int lca(int x, int y) const {\n    if(in[x] > in[y]) swap(x, y);\n \
    \   return x == y ? x : ord[rmq(in[x], in[y])];\n  }\n\nprivate:\n  vector< int\
    \ > ord, dep, in;\n  vector< vector< int > > st;\n  vector< char > lg;\n\n  inline\
    \ int chmin(int x, int y) const { return dep[x] < dep[y] ? x : y; }\n\n  void\
    \ build_sparse_table() {\n    int b = 0;\n    while((1 << b) <= dep.size()) ++b;\n\
    \    st.assign(b, vector< T >(1 << b));\n    lg.resize(dep.size() + 1);\n    for(int\
    \ i = 0; i <= dep.size(); i++) {\n      lg[i] = 31 - __builtin_clz(i);\n    }\n\
    \    for(int i = 0; i < dep.size(); i++) {\n      st[0][i] = i;\n    }\n    for(int\
    \ i = 1; i < b; i++) {\n      for(int j = 0; j + (1 << i) <= (1 << b); j++) {\n\
    \        st[i][j] = chmin(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);\n    \
    \  }\n    }\n  }\n\n  inline T rmq(int l, int r) const // [l, r)\n  {\n    auto\
    \ b = lg[r - l];\n    return chmin(st[b][l], st[b][r - (1 << b)]);\n  }\n\n  void\
    \ dfs(int idx, int par, int d) {\n    in[idx] = (int) ord.size();\n    ord.emplace_back(idx);\n\
    \    dep.emplace_back(d);\n    for(auto &to : g[idx]) {\n      if(to != par) {\n\
    \        dfs(to, idx, d + 1);\n        ord.emplace_back(idx);\n        dep.emplace_back(d);\n\
    \      }\n    }\n  }\n};\n"
  code: "/**\n * @brief RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148\
    )\n */\ntemplate< typename T = int >\nstruct RMQLowestCommonAncestor : Graph<\
    \ T > {\npublic:\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n\n  void\
    \ build(int root = 0) {\n    ord.reserve(g.size() * 2 - 1);\n    dep.reserve(g.size()\
    \ * 2 - 1);\n    in.resize(g.size());\n    dfs(root, -1, 0);\n    build_sparse_table();\n\
    \  }\n\n  int lca(int x, int y) const {\n    if(in[x] > in[y]) swap(x, y);\n \
    \   return x == y ? x : ord[rmq(in[x], in[y])];\n  }\n\nprivate:\n  vector< int\
    \ > ord, dep, in;\n  vector< vector< int > > st;\n  vector< char > lg;\n\n  inline\
    \ int chmin(int x, int y) const { return dep[x] < dep[y] ? x : y; }\n\n  void\
    \ build_sparse_table() {\n    int b = 0;\n    while((1 << b) <= dep.size()) ++b;\n\
    \    st.assign(b, vector< T >(1 << b));\n    lg.resize(dep.size() + 1);\n    for(int\
    \ i = 0; i <= dep.size(); i++) {\n      lg[i] = 31 - __builtin_clz(i);\n    }\n\
    \    for(int i = 0; i < dep.size(); i++) {\n      st[0][i] = i;\n    }\n    for(int\
    \ i = 1; i < b; i++) {\n      for(int j = 0; j + (1 << i) <= (1 << b); j++) {\n\
    \        st[i][j] = chmin(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]);\n    \
    \  }\n    }\n  }\n\n  inline T rmq(int l, int r) const // [l, r)\n  {\n    auto\
    \ b = lg[r - l];\n    return chmin(st[b][l], st[b][r - (1 << b)]);\n  }\n\n  void\
    \ dfs(int idx, int par, int d) {\n    in[idx] = (int) ord.size();\n    ord.emplace_back(idx);\n\
    \    dep.emplace_back(d);\n    for(auto &to : g[idx]) {\n      if(to != par) {\n\
    \        dfs(to, idx, d + 1);\n        ord.emplace_back(idx);\n        dep.emplace_back(d);\n\
    \      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/rmq-lowest-common-ancestor.cpp
  requiredBy: []
  timestamp: '2020-11-05 21:58:50+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-5-c-3.test.cpp
documentation_of: graph/tree/rmq-lowest-common-ancestor.cpp
layout: document
redirect_from:
- /library/graph/tree/rmq-lowest-common-ancestor.cpp
- /library/graph/tree/rmq-lowest-common-ancestor.cpp.html
title: "RMQ-Lowest-Common-Ancestor(\u6700\u5C0F\u5171\u901A\u7956\u5148)"
---
