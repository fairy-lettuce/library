---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    _deprecated_at_docs: docs/namori-graph.md
    document_title: Namori-Graph
    links: []
  bundledCode: "#line 1 \"graph/others/namori-graph.cpp\"\n/**\n * @brief Namori-Graph\n\
    \ * @docs docs/namori-graph.md\n */\ntemplate< typename T = int >\nstruct NamoriGraph\
    \ : Graph< T > {\npublic:\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n\
    \n  vector< Graph< T > > forest;\n  Edges< T > loop_edges;\n\n  struct Info {\n\
    \    int forest_id, id;\n  };\n\n  Info operator[](const int &k) const {\n   \
    \ return (Info) {mark_id[k], id[k]};\n  }\n\n  int inv(int forest_id, int k) {\n\
    \    return iv[forest_id][k];\n  }\n\n  void build() {\n    int n = (int) g.size();\n\
    \    vector< int > deg(n), used(n);\n    queue< int > que;\n    for(int i = 0;\
    \ i < n; i++) {\n      deg[i] = (int) g[i].size();\n      if(deg[i] == 1) {\n\
    \        que.emplace(i);\n        used[i] = true;\n      }\n    }\n    while(not\
    \ que.empty()) {\n      int idx = que.front();\n      que.pop();\n      for(auto\
    \ &e : g[idx]) {\n        if(used[e.to]) {\n          continue;\n        }\n \
    \       --deg[e.to];\n        if(deg[e.to] == 1) {\n          que.emplace(e.to);\n\
    \          used[e.to] = true;\n        }\n      }\n    }\n    int mx = 0;\n  \
    \  for(auto &edges : g) {\n      for(auto &e : edges) mx = max(mx, e.idx);\n \
    \   }\n    vector< int > edge_used(mx + 1);\n    vector< int > loop;\n    for(int\
    \ v = 0; v < n; v++) {\n      if(used[v]) {\n        continue;\n      }\n    \
    \  while(!used[v]) {\n        loop.emplace_back(v);\n        for(auto &e : g[v])\
    \ {\n          if(used[e.to] or edge_used[e.idx]) {\n            continue;\n \
    \         }\n          loop_edges.emplace_back(loop.size() - 1, loop.size(), e.cost,\
    \ e.idx);\n          v = e.to;\n          used[e.to] = true;\n          edge_used[e.idx]\
    \ = true;\n          break;\n        }\n      }\n      break;\n    }\n    loop_edges.back().to\
    \ = 0;\n    mark_id.resize(n);\n    id.resize(n);\n    int ptr = 0;\n    for(int\
    \ i = 0; i < (int) loop.size(); i++) {\n      int pre = loop[(i + loop.size()\
    \ - 1) % loop.size()];\n      int nxt = loop[(i + 1) % loop.size()];\n      int\
    \ sz = 0;\n      mark_id[loop[i]] = ptr;\n      iv.emplace_back();\n      id[loop[i]]\
    \ = sz++;\n      iv.back().emplace_back(loop[i]);\n      for(auto &e : g[loop[i]])\
    \ {\n        if(e.to != pre and e.to != nxt) {\n          mark_dfs(e.to, loop[i],\
    \ ptr, sz);\n          build_dfs(e.to, loop[i]);\n        }\n      }\n      Graph<\
    \ T > tree(sz);\n      for(auto &e : g[loop_vers[i]]) {\n        if(e.to != pre\
    \ and e.to != nxt) {\n          tree.add_edge(id[loop_vers[i]], id[e.to], e.cost,\
    \ e.idx);\n          build_dfs(e.to, loop_vers[i], tree);\n        }\n      }\n\
    \      forest.emplace_back(tree);\n    }\n  }\n\nprivate:\n  vector< vector< int\
    \ > > iv;\n  vector< int > mark_id, id;\n\n  void mark_dfs(int idx, int par, int\
    \ k, int &l) {\n    mark_id[idx] = k;\n    id[idx] = l++;\n    iv.back().emplace_back(idx);\n\
    \    for(auto &e : g[idx]) {\n      if(e.to != par) {\n        mark_dfs(e.to,\
    \ idx, k);\n      }\n    }\n  }\n\n  void build_dfs(int idx, int par, Graph< T\
    \ > &tree) {\n    for(auto &e : g[idx]) {\n      if(e.to != par) {\n        tree.add_edge(id[idx],\
    \ id[e.to], e.cost, e.idx);\n        build_dfs(e.to, idx, tree);\n      }\n  \
    \  }\n  }\n};\n"
  code: "/**\n * @brief Namori-Graph\n * @docs docs/namori-graph.md\n */\ntemplate<\
    \ typename T = int >\nstruct NamoriGraph : Graph< T > {\npublic:\n  using Graph<\
    \ T >::Graph;\n  using Graph< T >::g;\n\n  vector< Graph< T > > forest;\n  Edges<\
    \ T > loop_edges;\n\n  struct Info {\n    int forest_id, id;\n  };\n\n  Info operator[](const\
    \ int &k) const {\n    return (Info) {mark_id[k], id[k]};\n  }\n\n  int inv(int\
    \ forest_id, int k) {\n    return iv[forest_id][k];\n  }\n\n  void build() {\n\
    \    int n = (int) g.size();\n    vector< int > deg(n), used(n);\n    queue< int\
    \ > que;\n    for(int i = 0; i < n; i++) {\n      deg[i] = (int) g[i].size();\n\
    \      if(deg[i] == 1) {\n        que.emplace(i);\n        used[i] = true;\n \
    \     }\n    }\n    while(not que.empty()) {\n      int idx = que.front();\n \
    \     que.pop();\n      for(auto &e : g[idx]) {\n        if(used[e.to]) {\n  \
    \        continue;\n        }\n        --deg[e.to];\n        if(deg[e.to] == 1)\
    \ {\n          que.emplace(e.to);\n          used[e.to] = true;\n        }\n \
    \     }\n    }\n    int mx = 0;\n    for(auto &edges : g) {\n      for(auto &e\
    \ : edges) mx = max(mx, e.idx);\n    }\n    vector< int > edge_used(mx + 1);\n\
    \    vector< int > loop;\n    for(int v = 0; v < n; v++) {\n      if(used[v])\
    \ {\n        continue;\n      }\n      while(!used[v]) {\n        loop.emplace_back(v);\n\
    \        for(auto &e : g[v]) {\n          if(used[e.to] or edge_used[e.idx]) {\n\
    \            continue;\n          }\n          loop_edges.emplace_back(loop.size()\
    \ - 1, loop.size(), e.cost, e.idx);\n          v = e.to;\n          used[e.to]\
    \ = true;\n          edge_used[e.idx] = true;\n          break;\n        }\n \
    \     }\n      break;\n    }\n    loop_edges.back().to = 0;\n    mark_id.resize(n);\n\
    \    id.resize(n);\n    int ptr = 0;\n    for(int i = 0; i < (int) loop.size();\
    \ i++) {\n      int pre = loop[(i + loop.size() - 1) % loop.size()];\n      int\
    \ nxt = loop[(i + 1) % loop.size()];\n      int sz = 0;\n      mark_id[loop[i]]\
    \ = ptr;\n      iv.emplace_back();\n      id[loop[i]] = sz++;\n      iv.back().emplace_back(loop[i]);\n\
    \      for(auto &e : g[loop[i]]) {\n        if(e.to != pre and e.to != nxt) {\n\
    \          mark_dfs(e.to, loop[i], ptr, sz);\n          build_dfs(e.to, loop[i]);\n\
    \        }\n      }\n      Graph< T > tree(sz);\n      for(auto &e : g[loop_vers[i]])\
    \ {\n        if(e.to != pre and e.to != nxt) {\n          tree.add_edge(id[loop_vers[i]],\
    \ id[e.to], e.cost, e.idx);\n          build_dfs(e.to, loop_vers[i], tree);\n\
    \        }\n      }\n      forest.emplace_back(tree);\n    }\n  }\n\nprivate:\n\
    \  vector< vector< int > > iv;\n  vector< int > mark_id, id;\n\n  void mark_dfs(int\
    \ idx, int par, int k, int &l) {\n    mark_id[idx] = k;\n    id[idx] = l++;\n\
    \    iv.back().emplace_back(idx);\n    for(auto &e : g[idx]) {\n      if(e.to\
    \ != par) {\n        mark_dfs(e.to, idx, k);\n      }\n    }\n  }\n\n  void build_dfs(int\
    \ idx, int par, Graph< T > &tree) {\n    for(auto &e : g[idx]) {\n      if(e.to\
    \ != par) {\n        tree.add_edge(id[idx], id[e.to], e.cost, e.idx);\n      \
    \  build_dfs(e.to, idx, tree);\n      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/namori-graph.cpp
  requiredBy: []
  timestamp: '2021-04-18 02:03:03+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: graph/others/namori-graph.cpp
layout: document
redirect_from:
- /library/graph/others/namori-graph.cpp
- /library/graph/others/namori-graph.cpp.html
title: Namori-Graph
---
バグっているので使わないでください！(は？)

## 概要

$n$ 頂点 $n$ 辺からなる連結無向グラフは, サイクルが $1$ 個だけあるグラフとなる。

このグラフを, とある漫画家のアイコンにちなんで なもりグラフ と呼ばれることがるが, 学術的には Unicyclic Graph, Pseudoforest が正しい。

ここでは, このグラフを 1 つのサイクル と, サイクル内の頂点に付属する木に分解する。また頂点番号をサイクルの頂点に, サイクルの頂点数を $k$ として $[0, k)$ にふりなおす。また付属する木も同様に, 木の頂点数を $l$ として $[0, l)$ にふりなおす。


## 使い方

* `build()`: サイクルと木に分解する。頂点数と辺の本数が同じ無向連結グラフである必要がある。
* `forest`: 分解した無向木がサイクルの頂点の順に格納される。木の頂点番号は$0$ から振り直している。
* `loop_edges`: サイクルに含まれる辺が順に格納される。頂点番号はサイクルの頂点数を $k$ として $[0, k)$ にふりなおされている。$i$ 番目の辺は頂点 $i$ と $i+1$ を結ぶ辺である。
* `operator[k]`: 頂点 $k$ について, それが属するサイクルの頂点番号 `forest_id`, 振り直された木の頂点番号 `id` を返す。同様に `forest_id` は $[0, k)$ に振り直されている。
* `inv(forest_id, k)`: サイクルの頂点 `forest_id` の木の頂点 $k$ のもとの頂点番号を返す。特に `inv(forest_id, 0)` はサイクルに含まれいたもとの頂点番号を指す。

## 計算量

* $O(N)$
