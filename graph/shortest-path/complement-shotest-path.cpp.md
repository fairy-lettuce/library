---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Complement-Shortest-Path(\u88DC\u30B0\u30E9\u30D5\u6700\u77ED\
      \u8DEF)"
    links: []
  bundledCode: "#line 1 \"graph/shortest-path/complement-shotest-path.cpp\"\n/**\n\
    \ * @brief Complement-Shortest-Path(\u88DC\u30B0\u30E9\u30D5\u6700\u77ED\u8DEF\
    )\n */\ntemplate< typename T >\nstruct ComplementShortestPath : Graph< T > {\n\
    \  using Graph< T >::Graph;\n  using Graph< T >::g;\n\n  vector< vector< T > >\
    \ dists;\n\n  void build() {\n    for(auto &es : g) {\n      sort(begin(es), end(es),\
    \ [&](const Edge< T > &a, const Edge< T > &b) {\n        return a.to < b.to;\n\
    \      });\n    }\n    const int N = (int) g.size();\n    dists.resize(N);\n \
    \   for(int i = 0; i < N; i++) {\n      if((int) g[i].size() >= N / 2 - 1) {\n\
    \        dists[i] = complement_bfs(i);\n      }\n    }\n  }\n\n  T query(int s,\
    \ int t) const {\n    if(!dists[s].empty()) {\n      return dists[s][t];\n   \
    \ } else if(!dists[t].empty()) {\n      return dists[t][s];\n    } else if([&]()\
    \ -> bool {\n      int ok = 0, ng = (int) g[s].size();\n      while(ng - ok >\
    \ 1) {\n        int mid = (ok + ng) >> 1;\n        if(g[s][mid].to <= t) ok =\
    \ mid;\n        else ng = mid;\n      }\n      return ok < (int) g[s].size() and\
    \ g[s][ok].to == t;\n    }()) {\n      return 2;\n    } else {\n      return 1;\n\
    \    }\n  }\n\n  vector< T > complement_bfs(int s) {\n    vector< T > dist(g.size(),\
    \ -1);\n    queue< int > que;\n    dist[s] = 0;\n    que.emplace(s);\n    vector<\
    \ int > not_visited;\n    for(int i = 0; i < g.size(); i++) {\n      if(s != i)\
    \ {\n        not_visited.emplace_back(i);\n      }\n    }\n    while(!que.empty())\
    \ {\n      int idx = que.front();\n      que.pop();\n      int ptr = 0;\n    \
    \  vector< int > nxt_visited;\n      for(auto &to : not_visited) {\n        while(ptr\
    \ < (int) g[idx].size() and g[idx][ptr].to < to) {\n          ++ptr;\n       \
    \ }\n        if(ptr < (int) g[idx].size() and to == g[idx][ptr].to) {\n      \
    \    nxt_visited.emplace_back(to);\n        } else {\n          dist[to] = dist[idx]\
    \ + 1;\n          que.emplace(to);\n        }\n      }\n      not_visited = move(nxt_visited);\n\
    \    }\n    return dist;\n  }\n};\n"
  code: "/**\n * @brief Complement-Shortest-Path(\u88DC\u30B0\u30E9\u30D5\u6700\u77ED\
    \u8DEF)\n */\ntemplate< typename T >\nstruct ComplementShortestPath : Graph< T\
    \ > {\n  using Graph< T >::Graph;\n  using Graph< T >::g;\n\n  vector< vector<\
    \ T > > dists;\n\n  void build() {\n    for(auto &es : g) {\n      sort(begin(es),\
    \ end(es), [&](const Edge< T > &a, const Edge< T > &b) {\n        return a.to\
    \ < b.to;\n      });\n    }\n    const int N = (int) g.size();\n    dists.resize(N);\n\
    \    for(int i = 0; i < N; i++) {\n      if((int) g[i].size() >= N / 2 - 1) {\n\
    \        dists[i] = complement_bfs(i);\n      }\n    }\n  }\n\n  T query(int s,\
    \ int t) const {\n    if(!dists[s].empty()) {\n      return dists[s][t];\n   \
    \ } else if(!dists[t].empty()) {\n      return dists[t][s];\n    } else if([&]()\
    \ -> bool {\n      int ok = 0, ng = (int) g[s].size();\n      while(ng - ok >\
    \ 1) {\n        int mid = (ok + ng) >> 1;\n        if(g[s][mid].to <= t) ok =\
    \ mid;\n        else ng = mid;\n      }\n      return ok < (int) g[s].size() and\
    \ g[s][ok].to == t;\n    }()) {\n      return 2;\n    } else {\n      return 1;\n\
    \    }\n  }\n\n  vector< T > complement_bfs(int s) {\n    vector< T > dist(g.size(),\
    \ -1);\n    queue< int > que;\n    dist[s] = 0;\n    que.emplace(s);\n    vector<\
    \ int > not_visited;\n    for(int i = 0; i < g.size(); i++) {\n      if(s != i)\
    \ {\n        not_visited.emplace_back(i);\n      }\n    }\n    while(!que.empty())\
    \ {\n      int idx = que.front();\n      que.pop();\n      int ptr = 0;\n    \
    \  vector< int > nxt_visited;\n      for(auto &to : not_visited) {\n        while(ptr\
    \ < (int) g[idx].size() and g[idx][ptr].to < to) {\n          ++ptr;\n       \
    \ }\n        if(ptr < (int) g[idx].size() and to == g[idx][ptr].to) {\n      \
    \    nxt_visited.emplace_back(to);\n        } else {\n          dist[to] = dist[idx]\
    \ + 1;\n          que.emplace(to);\n        }\n      }\n      not_visited = move(nxt_visited);\n\
    \    }\n    return dist;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/shortest-path/complement-shotest-path.cpp
  requiredBy: []
  timestamp: '2021-01-31 00:27:22+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: graph/shortest-path/complement-shotest-path.cpp
layout: document
redirect_from:
- /library/graph/shortest-path/complement-shotest-path.cpp
- /library/graph/shortest-path/complement-shotest-path.cpp.html
title: "Complement-Shortest-Path(\u88DC\u30B0\u30E9\u30D5\u6700\u77ED\u8DEF)"
---
