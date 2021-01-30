---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: structure/segment-tree/segment-tree.cpp
    title: "Segment-Tree(\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)"
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_A
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_A
  bundledCode: "#line 1 \"test/verify/aoj-dsl-2-a.test.cpp\"\n#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_A\"\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/aoj-dsl-2-a.test.cpp\"\
    \n\n#line 1 \"structure/segment-tree/segment-tree.cpp\"\n/**\n * @brief Segment-Tree(\u30BB\
    \u30B0\u30E1\u30F3\u30C8\u6728)\n * @docs docs/segment-tree.md\n */\ntemplate<\
    \ typename Monoid, typename F >\nstruct SegmentTree {\n  int sz;\n  vector< Monoid\
    \ > seg;\n\n  const F f;\n  const Monoid M1;\n  \n  SegmentTree(int n, const F\
    \ f, const Monoid &M1) : f(f), M1(M1) {\n    sz = 1;\n    while(sz < n) sz <<=\
    \ 1;\n    seg.assign(2 * sz, M1);\n  }\n\n  void set(int k, const Monoid &x) {\n\
    \    seg[k + sz] = x;\n  }\n\n  void build() {\n    for(int k = sz - 1; k > 0;\
    \ k--) {\n      seg[k] = f(seg[2 * k + 0], seg[2 * k + 1]);\n    }\n  }\n\n  void\
    \ update(int k, const Monoid &x) {\n    k += sz;\n    seg[k] = x;\n    while(k\
    \ >>= 1) {\n      seg[k] = f(seg[2 * k + 0], seg[2 * k + 1]);\n    }\n  }\n\n\
    \  Monoid query(int a, int b) {\n    Monoid L = M1, R = M1;\n    for(a += sz,\
    \ b += sz; a < b; a >>= 1, b >>= 1) {\n      if(a & 1) L = f(L, seg[a++]);\n \
    \     if(b & 1) R = f(seg[--b], R);\n    }\n    return f(L, R);\n  }\n\n  Monoid\
    \ operator[](const int &k) const {\n    return seg[k + sz];\n  }\n\n  template<\
    \ typename C >\n  int find_subtree(int a, const C &check, Monoid &M, bool type)\
    \ {\n    while(a < sz) {\n      Monoid nxt = type ? f(seg[2 * a + type], M) :\
    \ f(M, seg[2 * a + type]);\n      if(check(nxt)) a = 2 * a + type;\n      else\
    \ M = nxt, a = 2 * a + 1 - type;\n    }\n    return a - sz;\n  }\n\n  template<\
    \ typename C >\n  int find_first(int a, const C &check) {\n    Monoid L = M1;\n\
    \    if(a <= 0) {\n      if(check(f(L, seg[1]))) return find_subtree(1, check,\
    \ L, false);\n      return -1;\n    }\n    int b = sz;\n    for(a += sz, b +=\
    \ sz; a < b; a >>= 1, b >>= 1) {\n      if(a & 1) {\n        Monoid nxt = f(L,\
    \ seg[a]);\n        if(check(nxt)) return find_subtree(a, check, L, false);\n\
    \        L = nxt;\n        ++a;\n      }\n    }\n    return -1;\n  }\n\n  template<\
    \ typename C >\n  int find_last(int b, const C &check) {\n    Monoid R = M1;\n\
    \    if(b >= sz) {\n      if(check(f(seg[1], R))) return find_subtree(1, check,\
    \ R, true);\n      return -1;\n    }\n    int a = sz;\n    for(b += sz; a < b;\
    \ a >>= 1, b >>= 1) {\n      if(b & 1) {\n        Monoid nxt = f(seg[--b], R);\n\
    \        if(check(nxt)) return find_subtree(b, check, R, true);\n        R = nxt;\n\
    \      }\n    }\n    return -1;\n  }\n};\n\ntemplate< typename Monoid, typename\
    \ F >\nSegmentTree< Monoid, F > get_segment_tree(int N, const F& f, const Monoid&\
    \ M1) {\n  return {N, f, M1};\n}\n#line 6 \"test/verify/aoj-dsl-2-a.test.cpp\"\
    \n\nint main() {\n  int N, Q;\n  scanf(\"%d %d\", &N, &Q);\n  auto seg = get_segment_tree(N,\
    \ [](int a, int b) { return min(a, b); }, INT_MAX);\n  while(Q--) {\n    int T,\
    \ X, Y;\n    scanf(\"%d %d %d\", &T, &X, &Y);\n    if(T == 0) seg.update(X, Y);\n\
    \    else printf(\"%d\\n\", seg.query(X, Y + 1));\n  }\n}\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_A\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../structure/segment-tree/segment-tree.cpp\"\
    \n\nint main() {\n  int N, Q;\n  scanf(\"%d %d\", &N, &Q);\n  auto seg = get_segment_tree(N,\
    \ [](int a, int b) { return min(a, b); }, INT_MAX);\n  while(Q--) {\n    int T,\
    \ X, Y;\n    scanf(\"%d %d %d\", &T, &X, &Y);\n    if(T == 0) seg.update(X, Y);\n\
    \    else printf(\"%d\\n\", seg.query(X, Y + 1));\n  }\n}\n"
  dependsOn:
  - template/template.cpp
  - structure/segment-tree/segment-tree.cpp
  isVerificationFile: true
  path: test/verify/aoj-dsl-2-a.test.cpp
  requiredBy: []
  timestamp: '2020-09-08 00:52:50+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-dsl-2-a.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-dsl-2-a.test.cpp
- /verify/test/verify/aoj-dsl-2-a.test.cpp.html
title: test/verify/aoj-dsl-2-a.test.cpp
---
