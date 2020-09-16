---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  - icon: ':heavy_check_mark:'
    path: graph/template.cpp
    title: graph/template.cpp
  - icon: ':heavy_check_mark:'
    path: structure/union-find/union-find.cpp
    title: Union-Find
  - icon: ':heavy_check_mark:'
    path: structure/heap/skew-heap.cpp
    title: structure/heap/skew-heap.cpp
  - icon: ':heavy_check_mark:'
    path: graph/mst/chu-liu-edmond.cpp
    title: graph/mst/chu-liu-edmond.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B
  bundledCode: "#line 1 \"test/verify/aoj-grl-2-b.test.cpp\"\n#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B\"\
    \n\n#line 1 \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace\
    \ std;\n\nusing int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll\
    \ = (1LL << 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup()\
    \ {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed\
    \ << setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
    \n\ntemplate< typename T1, typename T2 >\nostream &operator<<(ostream &os, const\
    \ pair< T1, T2 >& p) {\n  os << p.first << \" \" << p.second;\n  return os;\n\
    }\n\ntemplate< typename T1, typename T2 >\nistream &operator>>(istream &is, pair<\
    \ T1, T2 > &p) {\n  is >> p.first >> p.second;\n  return is;\n}\n\ntemplate< typename\
    \ T >\nostream &operator<<(ostream &os, const vector< T > &v) {\n  for(int i =\
    \ 0; i < (int) v.size(); i++) {\n    os << v[i] << (i + 1 != v.size() ? \" \"\
    \ : \"\");\n  }\n  return os;\n}\n\ntemplate< typename T >\nistream &operator>>(istream\
    \ &is, vector< T > &v) {\n  for(T &in : v) is >> in;\n  return is;\n}\n\ntemplate<\
    \ typename T1, typename T2 >\ninline bool chmax(T1 &a, T2 b) { return a < b &&\
    \ (a = b, true); }\n\ntemplate< typename T1, typename T2 >\ninline bool chmin(T1\
    \ &a, T2 b) { return a > b && (a = b, true); }\n\ntemplate< typename T = int64\
    \ >\nvector< T > make_v(size_t a) {\n  return vector< T >(a);\n}\n\ntemplate<\
    \ typename T, typename... Ts >\nauto make_v(size_t a, Ts... ts) {\n  return vector<\
    \ decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));\n}\n\ntemplate< typename\
    \ T, typename V >\ntypename enable_if< is_class< T >::value == 0 >::type fill_v(T\
    \ &t, const V &v) {\n  t = v;\n}\n\ntemplate< typename T, typename V >\ntypename\
    \ enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {\n  for(auto\
    \ &e : t) fill_v(e, v);\n}\n\ntemplate< typename F >\nstruct FixPoint : F {\n\
    \  FixPoint(F &&f) : F(forward< F >(f)) {}\n \n  template< typename... Args >\n\
    \  decltype(auto) operator()(Args &&... args) const {\n    return F::operator()(*this,\
    \ forward< Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 1 \"graph/template.cpp\"\
    \ntemplate< typename T >\nstruct edge {\n  int src, to;\n  T cost;\n\n  edge(int\
    \ to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int src, int to, T cost)\
    \ : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const int &x) {\n   \
    \ to = x;\n    return *this;\n  }\n\n  operator int() const { return to; }\n};\n\
    \ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate< typename\
    \ T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph = vector<\
    \ vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector< T >\
    \ >;\n#line 5 \"test/verify/aoj-grl-2-b.test.cpp\"\n\n#line 1 \"structure/union-find/union-find.cpp\"\
    \n/**\n * @brief Union-Find\n * @docs docs/union-find.md\n */\nstruct UnionFind\
    \ {\n  vector< int > data;\n\n  UnionFind() = default;\n\n  explicit UnionFind(size_t\
    \ sz) : data(sz, -1) {}\n\n  bool unite(int x, int y) {\n    x = find(x), y =\
    \ find(y);\n    if(x == y) return false;\n    if(data[x] > data[y]) swap(x, y);\n\
    \    data[x] += data[y];\n    data[y] = x;\n    return true;\n  }\n\n  int find(int\
    \ k) {\n    if(data[k] < 0) return (k);\n    return data[k] = find(data[k]);\n\
    \  }\n\n  int size(int k) {\n    return -data[find(k)];\n  }\n\n  bool same(int\
    \ x, int y) {\n    return find(x) == find(y);\n  }\n};\n#line 1 \"structure/heap/skew-heap.cpp\"\
    \ntemplate< typename T, typename E = T >\nstruct SkewHeap {\n  using G = function<\
    \ T(T, E) >;\n  using H = function< E(E, E) >;\n \n  struct Node {\n    T key;\n\
    \    E lazy;\n    Node *l, *r;\n  };\n \n  const bool rev;\n  const G g;\n  const\
    \ H h;\n \n  SkewHeap(bool rev = false) : g([](const T &a, const E &b) { return\
    \ a + b; }),\n                               h([](const E &a, const E &b) { return\
    \ a + b; }), rev(rev) {}\n \n  SkewHeap(const G &g, const H &h, bool rev = false)\
    \ : g(g), h(h), rev(rev) {}\n \n  Node *propagate(Node *t) {\n    if(t->lazy !=\
    \ 0) {\n      if(t->l) t->l->lazy = h(t->l->lazy, t->lazy);\n      if(t->r) t->r->lazy\
    \ = h(t->r->lazy, t->lazy);\n      t->key = g(t->key, t->lazy);\n      t->lazy\
    \ = 0;\n    }\n    return t;\n  }\n \n  Node *merge(Node *x, Node *y) {\n    if(!x\
    \ || !y) return x ? x : y;\n    propagate(x), propagate(y);\n    if((x->key >\
    \ y->key) ^ rev) swap(x, y);\n    x->r = merge(y, x->r);\n    swap(x->l, x->r);\n\
    \    return x;\n  }\n \n  void push(Node *&root, const T &key) {\n    root = merge(root,\
    \ new Node({key, 0, nullptr, nullptr}));\n  }\n \n  T top(Node *root) {\n    return\
    \ propagate(root)->key;\n  }\n \n  T pop(Node *&root) {\n    T top = propagate(root)->key;\n\
    \    auto *temp = root;\n    root = merge(root->l, root->r);\n    delete temp;\n\
    \    return top;\n  }\n \n  bool empty(Node *root) const {\n    return !root;\n\
    \  }\n \n  void add(Node *root, const E &lazy) {\n    if(root) {\n      root->lazy\
    \ = h(root->lazy, lazy);\n      propagate(root);\n    }\n  }\n \n  Node *makeheap()\
    \ {\n    return nullptr;\n  }\n};\n#line 8 \"test/verify/aoj-grl-2-b.test.cpp\"\
    \n\n#line 1 \"graph/mst/chu-liu-edmond.cpp\"\ntemplate< typename T >\nstruct MinimumSpanningTreeArborescence\n\
    {\n  using Pi = pair< T, int >;\n  using Heap = SkewHeap< Pi, int >;\n  using\
    \ Node = typename Heap::Node;\n  const Edges< T > &es;\n  const int V;\n  T INF;\n\
    \ \n  MinimumSpanningTreeArborescence(const Edges< T > &es, int V) :\n      INF(numeric_limits<\
    \ T >::max()), es(es), V(V) {}\n \n  T build(int start)\n  {\n    auto g = [](const\
    \ Pi &a, const T &b) { return Pi(a.first + b, a.second); };\n    auto h = [](const\
    \ T &a, const T &b) { return a + b; };\n    Heap heap(g, h);\n    vector< Node\
    \ * > heaps(V, heap.makeheap());\n    for(auto &e : es) heap.push(heaps[e.to],\
    \ {e.cost, e.src});\n    UnionFind uf(V);\n    vector< int > used(V, -1);\n  \
    \  used[start] = start;\n \n    T ret = 0;\n    for(int s = 0; s < V; s++) {\n\
    \      stack< int > path;\n      for(int u = s; used[u] < 0;) {\n        path.push(u);\n\
    \        used[u] = s;\n        if(heap.empty(heaps[u])) return -1;\n        auto\
    \ p = heap.top(heaps[u]);\n        ret += p.first;\n        heap.add(heaps[u],\
    \ -p.first);\n        heap.pop(heaps[u]);\n        int v = uf.find(p.second);\n\
    \        if(used[v] == s) {\n          int w;\n          Node *nextheap = heap.makeheap();\n\
    \          do {\n            w = path.top();\n            path.pop();\n      \
    \      nextheap = heap.merge(nextheap, heaps[w]);\n          } while(uf.unite(v,\
    \ w));\n          heaps[uf.find(v)] = nextheap;\n          used[uf.find(v)] =\
    \ -1;\n        }\n        u = uf.find(v);\n      }\n    }\n    return ret;\n \
    \ }\n};\n#line 10 \"test/verify/aoj-grl-2-b.test.cpp\"\n\nint main() {\n  int\
    \ V, E, R;\n  scanf(\"%d %d %d\", &V, &E, &R);\n  Edges< int > edges;\n  for(int\
    \ i = 0; i < E; i++) {\n    int a, b, c;\n    scanf(\"%d %d %d\", &a, &b, &c);\n\
    \    edges.emplace_back(a, b, c);\n  }\n  printf(\"%d\\n\", MinimumSpanningTreeArborescence<\
    \ int >(edges, V).build(R));\n}\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_2_B\"\
    \n\n#include \"../../template/template.cpp\"\n#include \"../../graph/template.cpp\"\
    \n\n#include \"../../structure/union-find/union-find.cpp\"\n#include \"../../structure/heap/skew-heap.cpp\"\
    \n\n#include \"../../graph/mst/chu-liu-edmond.cpp\"\n\nint main() {\n  int V,\
    \ E, R;\n  scanf(\"%d %d %d\", &V, &E, &R);\n  Edges< int > edges;\n  for(int\
    \ i = 0; i < E; i++) {\n    int a, b, c;\n    scanf(\"%d %d %d\", &a, &b, &c);\n\
    \    edges.emplace_back(a, b, c);\n  }\n  printf(\"%d\\n\", MinimumSpanningTreeArborescence<\
    \ int >(edges, V).build(R));\n}\n"
  dependsOn:
  - template/template.cpp
  - graph/template.cpp
  - structure/union-find/union-find.cpp
  - structure/heap/skew-heap.cpp
  - graph/mst/chu-liu-edmond.cpp
  isVerificationFile: true
  path: test/verify/aoj-grl-2-b.test.cpp
  requiredBy: []
  timestamp: '2020-02-19 21:42:58+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-grl-2-b.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-grl-2-b.test.cpp
- /verify/test/verify/aoj-grl-2-b.test.cpp.html
title: test/verify/aoj-grl-2-b.test.cpp
---
