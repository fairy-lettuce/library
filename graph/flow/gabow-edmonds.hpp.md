---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-general-matching.test.cpp
    title: test/verify/yosupo-general-matching.test.cpp
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/gabow-edmonds.md
    document_title: "Gabow Edmonds(\u4E00\u822C\u30B0\u30E9\u30D5\u306E\u6700\u5927\
      \u30DE\u30C3\u30C1\u30F3\u30B0)"
    links:
    - https://qiita.com/Kutimoti_T/items/5b579773e0a24d650bdf
  bundledCode: "#line 1 \"graph/flow/gabow-edmonds.hpp\"\n// https://qiita.com/Kutimoti_T/items/5b579773e0a24d650bdf\n\
    \n/**\n * @brief Gabow Edmonds(\u4E00\u822C\u30B0\u30E9\u30D5\u306E\u6700\u5927\
    \u30DE\u30C3\u30C1\u30F3\u30B0)\n * @docs docs/gabow-edmonds.md\n */\nstruct GabowEdmonds\
    \ {\n\n  struct edge {\n    int to, idx;\n  };\n\n  vector< vector< edge > > g;\n\
    \  vector< pair< int, int > > edges;\n  vector< int > mate, label, first;\n  queue<\
    \ int > que;\n\n  GabowEdmonds(int n) : g(n + 1), mate(n + 1), label(n + 1, -1),\
    \ first(n + 1) {}\n\n  void add_edge(int u, int v) {\n    ++u, ++v;\n    g[u].push_back((edge)\
    \ {v, (int) (edges.size() + g.size())});\n    g[v].push_back((edge) {u, (int)\
    \ (edges.size() + g.size())});\n    edges.emplace_back(u, v);\n  }\n\n  int find(int\
    \ x) {\n    if(label[first[x]] < 0) return first[x];\n    first[x] = find(first[x]);\n\
    \    return first[x];\n  }\n\n  void rematch(int v, int w) {\n    int t = mate[v];\n\
    \    mate[v] = w;\n    if(mate[t] != v) return;\n    if(label[v] < (int)g.size())\
    \ {\n      mate[t] = label[v];\n      rematch(label[v], t);\n    } else {\n  \
    \    int x = edges[label[v] - g.size()].first;\n      int y = edges[label[v] -\
    \ g.size()].second;\n      rematch(x, y);\n      rematch(y, x);\n    }\n  }\n\n\
    \  void assign_label(int x, int y, int num) {\n    int r = find(x);\n    int s\
    \ = find(y);\n    int join = 0;\n    if(r == s) return;\n    label[r] = -num;\n\
    \    label[s] = -num;\n    while(true) {\n      if(s != 0) swap(r, s);\n     \
    \ r = find(label[mate[r]]);\n      if(label[r] == -num) {\n        join = r;\n\
    \        break;\n      }\n      label[r] = -num;\n    }\n    int v = first[x];\n\
    \    while(v != join) {\n      que.push(v);\n      label[v] = num;\n      first[v]\
    \ = join;\n      v = first[label[mate[v]]];\n    }\n    v = first[y];\n    while(v\
    \ != join) {\n      que.push(v);\n      label[v] = num;\n      first[v] = join;\n\
    \      v = first[label[mate[v]]];\n    }\n  }\n\n  bool augment_check(int u) {\n\
    \    que = queue< int >();\n    first[u] = 0;\n    label[u] = 0;\n    que.push(u);\n\
    \    while(!que.empty()) {\n      int x = que.front();\n      que.pop();\n   \
    \   for(auto e : g[x]) {\n        int y = e.to;\n        if(mate[y] == 0 && y\
    \ != u) {\n          mate[y] = x;\n          rematch(x, y);\n          return\
    \ true;\n        } else if(label[y] >= 0) {\n          assign_label(x, y, e.idx);\n\
    \        } else if(label[mate[y]] < 0) {\n          label[mate[y]] = x;\n    \
    \      first[mate[y]] = y;\n          que.push(mate[y]);\n        }\n      }\n\
    \    }\n    return false;\n  }\n\n  vector< pair< int, int > > max_matching()\
    \ {\n    for(int i = 1; i < (int)g.size(); i++) {\n      if(mate[i] != 0) continue;\n\
    \      if(augment_check(i)) label.assign(g.size(), -1);\n    }\n    vector< pair<\
    \ int, int > > ret;\n    for(int i = 1; i < (int)g.size(); i++) {\n      if(i\
    \ < mate[i]) ret.emplace_back(i - 1, mate[i] - 1);\n    }\n    return ret;\n \
    \ }\n};\n"
  code: "// https://qiita.com/Kutimoti_T/items/5b579773e0a24d650bdf\n\n/**\n * @brief\
    \ Gabow Edmonds(\u4E00\u822C\u30B0\u30E9\u30D5\u306E\u6700\u5927\u30DE\u30C3\u30C1\
    \u30F3\u30B0)\n * @docs docs/gabow-edmonds.md\n */\nstruct GabowEdmonds {\n\n\
    \  struct edge {\n    int to, idx;\n  };\n\n  vector< vector< edge > > g;\n  vector<\
    \ pair< int, int > > edges;\n  vector< int > mate, label, first;\n  queue< int\
    \ > que;\n\n  GabowEdmonds(int n) : g(n + 1), mate(n + 1), label(n + 1, -1), first(n\
    \ + 1) {}\n\n  void add_edge(int u, int v) {\n    ++u, ++v;\n    g[u].push_back((edge)\
    \ {v, (int) (edges.size() + g.size())});\n    g[v].push_back((edge) {u, (int)\
    \ (edges.size() + g.size())});\n    edges.emplace_back(u, v);\n  }\n\n  int find(int\
    \ x) {\n    if(label[first[x]] < 0) return first[x];\n    first[x] = find(first[x]);\n\
    \    return first[x];\n  }\n\n  void rematch(int v, int w) {\n    int t = mate[v];\n\
    \    mate[v] = w;\n    if(mate[t] != v) return;\n    if(label[v] < (int)g.size())\
    \ {\n      mate[t] = label[v];\n      rematch(label[v], t);\n    } else {\n  \
    \    int x = edges[label[v] - g.size()].first;\n      int y = edges[label[v] -\
    \ g.size()].second;\n      rematch(x, y);\n      rematch(y, x);\n    }\n  }\n\n\
    \  void assign_label(int x, int y, int num) {\n    int r = find(x);\n    int s\
    \ = find(y);\n    int join = 0;\n    if(r == s) return;\n    label[r] = -num;\n\
    \    label[s] = -num;\n    while(true) {\n      if(s != 0) swap(r, s);\n     \
    \ r = find(label[mate[r]]);\n      if(label[r] == -num) {\n        join = r;\n\
    \        break;\n      }\n      label[r] = -num;\n    }\n    int v = first[x];\n\
    \    while(v != join) {\n      que.push(v);\n      label[v] = num;\n      first[v]\
    \ = join;\n      v = first[label[mate[v]]];\n    }\n    v = first[y];\n    while(v\
    \ != join) {\n      que.push(v);\n      label[v] = num;\n      first[v] = join;\n\
    \      v = first[label[mate[v]]];\n    }\n  }\n\n  bool augment_check(int u) {\n\
    \    que = queue< int >();\n    first[u] = 0;\n    label[u] = 0;\n    que.push(u);\n\
    \    while(!que.empty()) {\n      int x = que.front();\n      que.pop();\n   \
    \   for(auto e : g[x]) {\n        int y = e.to;\n        if(mate[y] == 0 && y\
    \ != u) {\n          mate[y] = x;\n          rematch(x, y);\n          return\
    \ true;\n        } else if(label[y] >= 0) {\n          assign_label(x, y, e.idx);\n\
    \        } else if(label[mate[y]] < 0) {\n          label[mate[y]] = x;\n    \
    \      first[mate[y]] = y;\n          que.push(mate[y]);\n        }\n      }\n\
    \    }\n    return false;\n  }\n\n  vector< pair< int, int > > max_matching()\
    \ {\n    for(int i = 1; i < (int)g.size(); i++) {\n      if(mate[i] != 0) continue;\n\
    \      if(augment_check(i)) label.assign(g.size(), -1);\n    }\n    vector< pair<\
    \ int, int > > ret;\n    for(int i = 1; i < (int)g.size(); i++) {\n      if(i\
    \ < mate[i]) ret.emplace_back(i - 1, mate[i] - 1);\n    }\n    return ret;\n \
    \ }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/flow/gabow-edmonds.hpp
  requiredBy: []
  timestamp: '2021-07-16 00:30:06+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-general-matching.test.cpp
documentation_of: graph/flow/gabow-edmonds.hpp
layout: document
redirect_from:
- /library/graph/flow/gabow-edmonds.hpp
- /library/graph/flow/gabow-edmonds.hpp.html
title: "Gabow Edmonds(\u4E00\u822C\u30B0\u30E9\u30D5\u306E\u6700\u5927\u30DE\u30C3\
  \u30C1\u30F3\u30B0)"
---
## 概要

一般グラフの最大マッチングを, GabowのEdmonds' Algorithmによって求める。

グラフ $G=(V, E)$ において, $M$ が $E$ の部分集合でかつ $M$ のどの $2$ 辺も共通の端点をもたないとき, $M$ を $G$ のマッチングといい, 辺の本数が最大であるマッチングを最大マッチングという.

## 使い方

* `GabowEdmonds(n)`: 頂点数 `n` で初期化する
* `add_edge(u, v)`: 頂点 `u`, `v` 間に無向辺を張る
* `max_matching()`: 最大マッチングを求め, その辺集合を返す.

## 計算量

* $O(VE \log V)$
