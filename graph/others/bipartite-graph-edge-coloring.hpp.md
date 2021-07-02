---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bipartite-edge-coloring.test.cpp
    title: test/verify/yosupo-bipartite-edge-coloring.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Bipartite-Graph-Edge-Coloring(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\
      \u8FBA\u5F69\u8272)"
    links:
    - https://ei1333.hateblo.jp/entry/2020/08/25/015955
  bundledCode: "#line 2 \"graph/others/bipartite-graph-edge-coloring.hpp\"\n/**\n\
    \ * @brief Bipartite-Graph-Edge-Coloring(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\u8FBA\
    \u5F69\u8272)\n * @see https://ei1333.hateblo.jp/entry/2020/08/25/015955\n */\n\
    struct BipariteGraphEdgeColoring {\nprivate:\n  vector< vector< int > > ans;\n\
    \  vector< int > A, B;\n  int L, R;\n\n  struct RegularGraph {\n    int k{}, n{};\n\
    \    vector< int > A, B;\n  };\n  RegularGraph g;\n\n  static UnionFind contract(valarray<\
    \ int > &deg, int k) {\n    using pi = pair< int, int >;\n    priority_queue<\
    \ pi, vector< pi >, greater<> > que;\n    for(int i = 0; i < (int) deg.size();\
    \ i++) {\n      que.emplace(deg[i], i);\n    }\n    UnionFind uf(deg.size());\n\
    \    while(que.size() > 1) {\n      auto p = que.top();\n      que.pop();\n  \
    \    auto q = que.top();\n      que.pop();\n      if(p.first + q.first > k) continue;\n\
    \      p.first += q.first;\n      uf.unite(p.second, q.second);\n      que.emplace(p);\n\
    \    }\n    return uf;\n  }\n\n\n  RegularGraph build_k_regular_graph() {\n  \
    \  valarray< int > deg[2];\n    deg[0] = valarray< int >(L);\n    deg[1] = valarray<\
    \ int >(R);\n    for(auto &p : A) deg[0][p]++;\n    for(auto &p : B) deg[1][p]++;\n\
    \n    int k = max(deg[0].max(), deg[1].max());\n\n    /* step 1 */\n    UnionFind\
    \ uf[2];\n    uf[0] = contract(deg[0], k);\n    uf[1] = contract(deg[1], k);\n\
    \n    vector< int > id[2];\n    int ptr[] = {0, 0};\n    id[0] = vector< int >(L);\n\
    \    id[1] = vector< int >(R);\n    for(int i = 0; i < L; i++) if(uf[0].find(i)\
    \ == i) id[0][i] = ptr[0]++;\n    for(int i = 0; i < R; i++) if(uf[1].find(i)\
    \ == i) id[1][i] = ptr[1]++;\n\n    /* step 2 */\n    int N = max(ptr[0], ptr[1]);\n\
    \    deg[0] = valarray< int >(N);\n    deg[1] = valarray< int >(N);\n\n    /*\
    \ step 3 */\n    vector< int > C, D;\n    C.reserve(N * k);\n    D.reserve(N *\
    \ k);\n    for(int i = 0; i < (int) A.size(); i++) {\n      int u = id[0][uf[0].find(A[i])];\n\
    \      int v = id[1][uf[1].find(B[i])];\n      C.emplace_back(u);\n      D.emplace_back(v);\n\
    \      deg[0][u]++;\n      deg[1][v]++;\n    }\n    int j = 0;\n    for(int i\
    \ = 0; i < N; i++) {\n      while(deg[0][i] < k) {\n        while(deg[1][j] ==\
    \ k) ++j;\n        C.emplace_back(i);\n        D.emplace_back(j);\n        ++deg[0][i];\n\
    \        ++deg[1][j];\n      }\n    }\n\n    return {k, N, C, D};\n  }\n\n  void\
    \ rec(const vector< int > &ord, int k) {\n    if(k == 0) {\n      return;\n  \
    \  } else if(k == 1) {\n      ans.emplace_back(ord);\n      return;\n    } else\
    \ if((k & 1) == 0) {\n      EulerianTrail< false > et(g.n + g.n);\n      for(auto\
    \ &p : ord) et.add_edge(g.A[p], g.B[p] + g.n);\n      auto paths = et.enumerate_eulerian_trail();\n\
    \      vector< int > path;\n      for(auto &ps : paths) {\n        for(auto &e\
    \ : ps) path.emplace_back(ord[e]);\n      }\n      vector< int > beet[2];\n  \
    \    for(int i = 0; i < (int) path.size(); i++) {\n        beet[i & 1].emplace_back(path[i]);\n\
    \      }\n      rec(beet[0], k / 2);\n      rec(beet[1], k / 2);\n    } else {\n\
    \      BipartiteFlow flow(g.n, g.n);\n      for(auto &i : ord) flow.add_edge(g.A[i],\
    \ g.B[i]);\n      flow.max_matching();\n      vector< int > beet;\n      ans.emplace_back();\n\
    \      for(auto &i : ord) {\n        if(flow.match_l[g.A[i]] == g.B[i]) {\n  \
    \        flow.match_l[g.A[i]] = -1;\n          ans.back().emplace_back(i);\n \
    \       } else {\n          beet.emplace_back(i);\n        }\n      }\n      rec(beet,\
    \ k - 1);\n    }\n  }\n\npublic:\n  explicit BipariteGraphEdgeColoring() : L(0),\
    \ R(0) {}\n\n  void add_edge(int a, int b) {\n    A.emplace_back(a);\n    B.emplace_back(b);\n\
    \    L = max(L, a + 1);\n    R = max(R, b + 1);\n  }\n\n  vector< vector< int\
    \ > > build() {\n    g = build_k_regular_graph();\n    vector< int > ord(g.A.size());\n\
    \    iota(ord.begin(), ord.end(), 0);\n    rec(ord, g.k);\n    vector< vector<\
    \ int > > res;\n    for(int i = 0; i < (int) ans.size(); i++) {\n      res.emplace_back();\n\
    \      for(auto &j : ans[i]) if(j < (int)A.size()) res.back().emplace_back(j);\n\
    \    }\n    return res;\n  }\n};\n"
  code: "#pragma once\n/**\n * @brief Bipartite-Graph-Edge-Coloring(\u4E8C\u90E8\u30B0\
    \u30E9\u30D5\u306E\u8FBA\u5F69\u8272)\n * @see https://ei1333.hateblo.jp/entry/2020/08/25/015955\n\
    \ */\nstruct BipariteGraphEdgeColoring {\nprivate:\n  vector< vector< int > >\
    \ ans;\n  vector< int > A, B;\n  int L, R;\n\n  struct RegularGraph {\n    int\
    \ k{}, n{};\n    vector< int > A, B;\n  };\n  RegularGraph g;\n\n  static UnionFind\
    \ contract(valarray< int > &deg, int k) {\n    using pi = pair< int, int >;\n\
    \    priority_queue< pi, vector< pi >, greater<> > que;\n    for(int i = 0; i\
    \ < (int) deg.size(); i++) {\n      que.emplace(deg[i], i);\n    }\n    UnionFind\
    \ uf(deg.size());\n    while(que.size() > 1) {\n      auto p = que.top();\n  \
    \    que.pop();\n      auto q = que.top();\n      que.pop();\n      if(p.first\
    \ + q.first > k) continue;\n      p.first += q.first;\n      uf.unite(p.second,\
    \ q.second);\n      que.emplace(p);\n    }\n    return uf;\n  }\n\n\n  RegularGraph\
    \ build_k_regular_graph() {\n    valarray< int > deg[2];\n    deg[0] = valarray<\
    \ int >(L);\n    deg[1] = valarray< int >(R);\n    for(auto &p : A) deg[0][p]++;\n\
    \    for(auto &p : B) deg[1][p]++;\n\n    int k = max(deg[0].max(), deg[1].max());\n\
    \n    /* step 1 */\n    UnionFind uf[2];\n    uf[0] = contract(deg[0], k);\n \
    \   uf[1] = contract(deg[1], k);\n\n    vector< int > id[2];\n    int ptr[] =\
    \ {0, 0};\n    id[0] = vector< int >(L);\n    id[1] = vector< int >(R);\n    for(int\
    \ i = 0; i < L; i++) if(uf[0].find(i) == i) id[0][i] = ptr[0]++;\n    for(int\
    \ i = 0; i < R; i++) if(uf[1].find(i) == i) id[1][i] = ptr[1]++;\n\n    /* step\
    \ 2 */\n    int N = max(ptr[0], ptr[1]);\n    deg[0] = valarray< int >(N);\n \
    \   deg[1] = valarray< int >(N);\n\n    /* step 3 */\n    vector< int > C, D;\n\
    \    C.reserve(N * k);\n    D.reserve(N * k);\n    for(int i = 0; i < (int) A.size();\
    \ i++) {\n      int u = id[0][uf[0].find(A[i])];\n      int v = id[1][uf[1].find(B[i])];\n\
    \      C.emplace_back(u);\n      D.emplace_back(v);\n      deg[0][u]++;\n    \
    \  deg[1][v]++;\n    }\n    int j = 0;\n    for(int i = 0; i < N; i++) {\n   \
    \   while(deg[0][i] < k) {\n        while(deg[1][j] == k) ++j;\n        C.emplace_back(i);\n\
    \        D.emplace_back(j);\n        ++deg[0][i];\n        ++deg[1][j];\n    \
    \  }\n    }\n\n    return {k, N, C, D};\n  }\n\n  void rec(const vector< int >\
    \ &ord, int k) {\n    if(k == 0) {\n      return;\n    } else if(k == 1) {\n \
    \     ans.emplace_back(ord);\n      return;\n    } else if((k & 1) == 0) {\n \
    \     EulerianTrail< false > et(g.n + g.n);\n      for(auto &p : ord) et.add_edge(g.A[p],\
    \ g.B[p] + g.n);\n      auto paths = et.enumerate_eulerian_trail();\n      vector<\
    \ int > path;\n      for(auto &ps : paths) {\n        for(auto &e : ps) path.emplace_back(ord[e]);\n\
    \      }\n      vector< int > beet[2];\n      for(int i = 0; i < (int) path.size();\
    \ i++) {\n        beet[i & 1].emplace_back(path[i]);\n      }\n      rec(beet[0],\
    \ k / 2);\n      rec(beet[1], k / 2);\n    } else {\n      BipartiteFlow flow(g.n,\
    \ g.n);\n      for(auto &i : ord) flow.add_edge(g.A[i], g.B[i]);\n      flow.max_matching();\n\
    \      vector< int > beet;\n      ans.emplace_back();\n      for(auto &i : ord)\
    \ {\n        if(flow.match_l[g.A[i]] == g.B[i]) {\n          flow.match_l[g.A[i]]\
    \ = -1;\n          ans.back().emplace_back(i);\n        } else {\n          beet.emplace_back(i);\n\
    \        }\n      }\n      rec(beet, k - 1);\n    }\n  }\n\npublic:\n  explicit\
    \ BipariteGraphEdgeColoring() : L(0), R(0) {}\n\n  void add_edge(int a, int b)\
    \ {\n    A.emplace_back(a);\n    B.emplace_back(b);\n    L = max(L, a + 1);\n\
    \    R = max(R, b + 1);\n  }\n\n  vector< vector< int > > build() {\n    g = build_k_regular_graph();\n\
    \    vector< int > ord(g.A.size());\n    iota(ord.begin(), ord.end(), 0);\n  \
    \  rec(ord, g.k);\n    vector< vector< int > > res;\n    for(int i = 0; i < (int)\
    \ ans.size(); i++) {\n      res.emplace_back();\n      for(auto &j : ans[i]) if(j\
    \ < (int)A.size()) res.back().emplace_back(j);\n    }\n    return res;\n  }\n\
    };\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/bipartite-graph-edge-coloring.hpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-bipartite-edge-coloring.test.cpp
documentation_of: graph/others/bipartite-graph-edge-coloring.hpp
layout: document
redirect_from:
- /library/graph/others/bipartite-graph-edge-coloring.hpp
- /library/graph/others/bipartite-graph-edge-coloring.hpp.html
title: "Bipartite-Graph-Edge-Coloring(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\u8FBA\u5F69\
  \u8272)"
---
