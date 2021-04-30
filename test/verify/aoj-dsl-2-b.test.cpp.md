---
data:
  _extendedDependsOn:
  - icon: ':question:'
    path: structure/others/binary-indexed-tree.cpp
    title: Binary-Indexed-Tree(BIT)
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
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B
  bundledCode: "#line 1 \"test/verify/aoj-dsl-2-b.test.cpp\"\n#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B\"\
    \n\n#line 1 \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace\
    \ std;\n\nusing int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll\
    \ = (1LL << 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup()\
    \ {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed\
    \ << setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
    \ntemplate< typename T1, typename T2 >\nostream &operator<<(ostream &os, const\
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
    \  explicit FixPoint(F &&f) : F(forward< F >(f)) {}\n\n  template< typename...\
    \ Args >\n  decltype(auto) operator()(Args &&... args) const {\n    return F::operator()(*this,\
    \ forward< Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/aoj-dsl-2-b.test.cpp\"\
    \n\n#line 1 \"structure/others/binary-indexed-tree.cpp\"\n/**\n * @brief Binary-Indexed-Tree(BIT)\n\
    \ * @docs docs/binary-indexed-tree.md\n */\ntemplate< typename T >\nstruct BinaryIndexedTree\
    \ {\nprivate:\n  vector< T > data;\n\npublic:\n  BinaryIndexedTree() = default;\n\
    \n  explicit BinaryIndexedTree(size_t sz) : data(sz + 1, 0) {}\n\n  explicit BinaryIndexedTree(const\
    \ vector< T > &vs) : data(vs.size() + 1, 0) {\n    for(size_t i = 0; i < vs.size();\
    \ i++) data[i + 1] = vs[i];\n    for(size_t i = 1; i < data.size(); i++) {\n \
    \     size_t j = i + (i & -i);\n      if(j < data.size()) data[j] += data[i];\n\
    \    }\n  }\n\n  void add(int k, const T &x) {\n    for(++k; k < (int) data.size();\
    \ k += k & -k) data[k] += x;\n  }\n\n  T sum(int r) const {\n    T ret = T();\n\
    \    for(; r > 0; r -= r & -r) ret += data[r];\n    return ret;\n  }\n\n  T sum(int\
    \ l, int r) const {\n    return sum(r) - sum(l);\n  }\n\n  int lower_bound(T x)\
    \ const {\n    int i = 0;\n    for(int k = 1 << (__lg(data.size() - 1) + 1); k\
    \ > 0; k >>= 1) {\n      if(i + k < data.size() && data[i + k] < x) {\n      \
    \  x -= data[i + k];\n        i += k;\n      }\n    }\n    return i;\n  }\n\n\
    \  int upper_bound(T x) const {\n    int i = 0;\n    for(int k = 1 << (__lg(data.size()\
    \ - 1) + 1); k > 0; k >>= 1) {\n      if(i + k < data.size() && data[i + k] <=\
    \ x) {\n        x -= data[i + k];\n        i += k;\n      }\n    }\n    return\
    \ i;\n  }\n};\n#line 6 \"test/verify/aoj-dsl-2-b.test.cpp\"\n\nint main() {\n\
    \  int N, Q;\n  cin >> N >> Q;\n  BinaryIndexedTree< int > bit(N);\n  while(Q--)\
    \ {\n    int T, X, Y;\n    cin >> T >> X >> Y;\n    if(T == 0) bit.add(X - 1,\
    \ Y);\n    else cout << bit.sum(X - 1, Y) << \"\\n\";\n  }\n}\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_B\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../structure/others/binary-indexed-tree.cpp\"\
    \n\nint main() {\n  int N, Q;\n  cin >> N >> Q;\n  BinaryIndexedTree< int > bit(N);\n\
    \  while(Q--) {\n    int T, X, Y;\n    cin >> T >> X >> Y;\n    if(T == 0) bit.add(X\
    \ - 1, Y);\n    else cout << bit.sum(X - 1, Y) << \"\\n\";\n  }\n}\n"
  dependsOn:
  - template/template.cpp
  - structure/others/binary-indexed-tree.cpp
  isVerificationFile: true
  path: test/verify/aoj-dsl-2-b.test.cpp
  requiredBy: []
  timestamp: '2021-05-01 00:06:55+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-dsl-2-b.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-dsl-2-b.test.cpp
- /verify/test/verify/aoj-dsl-2-b.test.cpp.html
title: test/verify/aoj-dsl-2-b.test.cpp
---
