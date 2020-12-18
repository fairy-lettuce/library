---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-2415.test.cpp
    title: test/verify/aoj-2415.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 1 \"dp/hu-tucker.cpp\"\ntemplate< typename Heap, typename T\
    \ >\nT hu_tucker(vector< T > vs, T INF) {\n  int N = (int) vs.size();\n  Heap\
    \ heap;\n  vector< typename Heap::Node * > hs(N - 1, heap.makeheap());\n  vector<\
    \ int > ls(N), rs(N);\n  vector< T > cs(N - 1);\n  using pi = pair< T, int >;\n\
    \  priority_queue< pi, vector< pi >, greater< pi > > que;\n  for(int i = 0; i\
    \ + 1 < N; i++) {\n    ls[i] = i - 1;\n    rs[i] = i + 1;\n    cs[i] = vs[i] +\
    \ vs[i + 1];\n    que.emplace(cs[i], i);\n  }\n  T ret = 0;\n  for(int k = 0;\
    \ k + 1 < N; k++) {\n    T c;\n    int i;\n    do {\n      tie(c, i) = que.top();\n\
    \      que.pop();\n    } while(rs[i] < 0 || cs[i] != c);\n \n    bool ml = false,\
    \ mr = false;\n    if(!heap.empty(hs[i]) && vs[i] + heap.top(hs[i]) == c) {\n\
    \      heap.pop(hs[i]);\n      ml = true;\n    } else if(vs[i] + vs[rs[i]] ==\
    \ c) {\n      ml = mr = true;\n    } else {\n      auto top = heap.pop(hs[i]);\n\
    \      if(!heap.empty(hs[i]) && heap.top(hs[i]) + top == c) {\n        heap.pop(hs[i]);\n\
    \      } else {\n        mr = true;\n      }\n    }\n    ret += c;\n    heap.push(hs[i],\
    \ c);\n    if(ml) vs[i] = INF;\n    if(mr) vs[rs[i]] = INF;\n \n    if(ml && i\
    \ > 0) {\n      int j = ls[i];\n      hs[j] = heap.merge(hs[j], hs[i]);\n    \
    \  rs[j] = rs[i];\n      rs[i] = -1;\n      ls[rs[j]] = j;\n      i = j;\n   \
    \ }\n \n    if(mr && rs[i] + 1 < N) {\n      int j = rs[i];\n      hs[i] = heap.merge(hs[i],\
    \ hs[j]);\n      rs[i] = rs[j];\n      rs[j] = -1;\n      ls[rs[i]] = i;\n   \
    \ }\n    cs[i] = vs[i] + vs[rs[i]];\n \n    if(!heap.empty(hs[i])) {\n      T\
    \ top = heap.pop(hs[i]);\n      cs[i] = min(cs[i], min(vs[i], vs[rs[i]]) + top);\n\
    \      if(!heap.empty(hs[i])) cs[i] = min(cs[i], top + heap.top(hs[i]));\n   \
    \   heap.push(hs[i], top);\n    }\n    que.emplace(cs[i], i);\n  }\n  return ret;\n\
    }\n"
  code: "template< typename Heap, typename T >\nT hu_tucker(vector< T > vs, T INF)\
    \ {\n  int N = (int) vs.size();\n  Heap heap;\n  vector< typename Heap::Node *\
    \ > hs(N - 1, heap.makeheap());\n  vector< int > ls(N), rs(N);\n  vector< T >\
    \ cs(N - 1);\n  using pi = pair< T, int >;\n  priority_queue< pi, vector< pi >,\
    \ greater< pi > > que;\n  for(int i = 0; i + 1 < N; i++) {\n    ls[i] = i - 1;\n\
    \    rs[i] = i + 1;\n    cs[i] = vs[i] + vs[i + 1];\n    que.emplace(cs[i], i);\n\
    \  }\n  T ret = 0;\n  for(int k = 0; k + 1 < N; k++) {\n    T c;\n    int i;\n\
    \    do {\n      tie(c, i) = que.top();\n      que.pop();\n    } while(rs[i] <\
    \ 0 || cs[i] != c);\n \n    bool ml = false, mr = false;\n    if(!heap.empty(hs[i])\
    \ && vs[i] + heap.top(hs[i]) == c) {\n      heap.pop(hs[i]);\n      ml = true;\n\
    \    } else if(vs[i] + vs[rs[i]] == c) {\n      ml = mr = true;\n    } else {\n\
    \      auto top = heap.pop(hs[i]);\n      if(!heap.empty(hs[i]) && heap.top(hs[i])\
    \ + top == c) {\n        heap.pop(hs[i]);\n      } else {\n        mr = true;\n\
    \      }\n    }\n    ret += c;\n    heap.push(hs[i], c);\n    if(ml) vs[i] = INF;\n\
    \    if(mr) vs[rs[i]] = INF;\n \n    if(ml && i > 0) {\n      int j = ls[i];\n\
    \      hs[j] = heap.merge(hs[j], hs[i]);\n      rs[j] = rs[i];\n      rs[i] =\
    \ -1;\n      ls[rs[j]] = j;\n      i = j;\n    }\n \n    if(mr && rs[i] + 1 <\
    \ N) {\n      int j = rs[i];\n      hs[i] = heap.merge(hs[i], hs[j]);\n      rs[i]\
    \ = rs[j];\n      rs[j] = -1;\n      ls[rs[i]] = i;\n    }\n    cs[i] = vs[i]\
    \ + vs[rs[i]];\n \n    if(!heap.empty(hs[i])) {\n      T top = heap.pop(hs[i]);\n\
    \      cs[i] = min(cs[i], min(vs[i], vs[rs[i]]) + top);\n      if(!heap.empty(hs[i]))\
    \ cs[i] = min(cs[i], top + heap.top(hs[i]));\n      heap.push(hs[i], top);\n \
    \   }\n    que.emplace(cs[i], i);\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: dp/hu-tucker.cpp
  requiredBy: []
  timestamp: '2019-12-20 16:29:52+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-2415.test.cpp
documentation_of: dp/hu-tucker.cpp
layout: document
redirect_from:
- /library/dp/hu-tucker.cpp
- /library/dp/hu-tucker.cpp.html
title: dp/hu-tucker.cpp
---
