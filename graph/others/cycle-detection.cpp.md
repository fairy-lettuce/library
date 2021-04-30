---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: graph/graph-template.cpp
    title: graph/graph-template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-cycle-detection.test.cpp
    title: test/verify/yosupo-cycle-detection.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/cycle-detection.md
    document_title: "Cycle-Detection(\u9589\u8DEF\u691C\u51FA)"
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
    \ Edge< T > >;\n#line 2 \"graph/others/cycle-detection.cpp\"\n\n/**\n * @brief\
    \ Cycle-Detection(\u9589\u8DEF\u691C\u51FA)\n * @docs docs/cycle-detection.md\n\
    \ */\ntemplate< typename T = int >\nstruct CycleDetection : Graph< T > {\n   \
    \ using Graph< T >::Graph;\n    using Graph< T >::g;\n\n    vector< int > used;\n\
    \    Edges< T > pre, cyrcle;\n\n    bool dfs(int idx) {\n        used[idx] = 1;\n\
    \        for(auto& e : g[idx]) {\n            if(used[e] == 0) {\n           \
    \     pre[e] = e;\n                if(dfs(e)) return true;\n            } else\
    \ if(used[e] == 1) {\n                int cur = idx;\n                while(cur\
    \ != e) {\n                    cyrcle.emplace_back(pre[cur]);\n              \
    \      cur = pre[cur].from;\n                }\n                cyrcle.emplace_back(e);\n\
    \                return true;\n            }\n        }\n\n        used[idx] =\
    \ 2;\n        return false;\n    }\n    Edges< T > build() {\n        used.assign(g.size(),\
    \ 0);\n        pre.resize(g.size());\n        for(int i = 0; i < (int)g.size();\
    \ i++) {\n            if(used[i] == 0 && dfs(i)) {\n                reverse(begin(cyrcle),\
    \ end(cyrcle));\n                return cyrcle;\n            }\n        }\n  \
    \      return {};\n    }\n};\n"
  code: "#include \"../graph-template.cpp\"\n\n/**\n * @brief Cycle-Detection(\u9589\
    \u8DEF\u691C\u51FA)\n * @docs docs/cycle-detection.md\n */\ntemplate< typename\
    \ T = int >\nstruct CycleDetection : Graph< T > {\n    using Graph< T >::Graph;\n\
    \    using Graph< T >::g;\n\n    vector< int > used;\n    Edges< T > pre, cyrcle;\n\
    \n    bool dfs(int idx) {\n        used[idx] = 1;\n        for(auto& e : g[idx])\
    \ {\n            if(used[e] == 0) {\n                pre[e] = e;\n           \
    \     if(dfs(e)) return true;\n            } else if(used[e] == 1) {\n       \
    \         int cur = idx;\n                while(cur != e) {\n                \
    \    cyrcle.emplace_back(pre[cur]);\n                    cur = pre[cur].from;\n\
    \                }\n                cyrcle.emplace_back(e);\n                return\
    \ true;\n            }\n        }\n\n        used[idx] = 2;\n        return false;\n\
    \    }\n    Edges< T > build() {\n        used.assign(g.size(), 0);\n        pre.resize(g.size());\n\
    \        for(int i = 0; i < (int)g.size(); i++) {\n            if(used[i] == 0\
    \ && dfs(i)) {\n                reverse(begin(cyrcle), end(cyrcle));\n       \
    \         return cyrcle;\n            }\n        }\n        return {};\n    }\n\
    };\n"
  dependsOn:
  - graph/graph-template.cpp
  isVerificationFile: false
  path: graph/others/cycle-detection.cpp
  requiredBy: []
  timestamp: '2020-09-30 18:06:49+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-cycle-detection.test.cpp
documentation_of: graph/others/cycle-detection.cpp
layout: document
redirect_from:
- /library/graph/others/cycle-detection.cpp
- /library/graph/others/cycle-detection.cpp.html
title: "Cycle-Detection(\u9589\u8DEF\u691C\u51FA)"
---
## 概要

有向グラフが与えられたとき, 辺素なサイクルを $1$ つみつける.

適当な頂点から DFS すると見つけられる.

## 使い方

* `build()`: 辺素なサイクルを $1$ つ見つけて返す. ただし, 見つからなかったとき空列を返す.

## 計算量

$O(E + V)$
