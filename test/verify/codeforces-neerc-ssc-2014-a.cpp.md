---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/codeforces-neerc-ssc-2014-a.cpp\"\n#define IGNORE\n\
    \nstruct UnionFindUndo {\n  vector< int > data;\n  stack< pair< int, int > > history;\n\
    \n  UnionFindUndo(int sz) {\n    data.assign(sz, -1);\n  }\n\n  bool unite(int\
    \ x, int y) {\n    x = find(x), y = find(y);\n    history.emplace(x, data[x]);\n\
    \    history.emplace(y, data[y]);\n    if(x == y) return (false);\n    if(data[x]\
    \ > data[y]) swap(x, y);\n    data[x] += data[y];\n    data[y] = x;\n    return\
    \ (true);\n  }\n\n  int find(int k) {\n    if(data[k] < 0) return (k);\n    return\
    \ (find(data[k]));\n  }\n\n  int size(int k) {\n    return (-data[find(k)]);\n\
    \  }\n\n  void undo() {\n    data[history.top().first] = history.top().second;\n\
    \    history.pop();\n    data[history.top().first] = history.top().second;\n \
    \   history.pop();\n  }\n\n  void snapshot() {\n    while(history.size()) history.pop();\n\
    \  }\n\n  void rollback() {\n    while(history.size()) undo();\n  }\n};\n\nint\
    \ main() {\n  int N, M, Q;\n  cin >> N >> M >> Q;\n  vector< int > X(M), Y(M);\n\
    \  for(int i = 0; i < M; i++) {\n    cin >> X[i] >> Y[i];\n    --X[i], --Y[i];\n\
    \  }\n  MoRollBack mo(N, Q);\n  for(int i = 0; i < Q; i++) {\n    int l, r;\n\
    \    cin >> l >> r;\n    mo.add(--l, r);\n  }\n\n  UnionFindUndo uf(N + N);\n\
    \  vector< int > ans(Q);\n  int dame_sum = 0, dame_add = 0;\n  vector< int > dame;\n\
    \  auto add = [&](int idx) {\n    uf.unite(X[idx], Y[idx] + N);\n    uf.unite(X[idx]\
    \ + N, Y[idx]);\n    dame_add += uf.find(X[idx]) == uf.find(Y[idx]);\n  };\n \
    \ auto rem = [&](int idx) {\n    ans[idx] = dame_sum + dame_add > 0;\n  };\n \
    \ auto reset = [&]() {\n    uf = UnionFindUndo(N + N);\n    dame_add = dame_sum\
    \ = 0;\n  };\n  auto snapshot = [&]() {\n    uf.snapshot();\n    dame_sum += dame_add;\n\
    \    dame_add = 0;\n  };\n  auto rollback = [&]() {\n    uf.rollback();\n    dame_add\
    \ = 0;\n  };\n  mo.run(add, rem, reset, snapshot, rollback);\n  for(auto &p :\
    \ ans) {\n    if(p) cout << \"Impossible\\n\";\n    else cout << \"Possible\\\
    n\";\n  }\n}\n"
  code: "#define IGNORE\n\nstruct UnionFindUndo {\n  vector< int > data;\n  stack<\
    \ pair< int, int > > history;\n\n  UnionFindUndo(int sz) {\n    data.assign(sz,\
    \ -1);\n  }\n\n  bool unite(int x, int y) {\n    x = find(x), y = find(y);\n \
    \   history.emplace(x, data[x]);\n    history.emplace(y, data[y]);\n    if(x ==\
    \ y) return (false);\n    if(data[x] > data[y]) swap(x, y);\n    data[x] += data[y];\n\
    \    data[y] = x;\n    return (true);\n  }\n\n  int find(int k) {\n    if(data[k]\
    \ < 0) return (k);\n    return (find(data[k]));\n  }\n\n  int size(int k) {\n\
    \    return (-data[find(k)]);\n  }\n\n  void undo() {\n    data[history.top().first]\
    \ = history.top().second;\n    history.pop();\n    data[history.top().first] =\
    \ history.top().second;\n    history.pop();\n  }\n\n  void snapshot() {\n    while(history.size())\
    \ history.pop();\n  }\n\n  void rollback() {\n    while(history.size()) undo();\n\
    \  }\n};\n\nint main() {\n  int N, M, Q;\n  cin >> N >> M >> Q;\n  vector< int\
    \ > X(M), Y(M);\n  for(int i = 0; i < M; i++) {\n    cin >> X[i] >> Y[i];\n  \
    \  --X[i], --Y[i];\n  }\n  MoRollBack mo(N, Q);\n  for(int i = 0; i < Q; i++)\
    \ {\n    int l, r;\n    cin >> l >> r;\n    mo.add(--l, r);\n  }\n\n  UnionFindUndo\
    \ uf(N + N);\n  vector< int > ans(Q);\n  int dame_sum = 0, dame_add = 0;\n  vector<\
    \ int > dame;\n  auto add = [&](int idx) {\n    uf.unite(X[idx], Y[idx] + N);\n\
    \    uf.unite(X[idx] + N, Y[idx]);\n    dame_add += uf.find(X[idx]) == uf.find(Y[idx]);\n\
    \  };\n  auto rem = [&](int idx) {\n    ans[idx] = dame_sum + dame_add > 0;\n\
    \  };\n  auto reset = [&]() {\n    uf = UnionFindUndo(N + N);\n    dame_add =\
    \ dame_sum = 0;\n  };\n  auto snapshot = [&]() {\n    uf.snapshot();\n    dame_sum\
    \ += dame_add;\n    dame_add = 0;\n  };\n  auto rollback = [&]() {\n    uf.rollback();\n\
    \    dame_add = 0;\n  };\n  mo.run(add, rem, reset, snapshot, rollback);\n  for(auto\
    \ &p : ans) {\n    if(p) cout << \"Impossible\\n\";\n    else cout << \"Possible\\\
    n\";\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/codeforces-neerc-ssc-2014-a.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/codeforces-neerc-ssc-2014-a.cpp
layout: document
redirect_from:
- /library/test/verify/codeforces-neerc-ssc-2014-a.cpp
- /library/test/verify/codeforces-neerc-ssc-2014-a.cpp.html
title: test/verify/codeforces-neerc-ssc-2014-a.cpp
---
