---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-7-a.test.cpp
    title: test/verify/aoj-grl-7-a.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/bipartite-matching.md
    document_title: "Bipartite-Matching(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\u6700\
      \u5927\u30DE\u30C3\u30C1\u30F3\u30B0)"
    links: []
  bundledCode: "#line 1 \"graph/flow/bipartite-matching.hpp\"\n/**\n * @brief Bipartite-Matching(\u4E8C\
    \u90E8\u30B0\u30E9\u30D5\u306E\u6700\u5927\u30DE\u30C3\u30C1\u30F3\u30B0)\n *\
    \ @docs docs/bipartite-matching.md\n */\nstruct BipartiteMatching {\n  vector<\
    \ vector< int > > graph;\n  vector< int > alive, used, match;\n  int timestamp;\n\
    \n  explicit BipartiteMatching(int n) : graph(n), alive(n, 1), used(n, 0), match(n,\
    \ -1), timestamp(0) {}\n\n  void add_edge(int u, int v) {\n    graph[u].push_back(v);\n\
    \    graph[v].push_back(u);\n  }\n\n  bool augment(int idx) {\n    used[idx] =\
    \ timestamp;\n    for(auto &to : graph[idx]) {\n      int to_match = match[to];\n\
    \      if(alive[to] == 0) continue;\n      if(to_match == -1 || (used[to_match]\
    \ != timestamp && augment(to_match))) {\n        match[idx] = to;\n        match[to]\
    \ = idx;\n        return true;\n      }\n    }\n    return false;\n  }\n\n  int\
    \ bipartite_matching() {\n    int ret = 0;\n    for(int i = 0; i < (int) graph.size();\
    \ i++) {\n      if(alive[i] == 0) continue;\n      if(match[i] == -1) {\n    \
    \    ++timestamp;\n        ret += augment(i);\n      }\n    }\n    return ret;\n\
    \  }\n\n  int add_vertex(int idx) {\n    alive[idx] = 1;\n    ++timestamp;\n \
    \   return augment(idx);\n  }\n\n  int erase_vertex(int idx) {\n    alive[idx]\
    \ = 0;\n    if(match[idx] == -1) {\n      return 0;\n    }\n    match[match[idx]]\
    \ = -1;\n    ++timestamp;\n    int ret = augment(match[idx]);\n    match[idx]\
    \ = -1;\n    return ret - 1;\n  }\n\n  void output() const {\n    for(int i =\
    \ 0; i < (int) graph.size(); i++) {\n      if(i < match[i]) {\n        cout <<\
    \ i << \"-\" << match[i] << endl;\n      }\n    }\n  }\n};\n"
  code: "/**\n * @brief Bipartite-Matching(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\u6700\
    \u5927\u30DE\u30C3\u30C1\u30F3\u30B0)\n * @docs docs/bipartite-matching.md\n */\n\
    struct BipartiteMatching {\n  vector< vector< int > > graph;\n  vector< int >\
    \ alive, used, match;\n  int timestamp;\n\n  explicit BipartiteMatching(int n)\
    \ : graph(n), alive(n, 1), used(n, 0), match(n, -1), timestamp(0) {}\n\n  void\
    \ add_edge(int u, int v) {\n    graph[u].push_back(v);\n    graph[v].push_back(u);\n\
    \  }\n\n  bool augment(int idx) {\n    used[idx] = timestamp;\n    for(auto &to\
    \ : graph[idx]) {\n      int to_match = match[to];\n      if(alive[to] == 0) continue;\n\
    \      if(to_match == -1 || (used[to_match] != timestamp && augment(to_match)))\
    \ {\n        match[idx] = to;\n        match[to] = idx;\n        return true;\n\
    \      }\n    }\n    return false;\n  }\n\n  int bipartite_matching() {\n    int\
    \ ret = 0;\n    for(int i = 0; i < (int) graph.size(); i++) {\n      if(alive[i]\
    \ == 0) continue;\n      if(match[i] == -1) {\n        ++timestamp;\n        ret\
    \ += augment(i);\n      }\n    }\n    return ret;\n  }\n\n  int add_vertex(int\
    \ idx) {\n    alive[idx] = 1;\n    ++timestamp;\n    return augment(idx);\n  }\n\
    \n  int erase_vertex(int idx) {\n    alive[idx] = 0;\n    if(match[idx] == -1)\
    \ {\n      return 0;\n    }\n    match[match[idx]] = -1;\n    ++timestamp;\n \
    \   int ret = augment(match[idx]);\n    match[idx] = -1;\n    return ret - 1;\n\
    \  }\n\n  void output() const {\n    for(int i = 0; i < (int) graph.size(); i++)\
    \ {\n      if(i < match[i]) {\n        cout << i << \"-\" << match[i] << endl;\n\
    \      }\n    }\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/bipartite-matching.hpp
  requiredBy: []
  timestamp: '2021-08-16 02:34:50+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-7-a.test.cpp
documentation_of: graph/flow/bipartite-matching.hpp
layout: document
redirect_from:
- /library/graph/flow/bipartite-matching.hpp
- /library/graph/flow/bipartite-matching.hpp.html
title: "Bipartite-Matching(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\u6700\u5927\u30DE\u30C3\
  \u30C1\u30F3\u30B0)"
---
## 概要

グラフ $G=(V, E)$ において, $V$ が $2$ つの部分集合 $X$ と $Y$ に分割され, $E$ のどの辺も一方の端点は $X$ に, もう一方の端点は $Y$ に属しているとき, $G$ を二部グラフという.

グラフ $G=(V, E)$ において, $M$ が $E$ の部分集合でかつ $M$ のどの $2$ 辺も共通の端点をもたないとき, $M$ を $G$ のマッチングといい, 辺の本数が最大であるマッチングを最大マッチングという.

ここでは, 二部グラフの最大マッチングを最大流のアルゴリズムを利用して求める.

* `BipartiteMatching(n)`:= 全体のグラフの頂点数を `n` で初期化する.
* `add_edge(u, v)`:= 頂点 `u`, `v` 間に辺を張る.
* `bipartite_matching()`:= 二部グラフの最大マッチングを返す.
* `add_vertex(idx)`:= 頂点 `idx` を追加し, フローの変化量を返す($0$ または $1$).
* `erase_vertex(idx)`:= 頂点 `idx` を削除し, フローの変化量を返す($0$ または $-1$).
* `output()`:= マッチングに使った辺を出力する.

## 計算量

* $O(V E)$
