---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-2-b.test.cpp
    title: test/verify/aoj-grl-2-b.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"graph/mst/chu-liu-edmond.cpp\"\ntemplate< typename T >\n\
    struct MinimumSpanningTreeArborescence\n{\n  using Pi = pair< T, int >;\n  using\
    \ Heap = SkewHeap< Pi, int >;\n  using Node = typename Heap::Node;\n  const Edges<\
    \ T > &es;\n  const int V;\n  T INF;\n \n  MinimumSpanningTreeArborescence(const\
    \ Edges< T > &es, int V) :\n      INF(numeric_limits< T >::max()), es(es), V(V)\
    \ {}\n \n  T build(int start)\n  {\n    auto g = [](const Pi &a, const T &b) {\
    \ return Pi(a.first + b, a.second); };\n    auto h = [](const T &a, const T &b)\
    \ { return a + b; };\n    Heap heap(g, h);\n    vector< Node * > heaps(V, heap.makeheap());\n\
    \    for(auto &e : es) heap.push(heaps[e.to], {e.cost, e.src});\n    UnionFind\
    \ uf(V);\n    vector< int > used(V, -1);\n    used[start] = start;\n \n    T ret\
    \ = 0;\n    for(int s = 0; s < V; s++) {\n      stack< int > path;\n      for(int\
    \ u = s; used[u] < 0;) {\n        path.push(u);\n        used[u] = s;\n      \
    \  if(heap.empty(heaps[u])) return -1;\n        auto p = heap.top(heaps[u]);\n\
    \        ret += p.first;\n        heap.add(heaps[u], -p.first);\n        heap.pop(heaps[u]);\n\
    \        int v = uf.find(p.second);\n        if(used[v] == s) {\n          int\
    \ w;\n          Node *nextheap = heap.makeheap();\n          do {\n          \
    \  w = path.top();\n            path.pop();\n            nextheap = heap.merge(nextheap,\
    \ heaps[w]);\n          } while(uf.unite(v, w));\n          heaps[uf.find(v)]\
    \ = nextheap;\n          used[uf.find(v)] = -1;\n        }\n        u = uf.find(v);\n\
    \      }\n    }\n    return ret;\n  }\n};\n"
  code: "template< typename T >\nstruct MinimumSpanningTreeArborescence\n{\n  using\
    \ Pi = pair< T, int >;\n  using Heap = SkewHeap< Pi, int >;\n  using Node = typename\
    \ Heap::Node;\n  const Edges< T > &es;\n  const int V;\n  T INF;\n \n  MinimumSpanningTreeArborescence(const\
    \ Edges< T > &es, int V) :\n      INF(numeric_limits< T >::max()), es(es), V(V)\
    \ {}\n \n  T build(int start)\n  {\n    auto g = [](const Pi &a, const T &b) {\
    \ return Pi(a.first + b, a.second); };\n    auto h = [](const T &a, const T &b)\
    \ { return a + b; };\n    Heap heap(g, h);\n    vector< Node * > heaps(V, heap.makeheap());\n\
    \    for(auto &e : es) heap.push(heaps[e.to], {e.cost, e.src});\n    UnionFind\
    \ uf(V);\n    vector< int > used(V, -1);\n    used[start] = start;\n \n    T ret\
    \ = 0;\n    for(int s = 0; s < V; s++) {\n      stack< int > path;\n      for(int\
    \ u = s; used[u] < 0;) {\n        path.push(u);\n        used[u] = s;\n      \
    \  if(heap.empty(heaps[u])) return -1;\n        auto p = heap.top(heaps[u]);\n\
    \        ret += p.first;\n        heap.add(heaps[u], -p.first);\n        heap.pop(heaps[u]);\n\
    \        int v = uf.find(p.second);\n        if(used[v] == s) {\n          int\
    \ w;\n          Node *nextheap = heap.makeheap();\n          do {\n          \
    \  w = path.top();\n            path.pop();\n            nextheap = heap.merge(nextheap,\
    \ heaps[w]);\n          } while(uf.unite(v, w));\n          heaps[uf.find(v)]\
    \ = nextheap;\n          used[uf.find(v)] = -1;\n        }\n        u = uf.find(v);\n\
    \      }\n    }\n    return ret;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: graph/mst/chu-liu-edmond.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:02:43+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-2-b.test.cpp
documentation_of: graph/mst/chu-liu-edmond.cpp
layout: document
redirect_from:
- /library/graph/mst/chu-liu-edmond.cpp
- /library/graph/mst/chu-liu-edmond.cpp.html
title: graph/mst/chu-liu-edmond.cpp
---
