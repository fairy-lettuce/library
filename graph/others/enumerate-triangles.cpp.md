---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.cpp
    title: graph/graph-template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-enumerate-triangles.test.cpp
    title: test/verify/yosupo-enumerate-triangles.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Enumerate-Triangles(\u4E09\u89D2\u5F62\u5168\u5217\u6319)"
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
    \ Edge< T > >;\n#line 2 \"graph/others/enumerate-triangles.cpp\"\n\n/**\n * @brief\
    \ Enumerate-Triangles(\u4E09\u89D2\u5F62\u5168\u5217\u6319)\n */\ntemplate< typename\
    \ T >\nvector< tuple< int, int, int > > enumerate_triangles(const Graph< T >&\
    \ g) {\n    int N = (int)g.size();\n    using pi = pair< int, int >;\n    vector<\
    \ pi > vp(N);\n    for(int i = 0; i < N; i++) {\n        vp[i] = {(int)g.g[i].size(),\
    \ i};\n    }\n    vector< vector< int > > h(N);\n    for(int i = 0; i < N; i++)\
    \ {\n        for(auto& j : g.g[i]) {\n            if(vp[i] > vp[j]) {\n      \
    \          h[i].emplace_back(j);\n            }\n        }\n    }\n    vector<\
    \ tuple< int, int, int > > triangle;\n    vector< int > used(N);\n    for(int\
    \ x = 0; x < N; x++) {\n        for(int z : h[x]) used[z] = true;\n        for(int\
    \ y : h[x]) {\n            for(int z : h[y]) {\n                if(used[z]) triangle.emplace_back(x,\
    \ y, z);\n            }\n        }\n        for(int z : h[x]) used[z] = false;\n\
    \    }\n\n    return triangle;\n}\n"
  code: "#include \"../graph-template.cpp\"\n\n/**\n * @brief Enumerate-Triangles(\u4E09\
    \u89D2\u5F62\u5168\u5217\u6319)\n */\ntemplate< typename T >\nvector< tuple< int,\
    \ int, int > > enumerate_triangles(const Graph< T >& g) {\n    int N = (int)g.size();\n\
    \    using pi = pair< int, int >;\n    vector< pi > vp(N);\n    for(int i = 0;\
    \ i < N; i++) {\n        vp[i] = {(int)g.g[i].size(), i};\n    }\n    vector<\
    \ vector< int > > h(N);\n    for(int i = 0; i < N; i++) {\n        for(auto& j\
    \ : g.g[i]) {\n            if(vp[i] > vp[j]) {\n                h[i].emplace_back(j);\n\
    \            }\n        }\n    }\n    vector< tuple< int, int, int > > triangle;\n\
    \    vector< int > used(N);\n    for(int x = 0; x < N; x++) {\n        for(int\
    \ z : h[x]) used[z] = true;\n        for(int y : h[x]) {\n            for(int\
    \ z : h[y]) {\n                if(used[z]) triangle.emplace_back(x, y, z);\n \
    \           }\n        }\n        for(int z : h[x]) used[z] = false;\n    }\n\n\
    \    return triangle;\n}\n"
  dependsOn:
  - graph/graph-template.cpp
  isVerificationFile: false
  path: graph/others/enumerate-triangles.cpp
  requiredBy: []
  timestamp: '2020-09-29 21:06:38+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-enumerate-triangles.test.cpp
documentation_of: graph/others/enumerate-triangles.cpp
layout: document
redirect_from:
- /library/graph/others/enumerate-triangles.cpp
- /library/graph/others/enumerate-triangles.cpp.html
title: "Enumerate-Triangles(\u4E09\u89D2\u5F62\u5168\u5217\u6319)"
---
