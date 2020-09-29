---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-pow.cpp
    title: math/combinatorics/mod-pow.cpp
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-tetration.cpp
    title: Mod-Tetration
  - icon: ':heavy_check_mark:'
    path: math/number-theory/euler-phi.cpp
    title: "Euler's-Phi-Function(\u30AA\u30A4\u30E9\u30FC\u306E\u03C6\u95A2\u6570)"
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/tetration_mod
    links:
    - https://judge.yosupo.jp/problem/tetration_mod
  bundledCode: "#line 1 \"test/verify/yosupo-tetration-mod.test.cpp\"\n#define PROBLEM\
    \ \"https://judge.yosupo.jp/problem/tetration_mod\"\n\n#line 1 \"template/template.cpp\"\
    \n#include<bits/stdc++.h>\n\nusing namespace std;\n\nusing int64 = long long;\n\
    const int mod = 1e9 + 7;\n\nconst int64 infll = (1LL << 62) - 1;\nconst int inf\
    \ = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup() {\n    cin.tie(nullptr);\n\
    \    ios::sync_with_stdio(false);\n    cout << fixed << setprecision(10);\n  \
    \  cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\n\ntemplate< typename\
    \ T1, typename T2 >\nostream &operator<<(ostream &os, const pair< T1, T2 >& p)\
    \ {\n  os << p.first << \" \" << p.second;\n  return os;\n}\n\ntemplate< typename\
    \ T1, typename T2 >\nistream &operator>>(istream &is, pair< T1, T2 > &p) {\n \
    \ is >> p.first >> p.second;\n  return is;\n}\n\ntemplate< typename T >\nostream\
    \ &operator<<(ostream &os, const vector< T > &v) {\n  for(int i = 0; i < (int)\
    \ v.size(); i++) {\n    os << v[i] << (i + 1 != v.size() ? \" \" : \"\");\n  }\n\
    \  return os;\n}\n\ntemplate< typename T >\nistream &operator>>(istream &is, vector<\
    \ T > &v) {\n  for(T &in : v) is >> in;\n  return is;\n}\n\ntemplate< typename\
    \ T1, typename T2 >\ninline bool chmax(T1 &a, T2 b) { return a < b && (a = b,\
    \ true); }\n\ntemplate< typename T1, typename T2 >\ninline bool chmin(T1 &a, T2\
    \ b) { return a > b && (a = b, true); }\n\ntemplate< typename T = int64 >\nvector<\
    \ T > make_v(size_t a) {\n  return vector< T >(a);\n}\n\ntemplate< typename T,\
    \ typename... Ts >\nauto make_v(size_t a, Ts... ts) {\n  return vector< decltype(make_v<\
    \ T >(ts...)) >(a, make_v< T >(ts...));\n}\n\ntemplate< typename T, typename V\
    \ >\ntypename enable_if< is_class< T >::value == 0 >::type fill_v(T &t, const\
    \ V &v) {\n  t = v;\n}\n\ntemplate< typename T, typename V >\ntypename enable_if<\
    \ is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {\n  for(auto &e\
    \ : t) fill_v(e, v);\n}\n\ntemplate< typename F >\nstruct FixPoint : F {\n  FixPoint(F\
    \ &&f) : F(forward< F >(f)) {}\n \n  template< typename... Args >\n  decltype(auto)\
    \ operator()(Args &&... args) const {\n    return F::operator()(*this, forward<\
    \ Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-tetration-mod.test.cpp\"\
    \n\n#line 1 \"math/combinatorics/mod-pow.cpp\"\ntemplate< typename T >\nT mod_pow(T\
    \ x, T n, const T &p) {\n  T ret = 1;\n  while(n > 0) {\n    if(n & 1) (ret *=\
    \ x) %= p;\n    (x *= x) %= p;\n    n >>= 1;\n  }\n  return ret;\n}\n\n#line 1\
    \ \"math/number-theory/euler-phi.cpp\"\n/**\n * @brief Euler's-Phi-Function(\u30AA\
    \u30A4\u30E9\u30FC\u306E\u03C6\u95A2\u6570)\n * @docs docs/euler-phi.md\n */\n\
    template< typename T >\nT euler_phi(T n) {\n  T ret = n;\n  for(T i = 2; i * i\
    \ <= n; i++) {\n    if(n % i == 0) {\n      ret -= ret / i;\n      while(n % i\
    \ == 0) n /= i;\n    }\n  }\n  if(n > 1) ret -= ret / n;\n  return ret;\n}\n#line\
    \ 7 \"test/verify/yosupo-tetration-mod.test.cpp\"\n\n#line 1 \"math/combinatorics/mod-tetration.cpp\"\
    \n/**\n * @brief Mod-Tetration\n */\ntemplate< typename T >\nT mod_tetration(const\
    \ T &a, const T &b, const T &m) {\n  if(m == 1) return 0;\n  if(a == 0) return\
    \ !(b & 1);\n  if(b == 0) return 1;\n  if(b == 1) return a % m;\n  if(b == 2)\
    \ return mod_pow(a % m, a, m);\n  auto phi = euler_phi(m);\n  return mod_pow(a\
    \ % m, mod_tetration(a, b - 1, phi) + phi, m);\n}\n#line 9 \"test/verify/yosupo-tetration-mod.test.cpp\"\
    \n\nint main() {\n  int T;\n  cin >> T;\n  while(T--) {\n    int a, b, m;\n  \
    \  cin >> a >> b >> m;\n    cout << mod_tetration< int64_t >(a, b, m) % m << \"\
    \\n\";\n  }\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/tetration_mod\"\n\n#include\
    \ \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/mod-pow.cpp\"\
    \n#include \"../../math/number-theory/euler-phi.cpp\"\n\n#include \"../../math/combinatorics/mod-tetration.cpp\"\
    \n\nint main() {\n  int T;\n  cin >> T;\n  while(T--) {\n    int a, b, m;\n  \
    \  cin >> a >> b >> m;\n    cout << mod_tetration< int64_t >(a, b, m) % m << \"\
    \\n\";\n  }\n}\n"
  dependsOn:
  - template/template.cpp
  - math/combinatorics/mod-pow.cpp
  - math/number-theory/euler-phi.cpp
  - math/combinatorics/mod-tetration.cpp
  isVerificationFile: true
  path: test/verify/yosupo-tetration-mod.test.cpp
  requiredBy: []
  timestamp: '2020-03-03 18:28:13+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-tetration-mod.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-tetration-mod.test.cpp
- /verify/test/verify/yosupo-tetration-mod.test.cpp.html
title: test/verify/yosupo-tetration-mod.test.cpp
---
