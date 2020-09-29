---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-joisc-2015-g.cpp\"\n#define IGNORE\n\
    \nstruct UnionFind {\n  vector< int > data;\n \n  UnionFind(int sz) {\n    data.assign(sz,\
    \ -1);\n  }\n \n  bool unite(int x, int y) {\n    x = find(x), y = find(y);\n\
    \    if(x == y) return (false);\n    if(data[x] > data[y]) swap(x, y);\n    data[x]\
    \ += data[y];\n    data[y] = x;\n    return (true);\n  }\n \n  int find(int k)\
    \ {\n    if(data[k] < 0) return (k);\n    return (data[k] = find(data[k]));\n\
    \  }\n \n  int size(int k) {\n    return (-data[find(k)]);\n  }\n};\n \nint main()\
    \ {\n  int N, Q;\n  cin >> N >> Q;\n  auto f = [](int a, int b) { return a + b;\
    \ };\n  auto g = [](int a, int b, int l) { return 0; };\n  auto h = [](int a,\
    \ int b) { return (a | b); };\n  auto s = [](int a) { return a; };\n  using LCT=LinkCutTree<\
    \ int >;\n  LCT lct(f, g, h, s, 0, 0);\n  vector< LCT::Node * > nodev, nodee;\n\
    \  for(int i = 0; i < N; i++) {\n    nodev.emplace_back(lct.make_node(i, 0));\n\
    \    nodee.emplace_back(lct.make_node(i, 1));\n  }\n  UnionFind uf(N);\n  int\
    \ cnt = 0;\n  for(int i = 0; i < Q; i++) {\n    int T, A, B;\n    cin >> T >>\
    \ A >> B;\n    --A, --B;\n    if(T == 1) {\n      if(uf.find(A) != uf.find(B))\
    \ {\n        lct.evert(nodev[B]);\n        lct.link(nodee[cnt], nodev[A]);\n \
    \       lct.link(nodev[B], nodee[cnt]);\n        uf.unite(A, B);\n        ++cnt;\n\
    \      } else {\n        lct.evert(nodev[A]);\n        lct.expose(nodev[B]);\n\
    \        lct.set_propagate(nodev[B], 1);\n      }\n    } else {\n      if(uf.find(A)\
    \ != uf.find(B)) {\n        cout << -1 << \"\\n\";\n      } else {\n        lct.evert(nodev[A]);\n\
    \        lct.expose(nodev[B]);\n        cout << nodev[B]->sum << \"\\n\";\n  \
    \    }\n    }\n  }\n}\n"
  code: "#define IGNORE\n\nstruct UnionFind {\n  vector< int > data;\n \n  UnionFind(int\
    \ sz) {\n    data.assign(sz, -1);\n  }\n \n  bool unite(int x, int y) {\n    x\
    \ = find(x), y = find(y);\n    if(x == y) return (false);\n    if(data[x] > data[y])\
    \ swap(x, y);\n    data[x] += data[y];\n    data[y] = x;\n    return (true);\n\
    \  }\n \n  int find(int k) {\n    if(data[k] < 0) return (k);\n    return (data[k]\
    \ = find(data[k]));\n  }\n \n  int size(int k) {\n    return (-data[find(k)]);\n\
    \  }\n};\n \nint main() {\n  int N, Q;\n  cin >> N >> Q;\n  auto f = [](int a,\
    \ int b) { return a + b; };\n  auto g = [](int a, int b, int l) { return 0; };\n\
    \  auto h = [](int a, int b) { return (a | b); };\n  auto s = [](int a) { return\
    \ a; };\n  using LCT=LinkCutTree< int >;\n  LCT lct(f, g, h, s, 0, 0);\n  vector<\
    \ LCT::Node * > nodev, nodee;\n  for(int i = 0; i < N; i++) {\n    nodev.emplace_back(lct.make_node(i,\
    \ 0));\n    nodee.emplace_back(lct.make_node(i, 1));\n  }\n  UnionFind uf(N);\n\
    \  int cnt = 0;\n  for(int i = 0; i < Q; i++) {\n    int T, A, B;\n    cin >>\
    \ T >> A >> B;\n    --A, --B;\n    if(T == 1) {\n      if(uf.find(A) != uf.find(B))\
    \ {\n        lct.evert(nodev[B]);\n        lct.link(nodee[cnt], nodev[A]);\n \
    \       lct.link(nodev[B], nodee[cnt]);\n        uf.unite(A, B);\n        ++cnt;\n\
    \      } else {\n        lct.evert(nodev[A]);\n        lct.expose(nodev[B]);\n\
    \        lct.set_propagate(nodev[B], 1);\n      }\n    } else {\n      if(uf.find(A)\
    \ != uf.find(B)) {\n        cout << -1 << \"\\n\";\n      } else {\n        lct.evert(nodev[A]);\n\
    \        lct.expose(nodev[B]);\n        cout << nodev[B]->sum << \"\\n\";\n  \
    \    }\n    }\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-joisc-2015-g.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-joisc-2015-g.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-joisc-2015-g.cpp
- /library/test/verify/atcoder-joisc-2015-g.cpp.html
title: test/verify/atcoder-joisc-2015-g.cpp
---
