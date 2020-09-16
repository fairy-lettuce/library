---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yukicoder-583.test.cpp
    title: test/verify/yukicoder-583.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bipartite-edge-coloring.test.cpp
    title: test/verify/yosupo-bipartite-edge-coloring.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    _deprecated_at_docs: docs/eulerian-trail.md
    document_title: "Eulerian-Trail(\u30AA\u30A4\u30E9\u30FC\u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/others/eulerian-trail.cpp\"\n/**\n * @brief Eulerian-Trail(\u30AA\
    \u30A4\u30E9\u30FC\u8DEF)\n * @docs docs/eulerian-trail.md\n */\ntemplate< bool\
    \ directed >\nstruct EulerianTrail {\n  vector< vector< pair< int, int > > > g;\n\
    \  vector< pair< int, int > > es;\n  int M;\n  vector< int > used_vertex, used_edge,\
    \ deg;\n\n  explicit EulerianTrail(int V) : g(V), M(0), deg(V), used_vertex(V)\
    \ {}\n\n  void add_edge(int a, int b) {\n    es.emplace_back(a, b);\n    g[a].emplace_back(b,\
    \ M);\n    if(directed) {\n      deg[a]++;\n      deg[b]--;\n    } else {\n  \
    \    g[b].emplace_back(a, M);\n      deg[a]++;\n      deg[b]++;\n    }\n    M++;\n\
    \  }\n\n  pair< int, int > get_edge(int idx) const {\n    return es[idx];\n  }\n\
    \n  vector< vector< int > > enumerate_eulerian_trail() {\n    if(directed) {\n\
    \      for(auto &p : deg) if(p != 0) return {};\n    } else {\n      for(auto\
    \ &p : deg) if(p & 1) return {};\n    }\n    used_edge.assign(M, 0);\n    vector<\
    \ vector< int > > ret;\n    for(int i = 0; i < (int) g.size(); i++) {\n      if(g[i].empty()\
    \ || used_vertex[i]) continue;\n      ret.emplace_back(go(i));\n    }\n    return\
    \ ret;\n  }\n\n  vector< vector< int > > enumerate_semi_eulerian_trail() {\n \
    \   UnionFind uf(g.size());\n    for(auto &p : es) uf.unite(p.first, p.second);\n\
    \    vector< vector< int > > group(g.size());\n    for(int i = 0; i < (int) g.size();\
    \ i++) group[uf.find(i)].emplace_back(i);\n    vector< vector< int > > ret;\n\
    \    used_edge.assign(M, 0);\n    for(auto &vs : group) {\n      if(vs.empty())\
    \ continue;\n      int latte = -1, malta = -1;\n      if(directed) {\n       \
    \ for(auto &p : vs) {\n          if(abs(deg[p]) > 1) {\n            return {};\n\
    \          } else if(deg[p] == 1) {\n            if(latte >= 0) return {};\n \
    \           latte = p;\n          }\n        }\n      } else {\n        for(auto\
    \ &p : vs) {\n          if(deg[p] & 1) {\n            if(latte == -1) latte =\
    \ p;\n            else if(malta == -1) malta = p;\n            else return {};\n\
    \          }\n        }\n      }\n      ret.emplace_back(go(latte == -1 ? vs.front()\
    \ : latte));\n      if(ret.back().empty()) ret.pop_back();\n    }\n    return\
    \ ret;\n  }\n\n  vector< int > go(int s) {\n    stack< pair< int, int > > st;\n\
    \    vector< int > ord;\n    st.emplace(s, -1);\n    while(!st.empty()) {\n  \
    \    int idx = st.top().first;\n      used_vertex[idx] = true;\n      if(g[idx].empty())\
    \ {\n        ord.emplace_back(st.top().second);\n        st.pop();\n      } else\
    \ {\n        auto e = g[idx].back();\n        g[idx].pop_back();\n        if(used_edge[e.second])\
    \ continue;\n        used_edge[e.second] = true;\n        st.emplace(e);\n   \
    \   }\n    }\n    ord.pop_back();\n    reverse(ord.begin(), ord.end());\n    return\
    \ ord;\n  }\n};\n"
  code: "/**\n * @brief Eulerian-Trail(\u30AA\u30A4\u30E9\u30FC\u8DEF)\n * @docs docs/eulerian-trail.md\n\
    \ */\ntemplate< bool directed >\nstruct EulerianTrail {\n  vector< vector< pair<\
    \ int, int > > > g;\n  vector< pair< int, int > > es;\n  int M;\n  vector< int\
    \ > used_vertex, used_edge, deg;\n\n  explicit EulerianTrail(int V) : g(V), M(0),\
    \ deg(V), used_vertex(V) {}\n\n  void add_edge(int a, int b) {\n    es.emplace_back(a,\
    \ b);\n    g[a].emplace_back(b, M);\n    if(directed) {\n      deg[a]++;\n   \
    \   deg[b]--;\n    } else {\n      g[b].emplace_back(a, M);\n      deg[a]++;\n\
    \      deg[b]++;\n    }\n    M++;\n  }\n\n  pair< int, int > get_edge(int idx)\
    \ const {\n    return es[idx];\n  }\n\n  vector< vector< int > > enumerate_eulerian_trail()\
    \ {\n    if(directed) {\n      for(auto &p : deg) if(p != 0) return {};\n    }\
    \ else {\n      for(auto &p : deg) if(p & 1) return {};\n    }\n    used_edge.assign(M,\
    \ 0);\n    vector< vector< int > > ret;\n    for(int i = 0; i < (int) g.size();\
    \ i++) {\n      if(g[i].empty() || used_vertex[i]) continue;\n      ret.emplace_back(go(i));\n\
    \    }\n    return ret;\n  }\n\n  vector< vector< int > > enumerate_semi_eulerian_trail()\
    \ {\n    UnionFind uf(g.size());\n    for(auto &p : es) uf.unite(p.first, p.second);\n\
    \    vector< vector< int > > group(g.size());\n    for(int i = 0; i < (int) g.size();\
    \ i++) group[uf.find(i)].emplace_back(i);\n    vector< vector< int > > ret;\n\
    \    used_edge.assign(M, 0);\n    for(auto &vs : group) {\n      if(vs.empty())\
    \ continue;\n      int latte = -1, malta = -1;\n      if(directed) {\n       \
    \ for(auto &p : vs) {\n          if(abs(deg[p]) > 1) {\n            return {};\n\
    \          } else if(deg[p] == 1) {\n            if(latte >= 0) return {};\n \
    \           latte = p;\n          }\n        }\n      } else {\n        for(auto\
    \ &p : vs) {\n          if(deg[p] & 1) {\n            if(latte == -1) latte =\
    \ p;\n            else if(malta == -1) malta = p;\n            else return {};\n\
    \          }\n        }\n      }\n      ret.emplace_back(go(latte == -1 ? vs.front()\
    \ : latte));\n      if(ret.back().empty()) ret.pop_back();\n    }\n    return\
    \ ret;\n  }\n\n  vector< int > go(int s) {\n    stack< pair< int, int > > st;\n\
    \    vector< int > ord;\n    st.emplace(s, -1);\n    while(!st.empty()) {\n  \
    \    int idx = st.top().first;\n      used_vertex[idx] = true;\n      if(g[idx].empty())\
    \ {\n        ord.emplace_back(st.top().second);\n        st.pop();\n      } else\
    \ {\n        auto e = g[idx].back();\n        g[idx].pop_back();\n        if(used_edge[e.second])\
    \ continue;\n        used_edge[e.second] = true;\n        st.emplace(e);\n   \
    \   }\n    }\n    ord.pop_back();\n    reverse(ord.begin(), ord.end());\n    return\
    \ ord;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/others/eulerian-trail.cpp
  requiredBy: []
  timestamp: '2020-09-08 21:03:17+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yukicoder-583.test.cpp
  - test/verify/yosupo-bipartite-edge-coloring.test.cpp
documentation_of: graph/others/eulerian-trail.cpp
layout: document
redirect_from:
- /library/graph/others/eulerian-trail.cpp
- /library/graph/others/eulerian-trail.cpp.html
title: "Eulerian-Trail(\u30AA\u30A4\u30E9\u30FC\u8DEF)"
---
## 概要

有向/無向グラフが与えられたときに, グラフの全ての辺をちょうど $1$ 回ずつ通る閉路やパスを各連結成分について求める.

連結なグラフでオイラー閉路が存在する必要十分条件は, 有向グラフでは全ての頂点について入次数と出次数が等しいこと, 無向グラフでは全ての頂点の次数が偶数であることである.

連結なグラフでオイラー路が存在する必要十分条件は, オイラー閉路の条件にマッチするかどうかに加えて, 有向グラフでは入次数と出次数の差が $1$ である頂点が $2$ 個, 無向グラフでは次数が奇数の頂点が $2$ 個であることである.

## 使い方

* `add_edge(a, b)`: 頂点 `a`, `b` 間に辺をはる.
* `enumerate_eulerian_trail()`: すべての連結成分についてオイラー路を列挙し, オイラー路の辺の idx の列を結合したものを返す. オイラー路が存在しない連結成分があるとき空列を返す.
* `enumerate_semi_eulerian_trail()`: すべての連結成分について準オイラー路を列挙し, 準オイラー路の辺の idx の列を結合したものを返す. 準オイラー路が存在しない連結成分があるとき空列を返す.
* `get_edge(idx)`: `idx` 番目に追加した辺の ${from, to}$ を返す.

## 計算量

$O(V + E)$
