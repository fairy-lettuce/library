---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: structure/union-find/union-find.cpp
    title: Union-Find
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-staticrmq-6.test.cpp
    title: test/verify/yosupo-staticrmq-6.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: Offline RMQ
    links: []
  bundledCode: "#line 1 \"structure/union-find/union-find.cpp\"\n/**\n * @brief Union-Find\n\
    \ * @docs docs/union-find.md\n */\nstruct UnionFind {\n  vector< int > data;\n\
    \n  UnionFind() = default;\n\n  explicit UnionFind(size_t sz) : data(sz, -1) {}\n\
    \n  bool unite(int x, int y) {\n    x = find(x), y = find(y);\n    if(x == y)\
    \ return false;\n    if(data[x] > data[y]) swap(x, y);\n    data[x] += data[y];\n\
    \    data[y] = x;\n    return true;\n  }\n\n  int find(int k) {\n    if(data[k]\
    \ < 0) return (k);\n    return data[k] = find(data[k]);\n  }\n\n  int size(int\
    \ k) {\n    return -data[find(k)];\n  }\n\n  bool same(int x, int y) {\n    return\
    \ find(x) == find(y);\n  }\n\n  vector< vector< int > > groups() {\n    int n\
    \ = (int) data.size();\n    vector< vector< int > > ret(n);\n    for(int i = 0;\
    \ i < n; i++) {\n      ret[find(i)].emplace_back(i);\n    }\n    ret.erase(remove_if(begin(ret),\
    \ end(ret), [&](const vector< int > &v) {\n      return v.empty();\n    }));\n\
    \    return ret;\n  }\n};\n#line 2 \"other/offline-rmq.cpp\"\n\n/**\n * @brief\
    \ Offline RMQ\n **/\ntemplate< typename Comp >\nvector< int > offline_rmq(vector<\
    \ pair< int, int > > &qs, const Comp &comp) {\n  int n = 0;\n  for(auto&[l, r]:\
    \ qs) n = max(n, r);\n  UnionFind uf(n);\n  vector< int > st(n), mark(n), ans(qs.size());\n\
    \  int top = -1;\n  for(auto&[l, r]: qs) mark[r - 1]++;\n  vector< vector< int\
    \ > > q(n);\n  for(int i = 0; i < n; i++) {\n    q[i].reserve(mark[i]);\n  }\n\
    \  for(int i = 0; i < qs.size(); i++) {\n    q[qs[i].second - 1].emplace_back(i);\n\
    \  }\n  for(int i = 0; i < n; i++) {\n    while(~top and not comp(st[top], i))\
    \ {\n      uf.unite(st[top--], i);\n    }\n    st[++top] = i;\n    mark[uf.find(i)]\
    \ = i;\n    for(auto &j: q[i]) {\n      ans[j] = mark[uf.find(qs[j].first)];\n\
    \    }\n  }\n  return ans;\n}\n"
  code: "#include \"../structure/union-find/union-find.cpp\"\n\n/**\n * @brief Offline\
    \ RMQ\n **/\ntemplate< typename Comp >\nvector< int > offline_rmq(vector< pair<\
    \ int, int > > &qs, const Comp &comp) {\n  int n = 0;\n  for(auto&[l, r]: qs)\
    \ n = max(n, r);\n  UnionFind uf(n);\n  vector< int > st(n), mark(n), ans(qs.size());\n\
    \  int top = -1;\n  for(auto&[l, r]: qs) mark[r - 1]++;\n  vector< vector< int\
    \ > > q(n);\n  for(int i = 0; i < n; i++) {\n    q[i].reserve(mark[i]);\n  }\n\
    \  for(int i = 0; i < qs.size(); i++) {\n    q[qs[i].second - 1].emplace_back(i);\n\
    \  }\n  for(int i = 0; i < n; i++) {\n    while(~top and not comp(st[top], i))\
    \ {\n      uf.unite(st[top--], i);\n    }\n    st[++top] = i;\n    mark[uf.find(i)]\
    \ = i;\n    for(auto &j: q[i]) {\n      ans[j] = mark[uf.find(qs[j].first)];\n\
    \    }\n  }\n  return ans;\n}\n"
  dependsOn:
  - structure/union-find/union-find.cpp
  isVerificationFile: false
  path: other/offline-rmq.cpp
  requiredBy: []
  timestamp: '2021-10-28 01:20:12+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-staticrmq-6.test.cpp
documentation_of: other/offline-rmq.cpp
layout: document
redirect_from:
- /library/other/offline-rmq.cpp
- /library/other/offline-rmq.cpp.html
title: Offline RMQ
---
