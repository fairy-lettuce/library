---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-2306.test.cpp
    title: test/verify/aoj-2306.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    _deprecated_at_docs: docs/enumerate-cliques.md
    document_title: "Enumerate-Cliques(\u30AF\u30EA\u30FC\u30AF\u5168\u5217\u6319)"
    links:
    - https://www.slideshare.net/wata_orz/ss-12131479
  bundledCode: "#line 1 \"graph/others/enumerate-cliques.cpp\"\n/**\n * @brief Enumerate-Cliques(\u30AF\
    \u30EA\u30FC\u30AF\u5168\u5217\u6319)\n * @see https://www.slideshare.net/wata_orz/ss-12131479\n\
    \ * @docs docs/enumerate-cliques.md\n */\nvector< vector< int > > enumerate_cliques(Matrix<\
    \ bool > g) {\n\n  int N = (int) g.size(), M = 0;\n  vector< int > deg(N);\n \
    \ vector< vector< int > > edge(N, vector< int >(N));\n  for(int i = 0; i < N;\
    \ i++) {\n    for(auto p : g[i]) deg[i] += p;\n    M += deg[i];\n  }\n  int lim\
    \ = (int) sqrt(M);\n\n  vector< vector< int > > cliques;\n\n  auto add_clique\
    \ = [&](const vector< int > &rem, bool last) {\n    vector< int > neighbor((int)\
    \ rem.size() - last);\n    for(int i = 0; i < (int) neighbor.size(); i++) {\n\
    \      for(int j = 0; j < (int) neighbor.size(); j++) {\n        if(i != j &&\
    \ !g[rem[i]][rem[j]]) neighbor[i] |= 1 << j;\n      }\n    }\n    for(int i =\
    \ 1 - last; i < (1 << neighbor.size()); i++) {\n      bool ok = true;\n      for(int\
    \ j = 0; j < neighbor.size(); j++) {\n        if((i >> j) & 1) {\n          if(i\
    \ & neighbor[j]) {\n            ok = false;\n            break;\n          }\n\
    \        }\n      }\n      if(ok) {\n        vector< int > clique;\n        if(last)\
    \ clique.emplace_back(rem.back());\n        for(int j = 0; j < neighbor.size();\
    \ j++) {\n          if((i >> j) & 1) clique.emplace_back(rem[j]);\n        }\n\
    \        cliques.emplace_back(clique);\n      }\n    }\n  };\n\n  vector< int\
    \ > used(N);\n  queue< int > que;\n  for(int i = 0; i < N; i++) {\n    if(deg[i]\
    \ < lim) {\n      used[i] = true;\n      que.emplace(i);\n    }\n  }\n  while(!que.empty())\
    \ {\n    int idx = que.front();\n    que.pop();\n    vector< int > rem;\n    for(int\
    \ k = 0; k < N; k++) {\n      if(g[idx][k]) rem.emplace_back(k);\n    }\n    rem.emplace_back(idx);\n\
    \    add_clique(rem, true);\n    used[idx] = true;\n    for(int k = 0; k < N;\
    \ k++) {\n      if(g[idx][k]) {\n        g[idx][k] = false;\n        g[k][idx]\
    \ = false;\n        --deg[k];\n        if(!used[k] && deg[k] < lim) {\n      \
    \    used[k] = true;\n          que.emplace(k);\n        }\n      }\n    }\n \
    \ }\n  vector< int > rem;\n  for(int i = 0; i < N; i++) {\n    if(!used[i]) rem.emplace_back(i);\n\
    \  }\n  add_clique(rem, false);\n  return cliques;\n}\n"
  code: "/**\n * @brief Enumerate-Cliques(\u30AF\u30EA\u30FC\u30AF\u5168\u5217\u6319\
    )\n * @see https://www.slideshare.net/wata_orz/ss-12131479\n * @docs docs/enumerate-cliques.md\n\
    \ */\nvector< vector< int > > enumerate_cliques(Matrix< bool > g) {\n\n  int N\
    \ = (int) g.size(), M = 0;\n  vector< int > deg(N);\n  vector< vector< int > >\
    \ edge(N, vector< int >(N));\n  for(int i = 0; i < N; i++) {\n    for(auto p :\
    \ g[i]) deg[i] += p;\n    M += deg[i];\n  }\n  int lim = (int) sqrt(M);\n\n  vector<\
    \ vector< int > > cliques;\n\n  auto add_clique = [&](const vector< int > &rem,\
    \ bool last) {\n    vector< int > neighbor((int) rem.size() - last);\n    for(int\
    \ i = 0; i < (int) neighbor.size(); i++) {\n      for(int j = 0; j < (int) neighbor.size();\
    \ j++) {\n        if(i != j && !g[rem[i]][rem[j]]) neighbor[i] |= 1 << j;\n  \
    \    }\n    }\n    for(int i = 1 - last; i < (1 << neighbor.size()); i++) {\n\
    \      bool ok = true;\n      for(int j = 0; j < neighbor.size(); j++) {\n   \
    \     if((i >> j) & 1) {\n          if(i & neighbor[j]) {\n            ok = false;\n\
    \            break;\n          }\n        }\n      }\n      if(ok) {\n       \
    \ vector< int > clique;\n        if(last) clique.emplace_back(rem.back());\n \
    \       for(int j = 0; j < neighbor.size(); j++) {\n          if((i >> j) & 1)\
    \ clique.emplace_back(rem[j]);\n        }\n        cliques.emplace_back(clique);\n\
    \      }\n    }\n  };\n\n  vector< int > used(N);\n  queue< int > que;\n  for(int\
    \ i = 0; i < N; i++) {\n    if(deg[i] < lim) {\n      used[i] = true;\n      que.emplace(i);\n\
    \    }\n  }\n  while(!que.empty()) {\n    int idx = que.front();\n    que.pop();\n\
    \    vector< int > rem;\n    for(int k = 0; k < N; k++) {\n      if(g[idx][k])\
    \ rem.emplace_back(k);\n    }\n    rem.emplace_back(idx);\n    add_clique(rem,\
    \ true);\n    used[idx] = true;\n    for(int k = 0; k < N; k++) {\n      if(g[idx][k])\
    \ {\n        g[idx][k] = false;\n        g[k][idx] = false;\n        --deg[k];\n\
    \        if(!used[k] && deg[k] < lim) {\n          used[k] = true;\n         \
    \ que.emplace(k);\n        }\n      }\n    }\n  }\n  vector< int > rem;\n  for(int\
    \ i = 0; i < N; i++) {\n    if(!used[i]) rem.emplace_back(i);\n  }\n  add_clique(rem,\
    \ false);\n  return cliques;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/enumerate-cliques.cpp
  requiredBy: []
  timestamp: '2020-10-14 14:38:29+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-2306.test.cpp
documentation_of: graph/others/enumerate-cliques.cpp
layout: document
redirect_from:
- /library/graph/others/enumerate-cliques.cpp
- /library/graph/others/enumerate-cliques.cpp.html
title: "Enumerate-Cliques(\u30AF\u30EA\u30FC\u30AF\u5168\u5217\u6319)"
---
## 概要

無向グラフが与えられたとき, クリークを全列挙する.

次数が $\sqrt {2E}$ 未満の頂点 $v$ を $1$ 個選んで, 頂点 $v$ に隣接する頂点の部分集合を全て試し, $v$ を除去して再帰的に求める.

クリークの個数は高々 $2 ^ {\sqrt {2E}}$ 個.

## 使い方

* `enumerate_clique(g)`: 隣接行列 `g` の部分グラフに含まれる全てのクリークを返す. 頂点数 $1$ もクリークとしてみなしている.

## 計算量

$O(2 ^ {\sqrt {2E}} V)$
