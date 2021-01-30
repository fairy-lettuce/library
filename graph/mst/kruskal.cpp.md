---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.cpp
    title: graph/graph-template.cpp
  - icon: ':heavy_check_mark:'
    path: structure/union-find/union-find.cpp
    title: Union-Find
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-2-a-2.test.cpp
    title: test/verify/aoj-grl-2-a-2.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-manhattanmst.test.cpp
    title: test/verify/yosupo-manhattanmst.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/kruskal.md
    document_title: "Kruskal(\u6700\u5C0F\u5168\u57DF\u6728)"
    links: []
  bundledCode: "#line 2 \"graph/graph-template.cpp\"\n\ntemplate< typename T = int\
    \ >\nstruct Edge {\n  int from, to;\n  T cost;\n  int idx;\n\n  Edge() = default;\n\
    \n  Edge(int from, int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost),\
    \ idx(idx) {}\n\n  operator int() const { return to; }\n};\n\ntemplate< typename\
    \ T = int >\nstruct Graph {\n  vector< vector< Edge< T > > > g;\n  int es;\n\n\
    \  Graph() = default;\n\n  explicit Graph(int n) : g(n), es(0) {}\n\n  size_t\
    \ size() const {\n    return g.size();\n  }\n\n  void add_directed_edge(int from,\
    \ int to, T cost = 1) {\n    g[from].emplace_back(from, to, cost, es++);\n  }\n\
    \n  void add_edge(int from, int to, T cost = 1) {\n    g[from].emplace_back(from,\
    \ to, cost, es);\n    g[to].emplace_back(to, from, cost, es++);\n  }\n\n  void\
    \ read(int M, int padding = -1, bool weighted = false, bool directed = false)\
    \ {\n    for(int i = 0; i < M; i++) {\n      int a, b;\n      cin >> a >> b;\n\
    \      a += padding;\n      b += padding;\n      T c = T(1);\n      if(weighted)\
    \ cin >> c;\n      if(directed) add_directed_edge(a, b, c);\n      else add_edge(a,\
    \ b, c);\n    }\n  }\n};\n\ntemplate< typename T = int >\nusing Edges = vector<\
    \ Edge< T > >;\n#line 1 \"structure/union-find/union-find.cpp\"\n/**\n * @brief\
    \ Union-Find\n * @docs docs/union-find.md\n */\nstruct UnionFind {\n  vector<\
    \ int > data;\n\n  UnionFind() = default;\n\n  explicit UnionFind(size_t sz) :\
    \ data(sz, -1) {}\n\n  bool unite(int x, int y) {\n    x = find(x), y = find(y);\n\
    \    if(x == y) return false;\n    if(data[x] > data[y]) swap(x, y);\n    data[x]\
    \ += data[y];\n    data[y] = x;\n    return true;\n  }\n\n  int find(int k) {\n\
    \    if(data[k] < 0) return (k);\n    return data[k] = find(data[k]);\n  }\n\n\
    \  int size(int k) {\n    return -data[find(k)];\n  }\n\n  bool same(int x, int\
    \ y) {\n    return find(x) == find(y);\n  }\n};\n#line 3 \"graph/mst/kruskal.cpp\"\
    \n\n/**\n * @brief Kruskal(\u6700\u5C0F\u5168\u57DF\u6728)\n * @docs docs/kruskal.md\n\
    \ */\ntemplate< typename T >\nstruct MinimumSpanningTree {\n  T cost;\n  Edges<\
    \ T > edges;\n};\n\ntemplate< typename T >\nMinimumSpanningTree< T > kruskal(Edges<\
    \ T > &edges, int V) {\n  sort(begin(edges), end(edges), [](const Edge< T > &a,\
    \ const Edge< T > &b) {\n    return a.cost < b.cost;\n  });\n  UnionFind tree(V);\n\
    \  T total = T();\n  Edges< T > es;\n  for(auto &e : edges) {\n    if(tree.unite(e.from,\
    \ e.to)) {\n      es.emplace_back(e);\n      total += e.cost;\n    }\n  }\n  return\
    \ {total, es};\n}\n"
  code: "#include \"../graph-template.cpp\"\n#include \"../../structure/union-find/union-find.cpp\"\
    \n\n/**\n * @brief Kruskal(\u6700\u5C0F\u5168\u57DF\u6728)\n * @docs docs/kruskal.md\n\
    \ */\ntemplate< typename T >\nstruct MinimumSpanningTree {\n  T cost;\n  Edges<\
    \ T > edges;\n};\n\ntemplate< typename T >\nMinimumSpanningTree< T > kruskal(Edges<\
    \ T > &edges, int V) {\n  sort(begin(edges), end(edges), [](const Edge< T > &a,\
    \ const Edge< T > &b) {\n    return a.cost < b.cost;\n  });\n  UnionFind tree(V);\n\
    \  T total = T();\n  Edges< T > es;\n  for(auto &e : edges) {\n    if(tree.unite(e.from,\
    \ e.to)) {\n      es.emplace_back(e);\n      total += e.cost;\n    }\n  }\n  return\
    \ {total, es};\n}\n"
  dependsOn:
  - graph/graph-template.cpp
  - structure/union-find/union-find.cpp
  isVerificationFile: false
  path: graph/mst/kruskal.cpp
  requiredBy: []
  timestamp: '2020-09-16 23:08:58+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-2-a-2.test.cpp
  - test/verify/yosupo-manhattanmst.test.cpp
documentation_of: graph/mst/kruskal.cpp
layout: document
redirect_from:
- /library/graph/mst/kruskal.cpp
- /library/graph/mst/kruskal.cpp.html
title: "Kruskal(\u6700\u5C0F\u5168\u57DF\u6728)"
---
## 概要

最小全域木(全域木のうち, その辺群の重みの総和が最小になる木)を求める. Union-Findを用いて辺集合にある辺を加えて閉路を作らないか判定しながら, 辺を重みが小さい順に走査する.

* `kruskal(edges, V)`: `V` 頂点の連結な重み付き辺集合 `edges` からなる重み付き連結グラフの最小全域木を求める. `cost` には辺の重みの総和, `edges` にはそれを構成する辺が格納される.

## 計算量

* $O(E \log V)$
