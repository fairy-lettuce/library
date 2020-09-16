---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    IGNORE: ''
    IGNORE_IF_CLANG: ''
    IGNORE_IF_GCC: ''
    links: []
  bundledCode: "#line 1 \"test/verify/yahoo-procon2018-final-c.cpp\"\n#define IGNORE\n\
    \nint main() {\n  int N, Q;\n  scanf(\"%d %d\", &N, &Q);\n  UnWeightedGraph g(N);\n\
    \  for(int i = 1; i < N; i++) {\n    int x, y;\n    scanf(\"%d %d\", &x, &y);\n\
    \    --x, --y;\n    g[x].emplace_back(y);\n    g[y].emplace_back(x);\n  }\n  vector<\
    \ pair< int, int > > ev[100000];\n  for(int i = 0; i < Q; i++) {\n    int v, k;\n\
    \    scanf(\"%d %d\", &v, &k);\n    --v;\n    ev[v].emplace_back(k, i);\n  }\n\
    \  vector< int > ans(Q);\n  CentroidDecomposition< UnWeightedGraph > cd(g);\n\
    \  UnWeightedGraph tree;\n  int root = cd.build(tree);\n  vector< int > used(N),\
    \ sz(N);\n \n  function< void(int, int, int, int) > add_path = [&](int idx, int\
    \ par, int dep, int d) {\n    sz[dep] += d;\n    for(auto &to : g[idx]) {\n  \
    \    if(to == par || used[to]) continue;\n      add_path(to, idx, dep + 1, d);\n\
    \    }\n  };\n  function< void(int, int, int) > get_path = [&](int idx, int par,\
    \ int dep) {\n    for(auto &e : ev[idx]) {\n      int rest = e.first - dep;\n\
    \      if(rest < 0) continue;\n      ans[e.second] += sz[rest];\n    }\n    for(auto\
    \ &to : g[idx]) {\n      if(to == par || used[to]) continue;\n      get_path(to,\
    \ idx, dep + 1);\n    }\n  };\n  function< void(int) > beet = [&](int idx) {\n\
    \    used[idx] = true;\n    add_path(idx, -1, 0, 1);\n    for(auto &e : ev[idx])\
    \ {\n      int rest = e.first;\n      if(rest < 0) continue;\n      ans[e.second]\
    \ += sz[rest];\n    }\n    for(auto &to : g[idx]) {\n      if(used[to]) continue;\n\
    \      add_path(to, idx, 1, -1);\n      get_path(to, idx, 1);\n      add_path(to,\
    \ idx, 1, 1);\n    }\n    add_path(idx, -1, 0, -1);\n    for(auto &to : tree[idx])\
    \ beet(to);\n    used[idx] = false;\n  };\n  beet(root);\n  for(auto &x : ans)\
    \ printf(\"%d\\n\", x);\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int N, Q;\n  scanf(\"%d %d\", &N, &Q);\n\
    \  UnWeightedGraph g(N);\n  for(int i = 1; i < N; i++) {\n    int x, y;\n    scanf(\"\
    %d %d\", &x, &y);\n    --x, --y;\n    g[x].emplace_back(y);\n    g[y].emplace_back(x);\n\
    \  }\n  vector< pair< int, int > > ev[100000];\n  for(int i = 0; i < Q; i++) {\n\
    \    int v, k;\n    scanf(\"%d %d\", &v, &k);\n    --v;\n    ev[v].emplace_back(k,\
    \ i);\n  }\n  vector< int > ans(Q);\n  CentroidDecomposition< UnWeightedGraph\
    \ > cd(g);\n  UnWeightedGraph tree;\n  int root = cd.build(tree);\n  vector< int\
    \ > used(N), sz(N);\n \n  function< void(int, int, int, int) > add_path = [&](int\
    \ idx, int par, int dep, int d) {\n    sz[dep] += d;\n    for(auto &to : g[idx])\
    \ {\n      if(to == par || used[to]) continue;\n      add_path(to, idx, dep +\
    \ 1, d);\n    }\n  };\n  function< void(int, int, int) > get_path = [&](int idx,\
    \ int par, int dep) {\n    for(auto &e : ev[idx]) {\n      int rest = e.first\
    \ - dep;\n      if(rest < 0) continue;\n      ans[e.second] += sz[rest];\n   \
    \ }\n    for(auto &to : g[idx]) {\n      if(to == par || used[to]) continue;\n\
    \      get_path(to, idx, dep + 1);\n    }\n  };\n  function< void(int) > beet\
    \ = [&](int idx) {\n    used[idx] = true;\n    add_path(idx, -1, 0, 1);\n    for(auto\
    \ &e : ev[idx]) {\n      int rest = e.first;\n      if(rest < 0) continue;\n \
    \     ans[e.second] += sz[rest];\n    }\n    for(auto &to : g[idx]) {\n      if(used[to])\
    \ continue;\n      add_path(to, idx, 1, -1);\n      get_path(to, idx, 1);\n  \
    \    add_path(to, idx, 1, 1);\n    }\n    add_path(idx, -1, 0, -1);\n    for(auto\
    \ &to : tree[idx]) beet(to);\n    used[idx] = false;\n  };\n  beet(root);\n  for(auto\
    \ &x : ans) printf(\"%d\\n\", x);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/yahoo-procon2018-final-c.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/yahoo-procon2018-final-c.cpp
layout: document
redirect_from:
- /library/test/verify/yahoo-procon2018-final-c.cpp
- /library/test/verify/yahoo-procon2018-final-c.cpp.html
title: test/verify/yahoo-procon2018-final-c.cpp
---
