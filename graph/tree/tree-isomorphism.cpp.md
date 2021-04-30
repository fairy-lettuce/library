---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2821.test.cpp
    title: test/verify/aoj-2821.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Tree-Isomorphism(\u6728\u306E\u540C\u578B\u6027\u5224\u5B9A)"
    links: []
  bundledCode: "#line 1 \"graph/tree/tree-isomorphism.cpp\"\n/**\n * @brief Tree-Isomorphism(\u6728\
    \u306E\u540C\u578B\u6027\u5224\u5B9A)\n */\ntemplate< typename T >\nbool tree_isomorphism(const\
    \ Graph< T > &a, const Graph< T > &b) {\n  if(a.size() != b.size()) return false;\n\
    \n  const int N = (int) a.size();\n  using pvi = pair< vector< int >, vector<\
    \ int > >;\n\n  auto get_uku = [&](const Graph< T > &t, int e) {\n    stack< pair<\
    \ int, int > > st;\n    st.emplace(e, -1);\n    vector< int > dep(N, -1), par(N);\n\
    \    while(!st.empty()) {\n      auto p = st.top();\n      if(dep[p.first] ==\
    \ -1) {\n        dep[p.first] = p.second == -1 ? 0 : dep[p.second] + 1;\n    \
    \    for(auto &to : t.g[p.first]) if(to != p.second) st.emplace(to, p.first);\n\
    \      } else {\n        par[p.first] = p.second;\n        st.pop();\n      }\n\
    \    }\n    return make_pair(dep, par);\n  };\n\n  auto solve = [&](const pvi\
    \ &latte, const pvi &malta) {\n\n    int d = *max_element(begin(latte.first),\
    \ end(latte.first));\n    if(d != *max_element(begin(malta.first), end(malta.first)))\
    \ return false;\n\n    vector< vector< int > > latte_d(d + 1), malta_d(d + 1),\
    \ latte_key(N), malta_key(N);\n\n    for(int i = 0; i < N; i++) latte_d[latte.first[i]].emplace_back(i);\n\
    \    for(int i = 0; i < N; i++) malta_d[malta.first[i]].emplace_back(i);\n\n \
    \   for(int i = d; i >= 0; i--) {\n      map< vector< int >, int > ord;\n    \
    \  for(auto &idx : latte_d[i]) {\n        sort(begin(latte_key[idx]), end(latte_key[idx]));\n\
    \        ord[latte_key[idx]]++;\n      }\n      for(auto &idx : malta_d[i]) {\n\
    \        sort(begin(malta_key[idx]), end(malta_key[idx]));\n        if(--ord[malta_key[idx]]\
    \ < 0) return false;\n      }\n      if(i == 0) return ord.size() == 1;\n\n  \
    \    int ptr = 0;\n      for(auto &p : ord) {\n        if(p.second != 0) return\
    \ false;\n        p.second = ptr++;\n      }\n      for(auto &idx : latte_d[i])\
    \ {\n        latte_key[latte.second[idx]].emplace_back(ord[latte_key[idx]]);\n\
    \      }\n      for(auto &idx : malta_d[i]) {\n        malta_key[malta.second[idx]].emplace_back(ord[malta_key[idx]]);\n\
    \      }\n    }\n    assert(0);\n  };\n  auto p = centroid(a), q = centroid(b);\n\
    \  if(p.size() != q.size()) return false;\n  auto a1 = get_uku(a, p[0]);\n  auto\
    \ b1 = get_uku(b, q[0]);\n  if(solve(a1, b1)) return true;\n  if(p.size() == 1)\
    \ return false;\n  auto a2 = get_uku(a, p[1]);\n  return solve(a2, b1);\n}\n"
  code: "/**\n * @brief Tree-Isomorphism(\u6728\u306E\u540C\u578B\u6027\u5224\u5B9A\
    )\n */\ntemplate< typename T >\nbool tree_isomorphism(const Graph< T > &a, const\
    \ Graph< T > &b) {\n  if(a.size() != b.size()) return false;\n\n  const int N\
    \ = (int) a.size();\n  using pvi = pair< vector< int >, vector< int > >;\n\n \
    \ auto get_uku = [&](const Graph< T > &t, int e) {\n    stack< pair< int, int\
    \ > > st;\n    st.emplace(e, -1);\n    vector< int > dep(N, -1), par(N);\n   \
    \ while(!st.empty()) {\n      auto p = st.top();\n      if(dep[p.first] == -1)\
    \ {\n        dep[p.first] = p.second == -1 ? 0 : dep[p.second] + 1;\n        for(auto\
    \ &to : t.g[p.first]) if(to != p.second) st.emplace(to, p.first);\n      } else\
    \ {\n        par[p.first] = p.second;\n        st.pop();\n      }\n    }\n   \
    \ return make_pair(dep, par);\n  };\n\n  auto solve = [&](const pvi &latte, const\
    \ pvi &malta) {\n\n    int d = *max_element(begin(latte.first), end(latte.first));\n\
    \    if(d != *max_element(begin(malta.first), end(malta.first))) return false;\n\
    \n    vector< vector< int > > latte_d(d + 1), malta_d(d + 1), latte_key(N), malta_key(N);\n\
    \n    for(int i = 0; i < N; i++) latte_d[latte.first[i]].emplace_back(i);\n  \
    \  for(int i = 0; i < N; i++) malta_d[malta.first[i]].emplace_back(i);\n\n   \
    \ for(int i = d; i >= 0; i--) {\n      map< vector< int >, int > ord;\n      for(auto\
    \ &idx : latte_d[i]) {\n        sort(begin(latte_key[idx]), end(latte_key[idx]));\n\
    \        ord[latte_key[idx]]++;\n      }\n      for(auto &idx : malta_d[i]) {\n\
    \        sort(begin(malta_key[idx]), end(malta_key[idx]));\n        if(--ord[malta_key[idx]]\
    \ < 0) return false;\n      }\n      if(i == 0) return ord.size() == 1;\n\n  \
    \    int ptr = 0;\n      for(auto &p : ord) {\n        if(p.second != 0) return\
    \ false;\n        p.second = ptr++;\n      }\n      for(auto &idx : latte_d[i])\
    \ {\n        latte_key[latte.second[idx]].emplace_back(ord[latte_key[idx]]);\n\
    \      }\n      for(auto &idx : malta_d[i]) {\n        malta_key[malta.second[idx]].emplace_back(ord[malta_key[idx]]);\n\
    \      }\n    }\n    assert(0);\n  };\n  auto p = centroid(a), q = centroid(b);\n\
    \  if(p.size() != q.size()) return false;\n  auto a1 = get_uku(a, p[0]);\n  auto\
    \ b1 = get_uku(b, q[0]);\n  if(solve(a1, b1)) return true;\n  if(p.size() == 1)\
    \ return false;\n  auto a2 = get_uku(a, p[1]);\n  return solve(a2, b1);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/tree/tree-isomorphism.cpp
  requiredBy: []
  timestamp: '2020-03-30 02:08:59+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-2821.test.cpp
documentation_of: graph/tree/tree-isomorphism.cpp
layout: document
redirect_from:
- /library/graph/tree/tree-isomorphism.cpp
- /library/graph/tree/tree-isomorphism.cpp.html
title: "Tree-Isomorphism(\u6728\u306E\u540C\u578B\u6027\u5224\u5B9A)"
---
