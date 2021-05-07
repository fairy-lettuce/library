---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/bbst/rbst.cpp\"\ntemplate< typename T, typename\
    \ F >\nstruct RBST : MergeSplitBasedBBST< T, F > {\nprivate:\n  using MergeSplitBasedBBST<\
    \ T, F >::MergeSplitBasedBBST;\n  using NP = typename MergeSplitBasedBBST< T,\
    \ F >::NP;\n  using MergeSplitBasedBBST< T, F >::count;\n  using MergeSplitBasedBBST<\
    \ T, F >::update;\n\n  int xor128() {\n    static int x = 123456789;\n    static\
    \ int y = 362436069;\n    static int z = 521288629;\n    static int w = 88675123;\n\
    \    int t;\n\n    t = x ^ (x << 11);\n    x = y;\n    y = z;\n    z = w;\n  \
    \  return w = (w ^ (w >> 19)) ^ (t ^ (t >> 8));\n  }\n\n  NP imp_merge(NP l, NP\
    \ r) override {\n    if(!l || !r) return l ? l : r;\n    if(xor128() % (count(l)\
    \ + count(r)) < count(l)) {\n      l->ch[1] = imp_merge(l->ch[1], r);\n      return\
    \ update(l);\n    } else {\n      r->ch[0] = imp_merge(l, r->ch[0]);\n      return\
    \ update(r);\n    }\n  }\n\n  pair< NP, NP > imp_split(NP t, int k) override {\n\
    \    if(!t) return {t, t};\n    if(k <= count(t->ch[0])) {\n      auto s = imp_split(t->ch[0],\
    \ k);\n      t->ch[0] = s.second;\n      return {s.first, update(t)};\n    } else\
    \ {\n      auto s = imp_split(t->ch[1], k - count(t->ch[0]) - 1);\n      t->ch[1]\
    \ = s.first;\n      return {update(t), s.second};\n    }\n  }\n\npublic:\n  void\
    \ set_element(NP &t, int k, const T &x) {\n    if(k < count(t->ch[0])) set_element(t->ch[0],\
    \ k, x);\n    else if(k == count(t->ch[0])) t->key = t->sum = x;\n    else set_element(t->ch[1],\
    \ k - count(t->ch[0]) - 1, x);\n    t = update(t);\n  }\n};\n"
  code: "template< typename T, typename F >\nstruct RBST : MergeSplitBasedBBST< T,\
    \ F > {\nprivate:\n  using MergeSplitBasedBBST< T, F >::MergeSplitBasedBBST;\n\
    \  using NP = typename MergeSplitBasedBBST< T, F >::NP;\n  using MergeSplitBasedBBST<\
    \ T, F >::count;\n  using MergeSplitBasedBBST< T, F >::update;\n\n  int xor128()\
    \ {\n    static int x = 123456789;\n    static int y = 362436069;\n    static\
    \ int z = 521288629;\n    static int w = 88675123;\n    int t;\n\n    t = x ^\
    \ (x << 11);\n    x = y;\n    y = z;\n    z = w;\n    return w = (w ^ (w >> 19))\
    \ ^ (t ^ (t >> 8));\n  }\n\n  NP imp_merge(NP l, NP r) override {\n    if(!l ||\
    \ !r) return l ? l : r;\n    if(xor128() % (count(l) + count(r)) < count(l)) {\n\
    \      l->ch[1] = imp_merge(l->ch[1], r);\n      return update(l);\n    } else\
    \ {\n      r->ch[0] = imp_merge(l, r->ch[0]);\n      return update(r);\n    }\n\
    \  }\n\n  pair< NP, NP > imp_split(NP t, int k) override {\n    if(!t) return\
    \ {t, t};\n    if(k <= count(t->ch[0])) {\n      auto s = imp_split(t->ch[0],\
    \ k);\n      t->ch[0] = s.second;\n      return {s.first, update(t)};\n    } else\
    \ {\n      auto s = imp_split(t->ch[1], k - count(t->ch[0]) - 1);\n      t->ch[1]\
    \ = s.first;\n      return {update(t), s.second};\n    }\n  }\n\npublic:\n  void\
    \ set_element(NP &t, int k, const T &x) {\n    if(k < count(t->ch[0])) set_element(t->ch[0],\
    \ k, x);\n    else if(k == count(t->ch[0])) t->key = t->sum = x;\n    else set_element(t->ch[1],\
    \ k - count(t->ch[0]) - 1, x);\n    t = update(t);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/bbst/rbst.cpp
  requiredBy: []
  timestamp: '2021-05-07 20:07:14+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/bbst/rbst.cpp
layout: document
redirect_from:
- /library/structure/bbst/rbst.cpp
- /library/structure/bbst/rbst.cpp.html
title: structure/bbst/rbst.cpp
---
