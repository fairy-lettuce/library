---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-int.cpp
    title: math/combinatorics/mod-int.cpp
  - icon: ':heavy_check_mark:'
    path: math/fft/number-theoretic-transform-friendly-mod-int.cpp
    title: Number-Theoretic-Transform-Friendly-Mod-Int
  - icon: ':heavy_check_mark:'
    path: math/fps/formal-power-series.cpp
    title: "Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\u7D1A\u6570)"
  - icon: ':heavy_check_mark:'
    path: math/fps/inv.cpp
    title: Inv ($\frac {1} {f(x)}$)
  - icon: ':heavy_check_mark:'
    path: math/fps/partition.cpp
    title: math/fps/partition.cpp
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
    PROBLEM: https://judge.yosupo.jp/problem/partition_function
    links:
    - https://judge.yosupo.jp/problem/partition_function
  bundledCode: "#line 1 \"test/verify/yosupo-partition-function.test.cpp\"\n#define\
    \ PROBLEM \"https://judge.yosupo.jp/problem/partition_function\"\n\n#line 1 \"\
    template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace std;\n\nusing\
    \ int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll = (1LL <<\
    \ 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup() {\n\
    \    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed <<\
    \ setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-partition-function.test.cpp\"\
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
    \ { return mod; }\n};\n\nusing modint = ModInt< mod >;\n#line 1 \"math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\
    \n/**\n * @brief Number-Theoretic-Transform-Friendly-Mod-Int\n */\ntemplate< typename\
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
    \ Mint >::root = Mint();\n#line 7 \"test/verify/yosupo-partition-function.test.cpp\"\
    \n\n#line 2 \"math/fps/formal-power-series.cpp\"\n\n/**\n * @brief Formal-Power-Series(\u5F62\
    \u5F0F\u7684\u51AA\u7D1A\u6570)\n */\ntemplate< typename T >\nstruct FormalPowerSeries\
    \ : vector< T > {\n  using vector< T >::vector;\n  using P = FormalPowerSeries;\n\
    \n  using MULT = function< vector< T >(P, P) >;\n  using FFT = function< void(P\
    \ &) >;\n  using SQRT = function< T(T) >;\n\n  static MULT &get_mult() {\n   \
    \ static MULT mult = nullptr;\n    return mult;\n  }\n\n  static void set_mult(MULT\
    \ f) {\n    get_mult() = f;\n  }\n\n  static FFT &get_fft() {\n    static FFT\
    \ fft = nullptr;\n    return fft;\n  }\n\n  static FFT &get_ifft() {\n    static\
    \ FFT ifft = nullptr;\n    return ifft;\n  }\n\n  static void set_fft(FFT f, FFT\
    \ g) {\n    get_fft() = f;\n    get_ifft() = g;\n    if(get_mult() == nullptr)\
    \ {\n      auto mult = [&](P a, P b) {\n        int need = a.size() + b.size()\
    \ - 1;\n        int nbase = 1;\n        while((1 << nbase) < need) nbase++;\n\
    \        int sz = 1 << nbase;\n        a.resize(sz, T(0));\n        b.resize(sz,\
    \ T(0));\n        get_fft()(a);\n        get_fft()(b);\n        for(int i = 0;\
    \ i < sz; i++) a[i] *= b[i];\n        get_ifft()(a);\n        a.resize(need);\n\
    \        return a;\n      };\n      set_mult(mult);\n    }\n  }\n\n  static SQRT\
    \ &get_sqrt() {\n    static SQRT sqr = nullptr;\n    return sqr;\n  }\n\n  static\
    \ void set_sqrt(SQRT sqr) {\n    get_sqrt() = sqr;\n  }\n\n  void shrink() {\n\
    \    while(this->size() && this->back() == T(0)) this->pop_back();\n  }\n\n  P\
    \ operator+(const P &r) const { return P(*this) += r; }\n\n  P operator+(const\
    \ T &v) const { return P(*this) += v; }\n\n  P operator-(const P &r) const { return\
    \ P(*this) -= r; }\n\n  P operator-(const T &v) const { return P(*this) -= v;\
    \ }\n\n  P operator*(const P &r) const { return P(*this) *= r; }\n\n  P operator*(const\
    \ T &v) const { return P(*this) *= v; }\n\n  P operator/(const P &r) const { return\
    \ P(*this) /= r; }\n\n  P operator%(const P &r) const { return P(*this) %= r;\
    \ }\n\n  P &operator+=(const P &r) {\n    if(r.size() > this->size()) this->resize(r.size());\n\
    \    for(int i = 0; i < r.size(); i++) (*this)[i] += r[i];\n    return *this;\n\
    \  }\n\n  P &operator+=(const T &r) {\n    if(this->empty()) this->resize(1);\n\
    \    (*this)[0] += r;\n    return *this;\n  }\n\n  P &operator-=(const P &r) {\n\
    \    if(r.size() > this->size()) this->resize(r.size());\n    for(int i = 0; i\
    \ < r.size(); i++) (*this)[i] -= r[i];\n    shrink();\n    return *this;\n  }\n\
    \n  P &operator-=(const T &r) {\n    if(this->empty()) this->resize(1);\n    (*this)[0]\
    \ -= r;\n    shrink();\n    return *this;\n  }\n\n  P &operator*=(const T &v)\
    \ {\n    const int n = (int) this->size();\n    for(int k = 0; k < n; k++) (*this)[k]\
    \ *= v;\n    return *this;\n  }\n\n  P &operator*=(const P &r) {\n    if(this->empty()\
    \ || r.empty()) {\n      this->clear();\n      return *this;\n    }\n    assert(get_mult()\
    \ != nullptr);\n    auto ret = get_mult()(*this, r);\n    return *this = P(begin(ret),\
    \ end(ret));\n  }\n\n  P &operator%=(const P &r) {\n    return *this -= *this\
    \ / r * r;\n  }\n\n  P operator-() const {\n    P ret(this->size());\n    for(int\
    \ i = 0; i < this->size(); i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n\
    \  P &operator/=(const P &r) {\n    if(this->size() < r.size()) {\n      this->clear();\n\
    \      return *this;\n    }\n    int n = this->size() - r.size() + 1;\n    return\
    \ *this = (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n  }\n\n  P dot(P r)\
    \ const {\n    P ret(min(this->size(), r.size()));\n    for(int i = 0; i < ret.size();\
    \ i++) ret[i] = (*this)[i] * r[i];\n    return ret;\n  }\n\n  P pre(int sz) const\
    \ {\n    return P(begin(*this), begin(*this) + min((int) this->size(), sz));\n\
    \  }\n\n  P operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n\
    \    P ret(*this);\n    ret.erase(ret.begin(), ret.begin() + sz);\n    return\
    \ ret;\n  }\n\n  P operator<<(int sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(),\
    \ sz, T(0));\n    return ret;\n  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n\
    \    if(deg != -1) ret.resize(deg, T(0));\n    reverse(begin(ret), end(ret));\n\
    \    return ret;\n  }\n\n  T operator()(T x) const {\n    T r = 0, w = 1;\n  \
    \  for(auto &v : *this) {\n      r += w * v;\n      w *= x;\n    }\n    return\
    \ r;\n  }\n\n  P diff() const;\n\n  P integral() const;\n\n  // F(0) must not\
    \ be 0\n  P inv_fast() const;\n\n  P inv(int deg = -1) const;\n\n  // F(0) must\
    \ be 1\n  P log(int deg = -1) const;\n\n  P sqrt(int deg = -1) const;\n\n  //\
    \ F(0) must be 0\n  P exp_fast(int deg = -1) const;\n\n  P exp(int deg = -1) const;\n\
    \n  P pow(int64_t k, int deg = -1) const;\n\n  P mod_pow(int64_t k, P g) const;\n\
    \n  P taylor_shift(T c) const;\n};\n#line 3 \"math/fps/inv.cpp\"\n\n/**\n * @brief\
    \ Inv ($\\frac {1} {f(x)}$)\n */\ntemplate< typename T >\ntypename FormalPowerSeries<\
    \ T >::P FormalPowerSeries< T >::inv_fast() const {\n  assert(((*this)[0]) !=\
    \ T(0));\n\n  const int n = (int) this->size();\n  P res{T(1) / (*this)[0]};\n\
    \n  for(int d = 1; d < n; d <<= 1) {\n    P f(2 * d), g(2 * d);\n    for(int j\
    \ = 0; j < min(n, 2 * d); j++) f[j] = (*this)[j];\n    for(int j = 0; j < d; j++)\
    \ g[j] = res[j];\n    get_fft()(f);\n    get_fft()(g);\n    for(int j = 0; j <\
    \ 2 * d; j++) f[j] *= g[j];\n    get_ifft()(f);\n    for(int j = 0; j < d; j++)\
    \ {\n      f[j] = 0;\n      f[j + d] = -f[j + d];\n    }\n    get_fft()(f);\n\
    \    for(int j = 0; j < 2 * d; j++) f[j] *= g[j];\n    get_ifft()(f);\n    for(int\
    \ j = 0; j < d; j++) f[j] = res[j];\n    res = f;\n  }\n  return res.pre(n);\n\
    }\n\ntemplate< typename T >\ntypename FormalPowerSeries< T >::P FormalPowerSeries<\
    \ T >::inv(int deg) const {\n  assert(((*this)[0]) != T(0));\n  const int n =\
    \ (int) this->size();\n  if(deg == -1) deg = n;\n  if(get_fft() != nullptr) {\n\
    \    P ret(*this);\n    ret.resize(deg, T(0));\n    return ret.inv_fast();\n \
    \ }\n  P ret({T(1) / (*this)[0]});\n  for(int i = 1; i < deg; i <<= 1) {\n   \
    \ ret = (ret + ret - ret * ret * pre(i << 1)).pre(i << 1);\n  }\n  return ret.pre(deg);\n\
    }\n#line 4 \"math/fps/partition.cpp\"\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > partition(int N) {\n  FormalPowerSeries< T > poly(N + 1);\n  poly[0] = 1;\n\
    \  for(int k = 1; k <= N; k++) {\n    if(1LL * k * (3 * k + 1) / 2 <= N) poly[k\
    \ * (3 * k + 1) / 2] += (k % 2 ? -1 : 1);\n    if(1LL * k * (3 * k - 1) / 2 <=\
    \ N) poly[k * (3 * k - 1) / 2] += (k % 2 ? -1 : 1);\n  }\n  return poly.inv();\n\
    }\n#line 9 \"test/verify/yosupo-partition-function.test.cpp\"\n\nconst int MOD\
    \ = 998244353;\nusing mint = ModInt< MOD >;\n\nint main() {\n  NumberTheoreticTransformFriendlyModInt<\
    \ mint > ntt;\n  using FPS = FormalPowerSeries< mint >;\n  FPS::set_fft([&](FPS\
    \ &a) { ntt.ntt(a); }, [&](FPS &a) { ntt.intt(a); });\n\n  int N;\n  cin >> N;\n\
    \  cout << partition< mint >(N) << endl;\n}\n\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/partition_function\"\n\n\
    #include \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/mod-int.cpp\"\
    \n#include \"../../math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\n\
    \n#include \"../../math/fps/partition.cpp\"\n\nconst int MOD = 998244353;\nusing\
    \ mint = ModInt< MOD >;\n\nint main() {\n  NumberTheoreticTransformFriendlyModInt<\
    \ mint > ntt;\n  using FPS = FormalPowerSeries< mint >;\n  FPS::set_fft([&](FPS\
    \ &a) { ntt.ntt(a); }, [&](FPS &a) { ntt.intt(a); });\n\n  int N;\n  cin >> N;\n\
    \  cout << partition< mint >(N) << endl;\n}\n\n"
  dependsOn:
  - template/template.cpp
  - math/combinatorics/mod-int.cpp
  - math/fft/number-theoretic-transform-friendly-mod-int.cpp
  - math/fps/partition.cpp
  - math/fps/formal-power-series.cpp
  - math/fps/inv.cpp
  isVerificationFile: true
  path: test/verify/yosupo-partition-function.test.cpp
  requiredBy: []
  timestamp: '2021-06-23 17:44:06+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-partition-function.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-partition-function.test.cpp
- /verify/test/verify/yosupo-partition-function.test.cpp.html
title: test/verify/yosupo-partition-function.test.cpp
---
