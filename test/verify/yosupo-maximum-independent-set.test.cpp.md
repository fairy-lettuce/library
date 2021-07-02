---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/others/maximum-independent-set.hpp
    title: graph/others/maximum-independent-set.hpp
  - icon: ':heavy_check_mark:'
    path: graph/template.hpp
    title: graph/template.hpp
  - icon: ':heavy_check_mark:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/maximum_independent_set
    links:
    - https://judge.yosupo.jp/problem/maximum_independent_set
  bundledCode: "#line 1 \"test/verify/yosupo-maximum-independent-set.test.cpp\"\n\
    #define PROBLEM \"https://judge.yosupo.jp/problem/maximum_independent_set\"\n\n\
    #line 1 \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-maximum-independent-set.test.cpp\"\
    \n\n#line 2 \"graph/others/maximum-independent-set.hpp\"\n\n#line 2 \"graph/template.hpp\"\
    \n\ntemplate< typename T >\nstruct edge {\n  int src, to;\n  T cost;\n\n  edge(int\
    \ to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int src, int to, T cost)\
    \ : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const int &x) {\n   \
    \ to = x;\n    return *this;\n  }\n\n  operator int() const { return to; }\n};\n\
    \ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate< typename\
    \ T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph = vector<\
    \ vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector< T >\
    \ >;\n#line 4 \"graph/others/maximum-independent-set.hpp\"\n\ntemplate< typename\
    \ T >\nvector< int > maximum_independent_set(const Matrix< T > &g, int trial =\
    \ 1000000) {\n\n  int N = (int) g.size();\n  vector< uint64_t > bit(N);\n\n  assert(N\
    \ <= 64);\n  for(int i = 0; i < N; i++) {\n    for(int j = 0; j < N; j++) {\n\
    \      if(i != j) {\n        assert(g[i][j] == g[j][i]);\n        if(g[i][j])\
    \ bit[i] |= uint64_t(1) << j;\n      }\n    }\n  }\n\n  vector< int > ord(N);\n\
    \  iota(begin(ord), end(ord), 0);\n  mt19937 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \  int ret = 0;\n  uint64_t ver = 0;\n  for(int i = 0; i < trial; i++) {\n   \
    \ shuffle(begin(ord), end(ord), mt);\n    uint64_t used = 0;\n    int add = 0;\n\
    \    for(int j : ord) {\n      if(used & bit[j]) continue;\n      used |= uint64_t(1)\
    \ << j;\n      ++add;\n    }\n    if(ret < add) {\n      ret = add;\n      ver\
    \ = used;\n    }\n  }\n  vector< int > ans;\n  for(int i = 0; i < N; i++) {\n\
    \    if((ver >> i) & 1) ans.emplace_back(i);\n  }\n  return ans;\n}\n#line 6 \"\
    test/verify/yosupo-maximum-independent-set.test.cpp\"\n\nint main() {\n  int N,\
    \ M;\n  cin >> N >> M;\n  Matrix < int > mat(N, vector< int >(N));\n  for(int\
    \ i = 0; i < M; i++) {\n    int a, b;\n    cin >> a >> b;\n    mat[a][b] = true;\n\
    \    mat[b][a] = true;\n  }\n  auto ret = maximum_independent_set(mat);\n  cout\
    \ << ret.size() << endl;\n  cout << ret << endl;\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/maximum_independent_set\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../graph/others/maximum-independent-set.hpp\"\
    \n\nint main() {\n  int N, M;\n  cin >> N >> M;\n  Matrix < int > mat(N, vector<\
    \ int >(N));\n  for(int i = 0; i < M; i++) {\n    int a, b;\n    cin >> a >> b;\n\
    \    mat[a][b] = true;\n    mat[b][a] = true;\n  }\n  auto ret = maximum_independent_set(mat);\n\
    \  cout << ret.size() << endl;\n  cout << ret << endl;\n}\n"
  dependsOn:
  - template/template.cpp
  - graph/others/maximum-independent-set.hpp
  - graph/template.hpp
  isVerificationFile: true
  path: test/verify/yosupo-maximum-independent-set.test.cpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-maximum-independent-set.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-maximum-independent-set.test.cpp
- /verify/test/verify/yosupo-maximum-independent-set.test.cpp.html
title: test/verify/yosupo-maximum-independent-set.test.cpp
---
