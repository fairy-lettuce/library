---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.cpp
    title: graph/graph-template.cpp
  - icon: ':question:'
    path: structure/heap/skew-heap.cpp
    title: Skew-Heap
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-2-b.test.cpp
    title: test/verify/aoj-grl-2-b.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-directedmst.test.cpp
    title: test/verify/yosupo-directedmst.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Directed-MST(\u6700\u5C0F\u6709\u5411\u5168\u57DF\u6728)"
    links: []
  bundledCode: "#line 2 \"graph/graph-template.cpp\"\n\ntemplate< typename T = int\
    \ >\nstruct Edge {\n  int from, to;\n  T cost;\n  int idx;\n\n  Edge() = default;\n\
    \n  Edge(int from, int to, T cost = 1, int idx = -1) : from(from), to(to), cost(cost),\
    \ idx(idx) {}\n\n  operator int() const { return to; }\n};\n\ntemplate< typename\
    \ T = int >\nstruct Graph {\n  vector< vector< Edge< T > > > g;\n  int es;\n\n\
    \  Graph() = default;\n\n  explicit Graph(int n) : g(n), es(0) {}\n\n  size_t\
    \ size() const {\n    return g.size();\n  }\n\n  void add_directed_edge(int from,\
    \ int to, T cost = 1) {\n    g[from].emplace_back(from, to, cost, es++);\n  }\n\
    \n  void add_edge(int from, int to, T cost = 1) {\n    g[from].emplace_back(from,\
    \ to, cost, es);\n    g[to].emplace_back(to, from, cost, es++);\n  }\n\n  void\
    \ read(int M, int padding = -1, bool weighted = false, bool directed = false)\
    \ {\n    for(int i = 0; i < M; i++) {\n      int a, b;\n      cin >> a >> b;\n\
    \      a += padding;\n      b += padding;\n      T c = T(1);\n      if(weighted)\
    \ cin >> c;\n      if(directed) add_directed_edge(a, b, c);\n      else add_edge(a,\
    \ b, c);\n    }\n  }\n};\n\ntemplate< typename T = int >\nusing Edges = vector<\
    \ Edge< T > >;\n#line 1 \"structure/heap/skew-heap.cpp\"\n/**\n * @brief Skew-Heap\n\
    \ */\ntemplate< typename T, bool isMin = true >\nstruct SkewHeap {\n  struct Node\
    \ {\n    T key, lazy;\n    Node *l, *r;\n    int idx;\n\n    explicit Node(const\
    \ T &key, int idx) : key(key), idx(idx), lazy(0), l(nullptr), r(nullptr) {}\n\
    \  };\n\n  SkewHeap() = default;\n\n  Node *alloc(const T &key, int idx = -1)\
    \ {\n    return new Node(key, idx);\n  }\n\n  Node *propagate(Node *t) {\n   \
    \ if(t && t->lazy != 0) {\n      if(t->l) t->l->lazy += t->lazy;\n      if(t->r)\
    \ t->r->lazy += t->lazy;\n      t->key += t->lazy;\n      t->lazy = 0;\n    }\n\
    \    return t;\n  }\n\n  Node *meld(Node *x, Node *y) {\n    propagate(x), propagate(y);\n\
    \    if(!x || !y) return x ? x : y;\n    if((x->key < y->key) ^ isMin) swap(x,\
    \ y);\n    x->r = meld(y, x->r);\n    swap(x->l, x->r);\n    return x;\n  }\n\n\
    \  Node *push(Node *t, const T &key, int idx = -1) {\n    return meld(t, alloc(key,\
    \ idx));\n  }\n\n  Node *pop(Node *t) {\n    assert(t != nullptr);\n    return\
    \ meld(t->l, t->r);\n  }\n\n  Node *add(Node *t, const T &lazy) {\n    if(t) {\n\
    \      t->lazy += lazy;\n      propagate(t);\n    }\n    return t;\n  }\n\n  Node\
    \ *make_root() {\n    return nullptr;\n  }\n};\n#line 3 \"graph/mst/directed-mst.cpp\"\
    \n\n/**\n * @brief Directed-MST(\u6700\u5C0F\u6709\u5411\u5168\u57DF\u6728)\n\
    \ */\ntemplate< typename T >\nstruct MinimumSpanningTree {\n  T cost;\n  Edges<\
    \ T > edges;\n};\n\ntemplate< typename T >\nMinimumSpanningTree< T > directed_mst(int\
    \ V, int root, Edges< T > edges) {\n  for(int i = 0; i < V; ++i) {\n    if(i !=\
    \ root) edges.emplace_back(i, root, 0);\n  }\n\n  int x = 0;\n  vector< int >\
    \ par(2 * V, -1), vis(par), link(par);\n\n  using Heap = SkewHeap< T, true >;\n\
    \  using Node = typename Heap::Node;\n\n  Heap heap;\n  vector< Node * > ins(2\
    \ * V, heap.make_root());\n\n  for(int i = 0; i < (int) edges.size(); i++) {\n\
    \    auto &e = edges[i];\n    ins[e.to] = heap.push(ins[e.to], e.cost, i);\n \
    \ }\n  vector< int > st;\n  auto go = [&](int x) {\n    x = edges[ins[x]->idx].from;\n\
    \    while(link[x] != -1) {\n      st.emplace_back(x);\n      x = link[x];\n \
    \   }\n    for(auto &p : st) {\n      link[p] = x;\n    }\n    st.clear();\n \
    \   return x;\n  };\n  for(int i = V; ins[x]; i++) {\n    for(; vis[x] == -1;\
    \ x = go(x)) vis[x] = 0;\n    for(; x != i; x = go(x)) {\n      auto w = ins[x]->key;\n\
    \      auto v = heap.pop(ins[x]);\n      v = heap.add(v, -w);\n      ins[i] =\
    \ heap.meld(ins[i], v);\n      par[x] = i;\n      link[x] = i;\n    }\n    for(;\
    \ ins[x] && go(x) == x; ins[x] = heap.pop(ins[x]));\n  }\n  T cost = 0;\n  Edges<\
    \ T > ans;\n  for(int i = root; i != -1; i = par[i]) {\n    vis[i] = 1;\n  }\n\
    \  for(int i = x; i >= 0; i--) {\n    if(vis[i] == 1) continue;\n    cost += edges[ins[i]->idx].cost;\n\
    \    ans.emplace_back(edges[ins[i]->idx]);\n    for(int j = edges[ins[i]->idx].to;\
    \ j != -1 && vis[j] == 0; j = par[j]) {\n      vis[j] = 1;\n    }\n  }\n  return\
    \ {cost, ans};\n}\n"
  code: "#include \"../graph-template.cpp\"\n#include \"../../structure/heap/skew-heap.cpp\"\
    \n\n/**\n * @brief Directed-MST(\u6700\u5C0F\u6709\u5411\u5168\u57DF\u6728)\n\
    \ */\ntemplate< typename T >\nstruct MinimumSpanningTree {\n  T cost;\n  Edges<\
    \ T > edges;\n};\n\ntemplate< typename T >\nMinimumSpanningTree< T > directed_mst(int\
    \ V, int root, Edges< T > edges) {\n  for(int i = 0; i < V; ++i) {\n    if(i !=\
    \ root) edges.emplace_back(i, root, 0);\n  }\n\n  int x = 0;\n  vector< int >\
    \ par(2 * V, -1), vis(par), link(par);\n\n  using Heap = SkewHeap< T, true >;\n\
    \  using Node = typename Heap::Node;\n\n  Heap heap;\n  vector< Node * > ins(2\
    \ * V, heap.make_root());\n\n  for(int i = 0; i < (int) edges.size(); i++) {\n\
    \    auto &e = edges[i];\n    ins[e.to] = heap.push(ins[e.to], e.cost, i);\n \
    \ }\n  vector< int > st;\n  auto go = [&](int x) {\n    x = edges[ins[x]->idx].from;\n\
    \    while(link[x] != -1) {\n      st.emplace_back(x);\n      x = link[x];\n \
    \   }\n    for(auto &p : st) {\n      link[p] = x;\n    }\n    st.clear();\n \
    \   return x;\n  };\n  for(int i = V; ins[x]; i++) {\n    for(; vis[x] == -1;\
    \ x = go(x)) vis[x] = 0;\n    for(; x != i; x = go(x)) {\n      auto w = ins[x]->key;\n\
    \      auto v = heap.pop(ins[x]);\n      v = heap.add(v, -w);\n      ins[i] =\
    \ heap.meld(ins[i], v);\n      par[x] = i;\n      link[x] = i;\n    }\n    for(;\
    \ ins[x] && go(x) == x; ins[x] = heap.pop(ins[x]));\n  }\n  T cost = 0;\n  Edges<\
    \ T > ans;\n  for(int i = root; i != -1; i = par[i]) {\n    vis[i] = 1;\n  }\n\
    \  for(int i = x; i >= 0; i--) {\n    if(vis[i] == 1) continue;\n    cost += edges[ins[i]->idx].cost;\n\
    \    ans.emplace_back(edges[ins[i]->idx]);\n    for(int j = edges[ins[i]->idx].to;\
    \ j != -1 && vis[j] == 0; j = par[j]) {\n      vis[j] = 1;\n    }\n  }\n  return\
    \ {cost, ans};\n}\n"
  dependsOn:
  - graph/graph-template.cpp
  - structure/heap/skew-heap.cpp
  isVerificationFile: false
  path: graph/mst/directed-mst.cpp
  requiredBy: []
  timestamp: '2020-12-18 22:15:25+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-2-b.test.cpp
  - test/verify/yosupo-directedmst.test.cpp
documentation_of: graph/mst/directed-mst.cpp
layout: document
redirect_from:
- /library/graph/mst/directed-mst.cpp
- /library/graph/mst/directed-mst.cpp.html
title: "Directed-MST(\u6700\u5C0F\u6709\u5411\u5168\u57DF\u6728)"
---
