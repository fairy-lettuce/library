---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/lagrange-polynomial-3.cpp
    title: "Lagrange Polynomial(\u591A\u9805\u5F0F\u88DC\u9593, \u5024)"
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-int.cpp
    title: math/combinatorics/mod-int.cpp
  - icon: ':heavy_check_mark:'
    path: math/fft/number-theoretic-transform-friendly-mod-int.cpp
    title: Number Theoretic Transform Friendly Mod Int
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
    PROBLEM: https://judge.yosupo.jp/problem/shift_of_sampling_points_of_polynomial
    links:
    - https://judge.yosupo.jp/problem/shift_of_sampling_points_of_polynomial
  bundledCode: "#line 1 \"test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp\"\
    \n#define PROBLEM \"https://judge.yosupo.jp/problem/shift_of_sampling_points_of_polynomial\"\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp\"\
    \n\n#line 1 \"math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\n/**\n\
    \ * @brief Number Theoretic Transform Friendly Mod Int\n */\ntemplate< typename\
    \ Mint >\nstruct NumberTheoreticTransformFriendlyModInt {\n\n  static vector<\
    \ Mint > dw, idw;\n  static int max_base;\n  static Mint root;\n\n  NumberTheoreticTransformFriendlyModInt()\
    \ = default;\n\n  static void init() {\n    if(dw.empty()) {\n      const unsigned\
    \ mod = Mint::get_mod();\n      assert(mod >= 3 && mod % 2 == 1);\n      auto\
    \ tmp = mod - 1;\n      max_base = 0;\n      while(tmp % 2 == 0) tmp >>= 1, max_base++;\n\
    \      root = 2;\n      while(root.pow((mod - 1) >> 1) == 1) root += 1;\n    \
    \  assert(root.pow(mod - 1) == 1);\n      dw.resize(max_base);\n      idw.resize(max_base);\n\
    \      for(int i = 0; i < max_base; i++) {\n        dw[i] = -root.pow((mod - 1)\
    \ >> (i + 2));\n        idw[i] = Mint(1) / dw[i];\n      }\n    }\n  }\n\n  static\
    \ void ntt(vector< Mint > &a) {\n    init();\n    const int n = (int) a.size();\n\
    \    assert((n & (n - 1)) == 0);\n    assert(__builtin_ctz(n) <= max_base);\n\
    \    for(int m = n; m >>= 1;) {\n      Mint w = 1;\n      for(int s = 0, k = 0;\
    \ s < n; s += 2 * m) {\n        for(int i = s, j = s + m; i < s + m; ++i, ++j)\
    \ {\n          auto x = a[i], y = a[j] * w;\n          a[i] = x + y, a[j] = x\
    \ - y;\n        }\n        w *= dw[__builtin_ctz(++k)];\n      }\n    }\n  }\n\
    \n  static void intt(vector< Mint > &a, bool f = true) {\n    init();\n    const\
    \ int n = (int) a.size();\n    assert((n & (n - 1)) == 0);\n    assert(__builtin_ctz(n)\
    \ <= max_base);\n    for(int m = 1; m < n; m *= 2) {\n      Mint w = 1;\n    \
    \  for(int s = 0, k = 0; s < n; s += 2 * m) {\n        for(int i = s, j = s +\
    \ m; i < s + m; ++i, ++j) {\n          auto x = a[i], y = a[j];\n          a[i]\
    \ = x + y, a[j] = (x - y) * w;\n        }\n        w *= idw[__builtin_ctz(++k)];\n\
    \      }\n    }\n    if(f) {\n      Mint inv_sz = Mint(1) / n;\n      for(int\
    \ i = 0; i < n; i++) a[i] *= inv_sz;\n    }\n  }\n\n  static vector< Mint > multiply(vector<\
    \ Mint > a, vector< Mint > b) {\n    int need = a.size() + b.size() - 1;\n   \
    \ int nbase = 1;\n    while((1 << nbase) < need) nbase++;\n    int sz = 1 << nbase;\n\
    \    a.resize(sz, 0);\n    b.resize(sz, 0);\n    ntt(a);\n    ntt(b);\n    Mint\
    \ inv_sz = Mint(1) / sz;\n    for(int i = 0; i < sz; i++) a[i] *= b[i] * inv_sz;\n\
    \    intt(a, false);\n    a.resize(need);\n    return a;\n  }\n};\n\ntemplate<\
    \ typename Mint >\nvector< Mint > NumberTheoreticTransformFriendlyModInt< Mint\
    \ >::dw = vector< Mint >();\ntemplate< typename Mint >\nvector< Mint > NumberTheoreticTransformFriendlyModInt<\
    \ Mint >::idw = vector< Mint >();\ntemplate< typename Mint >\nint NumberTheoreticTransformFriendlyModInt<\
    \ Mint >::max_base = 0;\ntemplate< typename Mint >\nMint NumberTheoreticTransformFriendlyModInt<\
    \ Mint >::root = Mint();\n#line 6 \"test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp\"\
    \n\n#line 1 \"math/combinatorics/lagrange-polynomial-3.cpp\"\n/**\n * @brief Lagrange\
    \ Polynomial(\u591A\u9805\u5F0F\u88DC\u9593, \u5024)\n */\ntemplate< typename\
    \ Mint, typename F >\nvector< Mint > lagrange_polynomial(const vector< Mint >\
    \ &y, int64_t T, const int &m, const F &multiply) {\n  int k = (int) y.size()\
    \ - 1;\n  T %= Mint::get_mod();\n  if(T <= k) {\n    vector< Mint > ret(m);\n\
    \    int ptr = 0;\n    for(int64_t i = T; i <= k and ptr < m; i++) {\n      ret[ptr++]\
    \ = y[i];\n    }\n    if(k + 1 < T + m) {\n      auto suf = lagrange_polynomial(y,\
    \ k + 1, m - ptr, multiply);\n      for(int i = k + 1; i < T + m; i++) {\n   \
    \     ret[ptr++] = suf[i - (k + 1)];\n      }\n    }\n    return ret;\n  }\n \
    \ if(T + m > Mint::get_mod()) {\n    auto pref = lagrange_polynomial(y, T, Mint::get_mod()\
    \ - T, multiply);\n    auto suf = lagrange_polynomial(y, 0, m - pref.size(), multiply);\n\
    \    copy(begin(suf), end(suf), back_inserter(pref));\n    return pref;\n  }\n\
    \  \n  vector< Mint > finv(k + 1, 1), d(k + 1);\n  for(int i = 2; i <= k; i++)\
    \ finv[k] *= i;\n  finv[k] = Mint(1) / finv[k];\n  for(int i = k; i >= 1; i--)\
    \ finv[i - 1] = finv[i] * i;\n  for(int i = 0; i <= k; i++) {\n    d[i] = finv[i]\
    \ * finv[k - i] * y[i];\n    if((k - i) & 1) d[i] = -d[i];\n  }\n\n  vector< Mint\
    \ > h(m + k);\n  for(int i = 0; i < m + k; i++) {\n    h[i] = Mint(1) / (T - k\
    \ + i);\n  }\n\n  auto dh = multiply(d, h);\n\n  vector< Mint > ret(m);\n  Mint\
    \ cur = T;\n  for(int i = 1; i <= k; i++) cur *= T - i;\n  for(int i = 0; i <\
    \ m; i++) {\n    ret[i] = cur * dh[k + i];\n    cur *= T + i + 1;\n    cur *=\
    \ h[i];\n  }\n  return ret;\n}\n#line 8 \"test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp\"\
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
    \ { return mod; }\n};\n\nusing modint = ModInt< mod >;\n#line 10 \"test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp\"\
    \n\nusing mint = ModInt< 998244353 >;\n\nint main() {\n  int N, T, M;\n  cin >>\
    \ N >> T >> M;\n  vector< mint > ys(N);\n  for(int i = 0; i < N; i++) cin >> ys[i];\n\
    \  NumberTheoreticTransformFriendlyModInt< mint > v;\n  auto multiply = [&](const\
    \ vector< mint > &a, const vector< mint > &b) { return v.multiply(a, b); };\n\
    \  cout << lagrange_polynomial(ys, M, T, multiply) << \"\\n\";\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/shift_of_sampling_points_of_polynomial\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\
    \n\n#include \"../../math/combinatorics/lagrange-polynomial-3.cpp\"\n\n#include\
    \ \"../../math/combinatorics/mod-int.cpp\"\n\nusing mint = ModInt< 998244353 >;\n\
    \nint main() {\n  int N, T, M;\n  cin >> N >> T >> M;\n  vector< mint > ys(N);\n\
    \  for(int i = 0; i < N; i++) cin >> ys[i];\n  NumberTheoreticTransformFriendlyModInt<\
    \ mint > v;\n  auto multiply = [&](const vector< mint > &a, const vector< mint\
    \ > &b) { return v.multiply(a, b); };\n  cout << lagrange_polynomial(ys, M, T,\
    \ multiply) << \"\\n\";\n}\n"
  dependsOn:
  - template/template.cpp
  - math/fft/number-theoretic-transform-friendly-mod-int.cpp
  - math/combinatorics/lagrange-polynomial-3.cpp
  - math/combinatorics/mod-int.cpp
  isVerificationFile: true
  path: test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp
  requiredBy: []
  timestamp: '2021-08-02 23:29:30+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp
- /verify/test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp.html
title: test/verify/yosupo-shift-of-sampling-points-of-polynomial.test.cpp
---
