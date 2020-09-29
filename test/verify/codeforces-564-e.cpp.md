---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/codeforces-564-e.cpp\"\n#define IGNORE\n\nint\
    \ main() {\n  struct tap {\n    int64 sz, szsum, cashsz, cashszsum;\n \n    tap()\
    \ : sz(0), szsum(0), cashsz(0), cashszsum(0) {}\n \n \n    void merge(int64 key,\
    \ const tap &parent, const tap &child) {\n      szsum = cashszsum;\n      szsum\
    \ += parent.sz * parent.sz;\n      szsum += child.sz * child.sz;\n \n      sz\
    \ = key;\n      sz += parent.sz;\n      sz += child.sz;\n      sz += cashsz;\n\
    \    }\n \n    void toggle() {\n    }\n \n    void add(const tap &child) {\n \
    \     cashszsum += child.sz * child.sz;\n      cashsz += child.sz;\n    }\n \n\
    \    void erase(const tap &child) {\n      cashszsum -= child.sz * child.sz;\n\
    \      cashsz -= child.sz;\n    }\n  } e;\n \n  int N, M;\n  cin >> N >> M;\n\
    \  vector< int > C(N);\n  cin >> C;\n \n  using pi = pair< int64, int >;\n \n\
    \  using LCT = LinkCutTreeSubtree< tap, int64 >;\n  LCT lct(e);\n  vector< LCT::Node\
    \ * > sub(N);\n  vector< map< int, vector< pair< int, int > > > > belong(N + 1);\n\
    \  for(int i = 0; i < N; i++) {\n    --C[i];\n    sub[i] = lct.make_node(1);\n\
    \    belong[C[i]][-1].emplace_back(i, 0);\n  }\n \n  vector< int > parent(N +\
    \ 1, -1);\n  vector< int > g[400001];\n \n  g[N].emplace_back(0);\n  sub.emplace_back(lct.make_node(1));\n\
    \ \n  function< void(int, int) > dfs = [&](int idx, int par) {\n    parent[idx]\
    \ = par;\n    for(auto &to : g[idx]) {\n      if(to == par) continue;\n      dfs(to,\
    \ idx);\n    }\n  };\n  for(int i = 1; i < N; i++) {\n    int x, y;\n    cin >>\
    \ x >> y;\n    --x, --y;\n    g[x].emplace_back(y);\n    g[y].emplace_back(x);\n\
    \    lct.evert(sub[y]);\n    lct.link(sub[y], sub[x]);\n  }\n  lct.evert(sub[0]);\n\
    \  lct.link(sub[0], sub[N]);\n  dfs(N, -1);\n \n  for(int i = 0; i < M; i++) {\n\
    \    int u, x;\n    cin >> u >> x;\n    --u, --x;\n    if(C[u] != x) {\n     \
    \ belong[C[u]][i].emplace_back(u, 1); // set black\n      C[u] = x;\n      belong[x][i].emplace_back(u,\
    \ 0); // set white\n    }\n  }\n \n \n  vector< int64 > ans(M + 1);\n \n \n  for(int\
    \ i = 0; i < N; i++) {\n \n    int last = -1;\n    int64 path = 1LL * N * N;\n\
    \ \n    set< int > st;\n \n    for(auto &vs : belong[i]) {\n      ans[last + 1]\
    \ += path;\n      ans[vs.first + 1] -= path;\n \n      for(auto &p : vs.second)\
    \ {\n        if(!p.second) {\n          st.emplace(p.first);\n          path -=\
    \ lct.query(lct.get_root(sub[p.first])).szsum;\n          lct.cut(sub[p.first]);\n\
    \          path += lct.query(lct.get_root(sub[parent[p.first]])).szsum;\n    \
    \      path += lct.query(lct.get_root(sub[p.first])).szsum;\n        } else {\n\
    \          st.erase(p.first);\n          path -= lct.query(lct.get_root(sub[p.first])).szsum;\n\
    \          path -= lct.query(lct.get_root(sub[parent[p.first]])).szsum;\n    \
    \      lct.link(sub[p.first], sub[parent[p.first]]);\n          path += lct.query(lct.get_root(sub[p.first])).szsum;\n\
    \        }\n      }\n      last = vs.first;\n    }\n    ans[last + 1] += path;\n\
    \    for(auto &p : st) lct.link(sub[p], sub[parent[p]]);\n  }\n \n  int64 ret\
    \ = 0;\n  for(int j = 0; j <= M; j++) {\n    ret += ans[j];\n    cout << 1LL *\
    \ N * N * N - ret << \"\\n\";\n  }\n}\n"
  code: "#define IGNORE\n\nint main() {\n  struct tap {\n    int64 sz, szsum, cashsz,\
    \ cashszsum;\n \n    tap() : sz(0), szsum(0), cashsz(0), cashszsum(0) {}\n \n\
    \ \n    void merge(int64 key, const tap &parent, const tap &child) {\n      szsum\
    \ = cashszsum;\n      szsum += parent.sz * parent.sz;\n      szsum += child.sz\
    \ * child.sz;\n \n      sz = key;\n      sz += parent.sz;\n      sz += child.sz;\n\
    \      sz += cashsz;\n    }\n \n    void toggle() {\n    }\n \n    void add(const\
    \ tap &child) {\n      cashszsum += child.sz * child.sz;\n      cashsz += child.sz;\n\
    \    }\n \n    void erase(const tap &child) {\n      cashszsum -= child.sz * child.sz;\n\
    \      cashsz -= child.sz;\n    }\n  } e;\n \n  int N, M;\n  cin >> N >> M;\n\
    \  vector< int > C(N);\n  cin >> C;\n \n  using pi = pair< int64, int >;\n \n\
    \  using LCT = LinkCutTreeSubtree< tap, int64 >;\n  LCT lct(e);\n  vector< LCT::Node\
    \ * > sub(N);\n  vector< map< int, vector< pair< int, int > > > > belong(N + 1);\n\
    \  for(int i = 0; i < N; i++) {\n    --C[i];\n    sub[i] = lct.make_node(1);\n\
    \    belong[C[i]][-1].emplace_back(i, 0);\n  }\n \n  vector< int > parent(N +\
    \ 1, -1);\n  vector< int > g[400001];\n \n  g[N].emplace_back(0);\n  sub.emplace_back(lct.make_node(1));\n\
    \ \n  function< void(int, int) > dfs = [&](int idx, int par) {\n    parent[idx]\
    \ = par;\n    for(auto &to : g[idx]) {\n      if(to == par) continue;\n      dfs(to,\
    \ idx);\n    }\n  };\n  for(int i = 1; i < N; i++) {\n    int x, y;\n    cin >>\
    \ x >> y;\n    --x, --y;\n    g[x].emplace_back(y);\n    g[y].emplace_back(x);\n\
    \    lct.evert(sub[y]);\n    lct.link(sub[y], sub[x]);\n  }\n  lct.evert(sub[0]);\n\
    \  lct.link(sub[0], sub[N]);\n  dfs(N, -1);\n \n  for(int i = 0; i < M; i++) {\n\
    \    int u, x;\n    cin >> u >> x;\n    --u, --x;\n    if(C[u] != x) {\n     \
    \ belong[C[u]][i].emplace_back(u, 1); // set black\n      C[u] = x;\n      belong[x][i].emplace_back(u,\
    \ 0); // set white\n    }\n  }\n \n \n  vector< int64 > ans(M + 1);\n \n \n  for(int\
    \ i = 0; i < N; i++) {\n \n    int last = -1;\n    int64 path = 1LL * N * N;\n\
    \ \n    set< int > st;\n \n    for(auto &vs : belong[i]) {\n      ans[last + 1]\
    \ += path;\n      ans[vs.first + 1] -= path;\n \n      for(auto &p : vs.second)\
    \ {\n        if(!p.second) {\n          st.emplace(p.first);\n          path -=\
    \ lct.query(lct.get_root(sub[p.first])).szsum;\n          lct.cut(sub[p.first]);\n\
    \          path += lct.query(lct.get_root(sub[parent[p.first]])).szsum;\n    \
    \      path += lct.query(lct.get_root(sub[p.first])).szsum;\n        } else {\n\
    \          st.erase(p.first);\n          path -= lct.query(lct.get_root(sub[p.first])).szsum;\n\
    \          path -= lct.query(lct.get_root(sub[parent[p.first]])).szsum;\n    \
    \      lct.link(sub[p.first], sub[parent[p.first]]);\n          path += lct.query(lct.get_root(sub[p.first])).szsum;\n\
    \        }\n      }\n      last = vs.first;\n    }\n    ans[last + 1] += path;\n\
    \    for(auto &p : st) lct.link(sub[p], sub[parent[p]]);\n  }\n \n  int64 ret\
    \ = 0;\n  for(int j = 0; j <= M; j++) {\n    ret += ans[j];\n    cout << 1LL *\
    \ N * N * N - ret << \"\\n\";\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/codeforces-564-e.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/codeforces-564-e.cpp
layout: document
redirect_from:
- /library/test/verify/codeforces-564-e.cpp
- /library/test/verify/codeforces-564-e.cpp.html
title: test/verify/codeforces-564-e.cpp
---
