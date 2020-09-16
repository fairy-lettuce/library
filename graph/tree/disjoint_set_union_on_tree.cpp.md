---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    document_title: Disjoint-Set-Union-On-Tree
    links: []
  bundledCode: "#line 1 \"graph/tree/disjoint_set_union_on_tree.cpp\"\n/**\n * @brief\
    \ Disjoint-Set-Union-On-Tree\n */\ntemplate< typename T >\nstruct DisjointSetUnionOnTree\
    \ : Graph< T > {\n  using F = function< void(int) >;\n  using Graph< T >::g;\n\
    \  vector< int > heavy, sz, in, out, ord;\n  const F expand, shrink, query;\n\
    \ \n  explicit DisjointSetUnionOnTree(int n, F expand, F shrink, F query)\n  \
    \    : Graph< T >(n), expand(move(expand)), shrink(move(shrink)), query(move(query))\
    \ {}\n \nprivate:\n  queue< int > que;\n \n  int build_subtree(int idx) {\n  \
    \  in[idx] = ord.size();\n    ord.emplace_back(idx);\n    for(auto &to : g[idx])\
    \ {\n      int sub = build_subtree(to);\n      sz[idx] += sub;\n      if(heavy[idx]\
    \ == -1 || sz[heavy[idx]] < sub) {\n        heavy[idx] = to;\n      }\n    }\n\
    \    out[idx] = ord.size();\n    return sz[idx];\n  }\n \n  void dfs(int idx,\
    \ bool keep) {\n    for(auto &to : g[idx]) {\n      if(heavy[idx] == to) continue;\n\
    \      dfs(to, false);\n    }\n    if(heavy[idx] != -1) {\n      dfs(heavy[idx],\
    \ true);\n    }\n    for(auto &to : g[idx]) {\n      if(heavy[idx] == to) continue;\n\
    \      for(int p = in[to]; p < out[to]; p++) {\n        expand(ord[p]);\n    \
    \  }\n    }\n    expand(idx);\n    query(idx);\n    if(!keep) {\n      for(int\
    \ p = in[idx]; p < out[idx]; p++) shrink(ord[p]);\n    }\n  }\n \npublic:\n  void\
    \ build(int root = 0) {\n    g = convert_rooted_tree(*this, root).g;\n    sz.assign(g.size(),\
    \ 1);\n    heavy.assign(g.size(), -1);\n    in.resize(g.size());\n    out.resize(g.size());\n\
    \    build_subtree(root);\n    dfs(root, false);\n  }\n};\n"
  code: "/**\n * @brief Disjoint-Set-Union-On-Tree\n */\ntemplate< typename T >\n\
    struct DisjointSetUnionOnTree : Graph< T > {\n  using F = function< void(int)\
    \ >;\n  using Graph< T >::g;\n  vector< int > heavy, sz, in, out, ord;\n  const\
    \ F expand, shrink, query;\n \n  explicit DisjointSetUnionOnTree(int n, F expand,\
    \ F shrink, F query)\n      : Graph< T >(n), expand(move(expand)), shrink(move(shrink)),\
    \ query(move(query)) {}\n \nprivate:\n  queue< int > que;\n \n  int build_subtree(int\
    \ idx) {\n    in[idx] = ord.size();\n    ord.emplace_back(idx);\n    for(auto\
    \ &to : g[idx]) {\n      int sub = build_subtree(to);\n      sz[idx] += sub;\n\
    \      if(heavy[idx] == -1 || sz[heavy[idx]] < sub) {\n        heavy[idx] = to;\n\
    \      }\n    }\n    out[idx] = ord.size();\n    return sz[idx];\n  }\n \n  void\
    \ dfs(int idx, bool keep) {\n    for(auto &to : g[idx]) {\n      if(heavy[idx]\
    \ == to) continue;\n      dfs(to, false);\n    }\n    if(heavy[idx] != -1) {\n\
    \      dfs(heavy[idx], true);\n    }\n    for(auto &to : g[idx]) {\n      if(heavy[idx]\
    \ == to) continue;\n      for(int p = in[to]; p < out[to]; p++) {\n        expand(ord[p]);\n\
    \      }\n    }\n    expand(idx);\n    query(idx);\n    if(!keep) {\n      for(int\
    \ p = in[idx]; p < out[idx]; p++) shrink(ord[p]);\n    }\n  }\n \npublic:\n  void\
    \ build(int root = 0) {\n    g = convert_rooted_tree(*this, root).g;\n    sz.assign(g.size(),\
    \ 1);\n    heavy.assign(g.size(), -1);\n    in.resize(g.size());\n    out.resize(g.size());\n\
    \    build_subtree(root);\n    dfs(root, false);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/disjoint_set_union_on_tree.cpp
  requiredBy: []
  timestamp: '2020-09-08 23:29:00+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: graph/tree/disjoint_set_union_on_tree.cpp
layout: document
redirect_from:
- /library/graph/tree/disjoint_set_union_on_tree.cpp
- /library/graph/tree/disjoint_set_union_on_tree.cpp.html
title: Disjoint-Set-Union-On-Tree
---
