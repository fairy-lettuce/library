---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"structure/union-find/bipartite-graph.cpp\"\nstruct BipartiteGraph\
    \ : UnionFind\n{\n  vector< int > color;\n\n  BipartiteGraph(int v) : color(v\
    \ + v, -1), UnionFind(v + v) {}\n\n  bool bipartite_graph_coloring()\n  {\n  \
    \  for(int i = 0; i < color.size() / 2; i++) {\n      int a = find(i);\n     \
    \ int b = find(i + (int) color.size() / 2);\n      if(a == b) return (false);\n\
    \      if(color[a] < 0) color[a] = 0, color[b] = 1;\n    }\n    return (true);\n\
    \  }\n\n  bool operator[](int k)\n  {\n    return (bool(color[find(k)]));\n  }\n\
    };\n"
  code: "struct BipartiteGraph : UnionFind\n{\n  vector< int > color;\n\n  BipartiteGraph(int\
    \ v) : color(v + v, -1), UnionFind(v + v) {}\n\n  bool bipartite_graph_coloring()\n\
    \  {\n    for(int i = 0; i < color.size() / 2; i++) {\n      int a = find(i);\n\
    \      int b = find(i + (int) color.size() / 2);\n      if(a == b) return (false);\n\
    \      if(color[a] < 0) color[a] = 0, color[b] = 1;\n    }\n    return (true);\n\
    \  }\n\n  bool operator[](int k)\n  {\n    return (bool(color[find(k)]));\n  }\n\
    };\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/union-find/bipartite-graph.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/union-find/bipartite-graph.cpp
layout: document
redirect_from:
- /library/structure/union-find/bipartite-graph.cpp
- /library/structure/union-find/bipartite-graph.cpp.html
title: structure/union-find/bipartite-graph.cpp
---
