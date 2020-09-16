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
  bundledCode: "#line 1 \"other/offline-dynamic-connectivity.cpp\"\nstruct OfflineDynamicConnectivity\
    \ {\n  using edge = pair< int, int >;\n\n  UnionFindUndo uf;\n  int V, Q, segsz;\n\
    \  vector< vector< edge > > seg;\n  int comp;\n\n  vector< pair< pair< int, int\
    \ >, edge > > pend;\n  map< edge, int > cnt, appear;\n\n  OfflineDynamicConnectivity(int\
    \ V, int Q) : uf(V), V(V), Q(Q), comp(V) {\n    segsz = 1;\n    while(segsz <\
    \ Q) segsz <<= 1;\n    seg.resize(2 * segsz - 1);\n  }\n\n  void insert(int idx,\
    \ int s, int t) {\n    auto e = minmax(s, t);\n    if(cnt[e]++ == 0) appear[e]\
    \ = idx;\n  }\n\n  void erase(int idx, int s, int t) {\n    auto e = minmax(s,\
    \ t);\n    if(--cnt[e] == 0) pend.emplace_back(make_pair(appear[e], idx), e);\n\
    \  }\n\n  void add(int a, int b, const edge &e, int k, int l, int r) {\n    if(r\
    \ <= a || b <= l) return;\n    if(a <= l && r <= b) {\n      seg[k].emplace_back(e);\n\
    \      return;\n    }\n    add(a, b, e, 2 * k + 1, l, (l + r) >> 1);\n    add(a,\
    \ b, e, 2 * k + 2, (l + r) >> 1, r);\n  }\n\n  void add(int a, int b, const edge\
    \ &e) {\n    add(a, b, e, 0, 0, segsz);\n  }\n\n  void build() {\n    for(auto\
    \ &p : cnt) {\n      if(p.second > 0) pend.emplace_back(make_pair(appear[p.first],\
    \ Q), p.first);\n    }\n    for(auto &s : pend) {\n      add(s.first.first, s.first.second,\
    \ s.second);\n    }\n  }\n\n  int run(const function< void(int) > &f, int k =\
    \ 0) {\n    int add = 0;\n    for(auto &e : seg[k]) {\n      add += uf.unite(e.first,\
    \ e.second);\n    }\n    comp -= add;\n    if(k < segsz - 1) {\n      run(f, 2\
    \ * k + 1);\n      run(f, 2 * k + 2);\n    } else if(k - (segsz - 1) < Q) {\n\
    \      int query_index = k - (segsz - 1);\n      f(query_index);\n    }\n    for(auto\
    \ &e : seg[k]) {\n      uf.undo();\n    }\n    comp += add;\n  }\n};\n"
  code: "struct OfflineDynamicConnectivity {\n  using edge = pair< int, int >;\n\n\
    \  UnionFindUndo uf;\n  int V, Q, segsz;\n  vector< vector< edge > > seg;\n  int\
    \ comp;\n\n  vector< pair< pair< int, int >, edge > > pend;\n  map< edge, int\
    \ > cnt, appear;\n\n  OfflineDynamicConnectivity(int V, int Q) : uf(V), V(V),\
    \ Q(Q), comp(V) {\n    segsz = 1;\n    while(segsz < Q) segsz <<= 1;\n    seg.resize(2\
    \ * segsz - 1);\n  }\n\n  void insert(int idx, int s, int t) {\n    auto e = minmax(s,\
    \ t);\n    if(cnt[e]++ == 0) appear[e] = idx;\n  }\n\n  void erase(int idx, int\
    \ s, int t) {\n    auto e = minmax(s, t);\n    if(--cnt[e] == 0) pend.emplace_back(make_pair(appear[e],\
    \ idx), e);\n  }\n\n  void add(int a, int b, const edge &e, int k, int l, int\
    \ r) {\n    if(r <= a || b <= l) return;\n    if(a <= l && r <= b) {\n      seg[k].emplace_back(e);\n\
    \      return;\n    }\n    add(a, b, e, 2 * k + 1, l, (l + r) >> 1);\n    add(a,\
    \ b, e, 2 * k + 2, (l + r) >> 1, r);\n  }\n\n  void add(int a, int b, const edge\
    \ &e) {\n    add(a, b, e, 0, 0, segsz);\n  }\n\n  void build() {\n    for(auto\
    \ &p : cnt) {\n      if(p.second > 0) pend.emplace_back(make_pair(appear[p.first],\
    \ Q), p.first);\n    }\n    for(auto &s : pend) {\n      add(s.first.first, s.first.second,\
    \ s.second);\n    }\n  }\n\n  int run(const function< void(int) > &f, int k =\
    \ 0) {\n    int add = 0;\n    for(auto &e : seg[k]) {\n      add += uf.unite(e.first,\
    \ e.second);\n    }\n    comp -= add;\n    if(k < segsz - 1) {\n      run(f, 2\
    \ * k + 1);\n      run(f, 2 * k + 2);\n    } else if(k - (segsz - 1) < Q) {\n\
    \      int query_index = k - (segsz - 1);\n      f(query_index);\n    }\n    for(auto\
    \ &e : seg[k]) {\n      uf.undo();\n    }\n    comp += add;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/offline-dynamic-connectivity.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/offline-dynamic-connectivity.cpp
layout: document
redirect_from:
- /library/other/offline-dynamic-connectivity.cpp
- /library/other/offline-dynamic-connectivity.cpp.html
title: other/offline-dynamic-connectivity.cpp
---
