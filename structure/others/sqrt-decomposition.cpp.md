---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/others/sqrt-decomposition.cpp\"\ntemplate< typename\
    \ T, typename E = int >\nstruct SqrtDecomposition {\n\n  vector< E > block_add,\
    \ elem_add;\n  vector< int > block_pos;\n  vector< T > data, lsum;\n  vector<\
    \ vector< T > > sum;\n  int N, B, K;\n  E L;\n\n  SqrtDecomposition(int N, E L\
    \ = 0) : N(N), L(L) { // find the sum of L or more in the interval\n    B = (int)\
    \ sqrt(N);\n    K = (N + B - 1) / B;\n\n    block_add.assign(K, 0);\n    block_pos.resize(N);\n\
    \    for(int k = 0; k < K; k++) {\n      for(int i = k * B; i < min((k + 1) *\
    \ B, N); i++) block_pos[i] = k;\n    }\n    elem_add.assign(N, 0);\n    data.assign(N,\
    \ 0);\n    sum.assign(K, vector< T >(B, 0));\n    lsum.assign(K, 0);\n  }\n\n\n\
    \  void build(const vector< E > &add, const vector< T > &dat) {\n    assert(add.size()\
    \ == elem_add.size());\n    assert(dat.size() == data.size());\n    elem_add =\
    \ add;\n    data = dat;\n    for(int k = 0; k < K; k++) {\n      E tap = elem_add[k\
    \ * B];\n      for(int i = k * B; i < min((k + 1) * B, N); i++) tap = min(tap,\
    \ elem_add[i]);\n      block_add[k] = tap;\n      for(int i = k * B; i < min((k\
    \ + 1) * B, N); i++) {\n        elem_add[i] -= block_add[k];\n        set(i, dat[i]);\n\
    \      }\n    }\n  }\n\n  inline void del(int k) {\n    sum[block_pos[k]][elem_add[k]]\
    \ -= data[k];\n    if(block_add[block_pos[k]] + elem_add[k] >= L) lsum[block_pos[k]]\
    \ -= data[k];\n  }\n\n  inline void set(int k) {\n    while(sum[block_pos[k]].size()\
    \ <= elem_add[k]) sum[block_pos[k]].push_back(0);\n    sum[block_pos[k]][elem_add[k]]\
    \ += data[k];\n    if(block_add[block_pos[k]] + elem_add[k] >= L) lsum[block_pos[k]]\
    \ += data[k];\n  }\n\n  void set(int k, T x) {\n    data[k] = x;\n    set(k);\n\
    \  }\n\n  void add(int a, int b) {\n    for(int k = 0; k < K; k++) {\n      int\
    \ l = k * B;\n      int r = min(l + B, N);\n\n      if(r <= a || b <= l) {\n\n\
    \      } else if(a <= l && r <= b) {\n        block_add[k]++;\n        if(0 <=\
    \ L - block_add[k] && L - block_add[k] < sum[k].size()) {\n          lsum[k] +=\
    \ sum[k][L - block_add[k]];\n        }\n      } else {\n        for(int i = max(a,\
    \ l); i < min(b, r); i++) {\n          del(i);\n          elem_add[i]++;\n   \
    \       set(i);\n        }\n      }\n    }\n  }\n\n\n  void sub(int a, int b)\
    \ {\n    for(int k = 0; k < K; k++) {\n      int l = k * B;\n      int r = min(l\
    \ + B, N);\n\n      if(r <= a || b <= l) {\n\n      } else if(a <= l && r <= b)\
    \ {\n        if(0 <= L - block_add[k] && L - block_add[k] < sum[k].size()) {\n\
    \          lsum[k] -= sum[k][L - block_add[k]];\n        }\n        block_add[k]--;\n\
    \      } else {\n        if(0 <= L - block_add[k] && L - block_add[k] < sum[k].size())\
    \ {\n          lsum[k] -= sum[k][L - block_add[k]];\n        }\n        block_add[k]--;\n\
    \        for(int i = l; i < max(a, l); i++) {\n          del(i);\n          elem_add[i]++;\n\
    \          set(i);\n        }\n        for(int i = min(b, r); i < r; i++) {\n\
    \          del(i);\n          elem_add[i]++;\n          set(i);\n        }\n \
    \     }\n    }\n  }\n\n\n  T query(int a, int b, E x) {\n    T ret = 0;\n    for(int\
    \ k = 0; k < K; k++) {\n      int l = k * B;\n      int r = min(l + B, N);\n\n\
    \      if(r <= a || b <= l) {\n\n      } else if(a <= l && r <= b) {\n       \
    \ if(0 <= x - block_add[k] && x - block_add[k] < sum[k].size()) {\n          ret\
    \ += sum[k][x - block_add[k]];\n        }\n      } else {\n        for(int i =\
    \ max(a, l); i < min(b, r); i++) {\n          if(block_add[k] + elem_add[i] ==\
    \ x) ret += data[i];\n        }\n      }\n    }\n    return ret;\n  }\n\n\n  T\
    \ query_low(int a, int b) {\n    T ret = 0;\n    for(int k = 0; k < K; k++) {\n\
    \      int l = k * B;\n      int r = min(l + B, N);\n\n      if(r <= a || b <=\
    \ l) {\n\n      } else if(a <= l && r <= b) {\n        ret += lsum[k];\n     \
    \ } else {\n        for(int i = max(a, l); i < min(b, r); i++) {\n          if(block_add[k]\
    \ + elem_add[i] >= L) ret += data[i];\n        }\n      }\n    }\n    return ret;\n\
    \  }\n};\n"
  code: "template< typename T, typename E = int >\nstruct SqrtDecomposition {\n\n\
    \  vector< E > block_add, elem_add;\n  vector< int > block_pos;\n  vector< T >\
    \ data, lsum;\n  vector< vector< T > > sum;\n  int N, B, K;\n  E L;\n\n  SqrtDecomposition(int\
    \ N, E L = 0) : N(N), L(L) { // find the sum of L or more in the interval\n  \
    \  B = (int) sqrt(N);\n    K = (N + B - 1) / B;\n\n    block_add.assign(K, 0);\n\
    \    block_pos.resize(N);\n    for(int k = 0; k < K; k++) {\n      for(int i =\
    \ k * B; i < min((k + 1) * B, N); i++) block_pos[i] = k;\n    }\n    elem_add.assign(N,\
    \ 0);\n    data.assign(N, 0);\n    sum.assign(K, vector< T >(B, 0));\n    lsum.assign(K,\
    \ 0);\n  }\n\n\n  void build(const vector< E > &add, const vector< T > &dat) {\n\
    \    assert(add.size() == elem_add.size());\n    assert(dat.size() == data.size());\n\
    \    elem_add = add;\n    data = dat;\n    for(int k = 0; k < K; k++) {\n    \
    \  E tap = elem_add[k * B];\n      for(int i = k * B; i < min((k + 1) * B, N);\
    \ i++) tap = min(tap, elem_add[i]);\n      block_add[k] = tap;\n      for(int\
    \ i = k * B; i < min((k + 1) * B, N); i++) {\n        elem_add[i] -= block_add[k];\n\
    \        set(i, dat[i]);\n      }\n    }\n  }\n\n  inline void del(int k) {\n\
    \    sum[block_pos[k]][elem_add[k]] -= data[k];\n    if(block_add[block_pos[k]]\
    \ + elem_add[k] >= L) lsum[block_pos[k]] -= data[k];\n  }\n\n  inline void set(int\
    \ k) {\n    while(sum[block_pos[k]].size() <= elem_add[k]) sum[block_pos[k]].push_back(0);\n\
    \    sum[block_pos[k]][elem_add[k]] += data[k];\n    if(block_add[block_pos[k]]\
    \ + elem_add[k] >= L) lsum[block_pos[k]] += data[k];\n  }\n\n  void set(int k,\
    \ T x) {\n    data[k] = x;\n    set(k);\n  }\n\n  void add(int a, int b) {\n \
    \   for(int k = 0; k < K; k++) {\n      int l = k * B;\n      int r = min(l +\
    \ B, N);\n\n      if(r <= a || b <= l) {\n\n      } else if(a <= l && r <= b)\
    \ {\n        block_add[k]++;\n        if(0 <= L - block_add[k] && L - block_add[k]\
    \ < sum[k].size()) {\n          lsum[k] += sum[k][L - block_add[k]];\n       \
    \ }\n      } else {\n        for(int i = max(a, l); i < min(b, r); i++) {\n  \
    \        del(i);\n          elem_add[i]++;\n          set(i);\n        }\n   \
    \   }\n    }\n  }\n\n\n  void sub(int a, int b) {\n    for(int k = 0; k < K; k++)\
    \ {\n      int l = k * B;\n      int r = min(l + B, N);\n\n      if(r <= a ||\
    \ b <= l) {\n\n      } else if(a <= l && r <= b) {\n        if(0 <= L - block_add[k]\
    \ && L - block_add[k] < sum[k].size()) {\n          lsum[k] -= sum[k][L - block_add[k]];\n\
    \        }\n        block_add[k]--;\n      } else {\n        if(0 <= L - block_add[k]\
    \ && L - block_add[k] < sum[k].size()) {\n          lsum[k] -= sum[k][L - block_add[k]];\n\
    \        }\n        block_add[k]--;\n        for(int i = l; i < max(a, l); i++)\
    \ {\n          del(i);\n          elem_add[i]++;\n          set(i);\n        }\n\
    \        for(int i = min(b, r); i < r; i++) {\n          del(i);\n          elem_add[i]++;\n\
    \          set(i);\n        }\n      }\n    }\n  }\n\n\n  T query(int a, int b,\
    \ E x) {\n    T ret = 0;\n    for(int k = 0; k < K; k++) {\n      int l = k *\
    \ B;\n      int r = min(l + B, N);\n\n      if(r <= a || b <= l) {\n\n      }\
    \ else if(a <= l && r <= b) {\n        if(0 <= x - block_add[k] && x - block_add[k]\
    \ < sum[k].size()) {\n          ret += sum[k][x - block_add[k]];\n        }\n\
    \      } else {\n        for(int i = max(a, l); i < min(b, r); i++) {\n      \
    \    if(block_add[k] + elem_add[i] == x) ret += data[i];\n        }\n      }\n\
    \    }\n    return ret;\n  }\n\n\n  T query_low(int a, int b) {\n    T ret = 0;\n\
    \    for(int k = 0; k < K; k++) {\n      int l = k * B;\n      int r = min(l +\
    \ B, N);\n\n      if(r <= a || b <= l) {\n\n      } else if(a <= l && r <= b)\
    \ {\n        ret += lsum[k];\n      } else {\n        for(int i = max(a, l); i\
    \ < min(b, r); i++) {\n          if(block_add[k] + elem_add[i] >= L) ret += data[i];\n\
    \        }\n      }\n    }\n    return ret;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/sqrt-decomposition.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/others/sqrt-decomposition.cpp
layout: document
redirect_from:
- /library/structure/others/sqrt-decomposition.cpp
- /library/structure/others/sqrt-decomposition.cpp.html
title: structure/others/sqrt-decomposition.cpp
---
