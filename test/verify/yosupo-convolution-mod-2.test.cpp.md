---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/montgomery-mod-int.cpp
    title: Montgomery ModInt
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
    PROBLEM: https://judge.yosupo.jp/problem/convolution_mod
    links:
    - https://judge.yosupo.jp/problem/convolution_mod
  bundledCode: "#line 1 \"test/verify/yosupo-convolution-mod-2.test.cpp\"\n#define\
    \ PROBLEM \"https://judge.yosupo.jp/problem/convolution_mod\"\n\n#line 1 \"template/template.cpp\"\
    \n#include<bits/stdc++.h>\n\nusing namespace std;\n\nusing int64 = long long;\n\
    const int mod = 1e9 + 7;\n\nconst int64 infll = (1LL << 62) - 1;\nconst int inf\
    \ = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup() {\n    cin.tie(nullptr);\n\
    \    ios::sync_with_stdio(false);\n    cout << fixed << setprecision(10);\n  \
    \  cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\ntemplate< typename T1,\
    \ typename T2 >\nostream &operator<<(ostream &os, const pair< T1, T2 >& p) {\n\
    \  os << p.first << \" \" << p.second;\n  return os;\n}\n\ntemplate< typename\
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
    \ : t) fill_v(e, v);\n}\n\ntemplate< typename F >\nstruct FixPoint : F {\n  explicit\
    \ FixPoint(F &&f) : F(forward< F >(f)) {}\n\n  template< typename... Args >\n\
    \  decltype(auto) operator()(Args &&... args) const {\n    return F::operator()(*this,\
    \ forward< Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-convolution-mod-2.test.cpp\"\
    \n\n#line 1 \"math/combinatorics/montgomery-mod-int.cpp\"\n/**\n * @brief Montgomery\
    \ ModInt\n */\ntemplate< uint32_t mod, bool fast = false >\nstruct MontgomeryModInt\
    \ {\n  using mint = MontgomeryModInt;\n  using i32 = int32_t;\n  using i64 = int64_t;\n\
    \  using u32 = uint32_t;\n  using u64 = uint64_t;\n\n  static constexpr u32 get_r()\
    \ {\n    u32 ret = mod;\n    for(i32 i = 0; i < 4; i++) ret *= 2 - mod * ret;\n\
    \    return ret;\n  }\n\n  static constexpr u32 r = get_r();\n  static constexpr\
    \ u32 n2 = -u64(mod) % mod;\n\n  static_assert(r * mod == 1, \"invalid, r * mod\
    \ != 1\");\n  static_assert(mod < (1 << 30), \"invalid, mod >= 2 ^ 30\");\n  static_assert((mod\
    \ & 1) == 1, \"invalid, mod % 2 == 0\");\n\n  u32 x;\n\n  MontgomeryModInt() :\
    \ x{} {}\n\n  MontgomeryModInt(const i64 &a)\n      : x(reduce(u64(fast ? a :\
    \ (a % mod + mod)) * n2)) {}\n\n  static constexpr u32 reduce(const u64 &b) {\n\
    \    return u32(b >> 32) + mod - u32((u64(u32(b) * r) * mod) >> 32);\n  }\n\n\
    \  mint &operator+=(const mint &p) {\n    if(i32(x += p.x - 2 * mod) < 0) x +=\
    \ 2 * mod;\n    return *this;\n  }\n\n  mint &operator-=(const mint &p) {\n  \
    \  if(i32(x -= p.x) < 0) x += 2 * mod;\n    return *this;\n  }\n\n  mint &operator*=(const\
    \ mint &p) {\n    x = reduce(u64(x) * p.x);\n    return *this;\n  }\n\n  mint\
    \ &operator/=(const mint &p) {\n    *this *= p.inverse();\n    return *this;\n\
    \  }\n\n  mint operator-() const { return mint() - *this; }\n\n  mint operator+(const\
    \ mint &p) const { return mint(*this) += p; }\n\n  mint operator-(const mint &p)\
    \ const { return mint(*this) -= p; }\n\n  mint operator*(const mint &p) const\
    \ { return mint(*this) *= p; }\n\n  mint operator/(const mint &p) const { return\
    \ mint(*this) /= p; }\n\n  bool operator==(const mint &p) const { return (x >=\
    \ mod ? x - mod : x) == (p.x >= mod ? p.x - mod : p.x); }\n\n  bool operator!=(const\
    \ mint &p) const { return (x >= mod ? x - mod : x) != (p.x >= mod ? p.x - mod\
    \ : p.x); }\n\n  u32 get() const {\n    u32 ret = reduce(x);\n    return ret >=\
    \ mod ? ret - mod : ret;\n  }\n\n  mint pow(u64 n) const {\n    mint ret(1), mul(*this);\n\
    \    while(n > 0) {\n      if(n & 1) ret *= mul;\n      mul *= mul;\n      n >>=\
    \ 1;\n    }\n    return ret;\n  }\n\n  mint inverse() const {\n    return pow(mod\
    \ - 2);\n  }\n\n  friend ostream &operator<<(ostream &os, const mint &p) {\n \
    \   return os << p.get();\n  }\n\n  friend istream &operator>>(istream &is, mint\
    \ &a) {\n    i64 t;\n    is >> t;\n    a = mint(t);\n    return is;\n  }\n\n \
    \ static u32 get_mod() { return mod; }\n};\n\nusing modint = MontgomeryModInt<\
    \ mod >;\n#line 1 \"math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\
    \n/**\n * @brief Number Theoretic Transform Friendly Mod Int\n */\ntemplate< typename\
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
    \ Mint >::root = Mint();\n#line 7 \"test/verify/yosupo-convolution-mod-2.test.cpp\"\
    \n\nconst int MOD = 998244353;\nusing mint = MontgomeryModInt< MOD, true >;\n\n\
    int main() {\n  int N, M;\n  cin >> N >> M;\n  vector< mint > A(N), B(M);\n  for(auto\
    \ &a : A) cin >> a;\n  for(auto &b : B) cin >> b;\n  NumberTheoreticTransformFriendlyModInt<\
    \ mint > ntt;\n  for(auto &c : ntt.multiply(A, B)) cout << c << \" \";\n  cout\
    \ << endl;\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/convolution_mod\"\n\n#include\
    \ \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/montgomery-mod-int.cpp\"\
    \n#include \"../../math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\n\
    \nconst int MOD = 998244353;\nusing mint = MontgomeryModInt< MOD, true >;\n\n\
    int main() {\n  int N, M;\n  cin >> N >> M;\n  vector< mint > A(N), B(M);\n  for(auto\
    \ &a : A) cin >> a;\n  for(auto &b : B) cin >> b;\n  NumberTheoreticTransformFriendlyModInt<\
    \ mint > ntt;\n  for(auto &c : ntt.multiply(A, B)) cout << c << \" \";\n  cout\
    \ << endl;\n}\n"
  dependsOn:
  - template/template.cpp
  - math/combinatorics/montgomery-mod-int.cpp
  - math/fft/number-theoretic-transform-friendly-mod-int.cpp
  isVerificationFile: true
  path: test/verify/yosupo-convolution-mod-2.test.cpp
  requiredBy: []
  timestamp: '2021-08-09 21:02:39+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-convolution-mod-2.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-convolution-mod-2.test.cpp
- /verify/test/verify/yosupo-convolution-mod-2.test.cpp.html
title: test/verify/yosupo-convolution-mod-2.test.cpp
---
