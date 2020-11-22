---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/combination.cpp
    title: math/combinatorics/combination.cpp
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-int.cpp
    title: math/combinatorics/mod-int.cpp
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/stirling-number-second.cpp
    title: math/combinatorics/stirling-number-second.cpp
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I
  bundledCode: "#line 1 \"test/verify/aoj-dpl-5-i.test.cpp\"\n#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I\"\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/aoj-dpl-5-i.test.cpp\"\
    \n\n#line 1 \"math/combinatorics/mod-int.cpp\"\ntemplate< int mod >\nstruct ModInt\
    \ {\n  int x;\n\n  ModInt() : x(0) {}\n\n  ModInt(int64_t y) : x(y >= 0 ? y %\
    \ mod : (mod - (-y) % mod) % mod) {}\n\n  ModInt &operator+=(const ModInt &p)\
    \ {\n    if((x += p.x) >= mod) x -= mod;\n    return *this;\n  }\n\n  ModInt &operator-=(const\
    \ ModInt &p) {\n    if((x += mod - p.x) >= mod) x -= mod;\n    return *this;\n\
    \  }\n\n  ModInt &operator*=(const ModInt &p) {\n    x = (int) (1LL * x * p.x\
    \ % mod);\n    return *this;\n  }\n\n  ModInt &operator/=(const ModInt &p) {\n\
    \    *this *= p.inverse();\n    return *this;\n  }\n\n  ModInt operator-() const\
    \ { return ModInt(-x); }\n\n  ModInt operator+(const ModInt &p) const { return\
    \ ModInt(*this) += p; }\n\n  ModInt operator-(const ModInt &p) const { return\
    \ ModInt(*this) -= p; }\n\n  ModInt operator*(const ModInt &p) const { return\
    \ ModInt(*this) *= p; }\n\n  ModInt operator/(const ModInt &p) const { return\
    \ ModInt(*this) /= p; }\n\n  bool operator==(const ModInt &p) const { return x\
    \ == p.x; }\n\n  bool operator!=(const ModInt &p) const { return x != p.x; }\n\
    \n  ModInt inverse() const {\n    int a = x, b = mod, u = 1, v = 0, t;\n    while(b\
    \ > 0) {\n      t = a / b;\n      swap(a -= t * b, b);\n      swap(u -= t * v,\
    \ v);\n    }\n    return ModInt(u);\n  }\n\n  ModInt pow(int64_t n) const {\n\
    \    ModInt ret(1), mul(x);\n    while(n > 0) {\n      if(n & 1) ret *= mul;\n\
    \      mul *= mul;\n      n >>= 1;\n    }\n    return ret;\n  }\n\n  friend ostream\
    \ &operator<<(ostream &os, const ModInt &p) {\n    return os << p.x;\n  }\n\n\
    \  friend istream &operator>>(istream &is, ModInt &a) {\n    int64_t t;\n    is\
    \ >> t;\n    a = ModInt< mod >(t);\n    return (is);\n  }\n\n  static int get_mod()\
    \ { return mod; }\n};\n\nusing modint = ModInt< mod >;\n#line 1 \"math/combinatorics/combination.cpp\"\
    \ntemplate< typename T >\nstruct Combination {\n  vector< T > _fact, _rfact, _inv;\n\
    \n  Combination(int sz) : _fact(sz + 1), _rfact(sz + 1), _inv(sz + 1) {\n    _fact[0]\
    \ = _rfact[sz] = _inv[0] = 1;\n    for(int i = 1; i <= sz; i++) _fact[i] = _fact[i\
    \ - 1] * i;\n    _rfact[sz] /= _fact[sz];\n    for(int i = sz - 1; i >= 0; i--)\
    \ _rfact[i] = _rfact[i + 1] * (i + 1);\n    for(int i = 1; i <= sz; i++) _inv[i]\
    \ = _rfact[i] * _fact[i - 1];\n  }\n\n  inline T fact(int k) const { return _fact[k];\
    \ }\n\n  inline T rfact(int k) const { return _rfact[k]; }\n\n  inline T inv(int\
    \ k) const { return _inv[k]; }\n\n  T P(int n, int r) const {\n    if(r < 0 ||\
    \ n < r) return 0;\n    return fact(n) * rfact(n - r);\n  }\n\n  T C(int p, int\
    \ q) const {\n    if(q < 0 || p < q) return 0;\n    return fact(p) * rfact(q)\
    \ * rfact(p - q);\n  }\n\n  T H(int n, int r) const {\n    if(n < 0 || r < 0)\
    \ return (0);\n    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n#line 7 \"test/verify/aoj-dpl-5-i.test.cpp\"\
    \n\n#line 1 \"math/combinatorics/stirling-number-second.cpp\"\ntemplate< typename\
    \ T >\nT stirling_number_second(int n, int k) {\n  Combination< T > table(k);\n\
    \  T ret = 0;\n  for(int i = 0; i <= k; i++) {\n    auto add = T(i).pow(n) * table.C(k,\
    \ i);\n    if((k - i) & 1) ret -= add;\n    else ret += add;\n  }\n  return ret\
    \ * table.rfact(k);\n}\n\n#line 9 \"test/verify/aoj-dpl-5-i.test.cpp\"\n\nint\
    \ main() {\n  int N, K;\n  cin >> N >> K;\n  cout << stirling_number_second< modint\
    \ >(N, K) << endl;\n}\n\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DPL_5_I\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/mod-int.cpp\"\
    \n#include \"../../math/combinatorics/combination.cpp\"\n\n#include \"../../math/combinatorics/stirling-number-second.cpp\"\
    \n\nint main() {\n  int N, K;\n  cin >> N >> K;\n  cout << stirling_number_second<\
    \ modint >(N, K) << endl;\n}\n\n"
  dependsOn:
  - template/template.cpp
  - math/combinatorics/mod-int.cpp
  - math/combinatorics/combination.cpp
  - math/combinatorics/stirling-number-second.cpp
  isVerificationFile: true
  path: test/verify/aoj-dpl-5-i.test.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-dpl-5-i.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-dpl-5-i.test.cpp
- /verify/test/verify/aoj-dpl-5-i.test.cpp.html
title: test/verify/aoj-dpl-5-i.test.cpp
---
