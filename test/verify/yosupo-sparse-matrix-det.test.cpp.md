---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-int.cpp
    title: math/combinatorics/mod-int.cpp
  - icon: ':heavy_check_mark:'
    path: math/fps/berlekamp-massey.cpp
    title: math/fps/berlekamp-massey.cpp
  - icon: ':heavy_check_mark:'
    path: math/fps/formal-power-series.cpp
    title: math/fps/formal-power-series.cpp
  - icon: ':heavy_check_mark:'
    path: math/fps/sparse-matrix.cpp
    title: math/fps/sparse-matrix.cpp
  - icon: ':heavy_check_mark:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/sparse_matrix_det
    links:
    - https://judge.yosupo.jp/problem/sparse_matrix_det
  bundledCode: "#line 1 \"test/verify/yosupo-sparse-matrix-det.test.cpp\"\n#define\
    \ PROBLEM \"https://judge.yosupo.jp/problem/sparse_matrix_det\"\n\n#line 1 \"\
    template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace std;\n\nusing\
    \ int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll = (1LL <<\
    \ 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup() {\n\
    \    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed <<\
    \ setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-sparse-matrix-det.test.cpp\"\
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
    \ { return mod; }\n};\n\nusing modint = ModInt< mod >;\n#line 6 \"test/verify/yosupo-sparse-matrix-det.test.cpp\"\
    \n\n#line 1 \"math/fps/formal-power-series.cpp\"\ntemplate< typename T >\nstruct\
    \ FormalPowerSeries : vector< T > {\n  using vector< T >::vector;\n  using P =\
    \ FormalPowerSeries;\n\n  using MULT = function< P(P, P) >;\n  using FFT = function<\
    \ void(P &) >;\n  using SQRT = function< T(T) >;\n\n  static MULT &get_mult()\
    \ {\n    static MULT mult = nullptr;\n    return mult;\n  }\n\n  static void set_mult(MULT\
    \ f) {\n    get_mult() = f;\n  }\n\n  static FFT &get_fft() {\n    static FFT\
    \ fft = nullptr;\n    return fft;\n  }\n\n  static FFT &get_ifft() {\n    static\
    \ FFT ifft = nullptr;\n    return ifft;\n  }\n\n  static void set_fft(FFT f, FFT\
    \ g) {\n    get_fft() = f;\n    get_ifft() = g;\n  }\n\n  static SQRT &get_sqrt()\
    \ {\n    static SQRT sqr = nullptr;\n    return sqr;\n  }\n\n  static void set_sqrt(SQRT\
    \ sqr) {\n    get_sqrt() = sqr;\n  }\n\n  void shrink() {\n    while(this->size()\
    \ && this->back() == T(0)) this->pop_back();\n  }\n\n  P operator+(const P &r)\
    \ const { return P(*this) += r; }\n\n  P operator+(const T &v) const { return\
    \ P(*this) += v; }\n\n  P operator-(const P &r) const { return P(*this) -= r;\
    \ }\n\n  P operator-(const T &v) const { return P(*this) -= v; }\n\n  P operator*(const\
    \ P &r) const { return P(*this) *= r; }\n\n  P operator*(const T &v) const { return\
    \ P(*this) *= v; }\n\n  P operator/(const P &r) const { return P(*this) /= r;\
    \ }\n\n  P operator%(const P &r) const { return P(*this) %= r; }\n\n  P &operator+=(const\
    \ P &r) {\n    if(r.size() > this->size()) this->resize(r.size());\n    for(int\
    \ i = 0; i < r.size(); i++) (*this)[i] += r[i];\n    return *this;\n  }\n\n  P\
    \ &operator+=(const T &r) {\n    if(this->empty()) this->resize(1);\n    (*this)[0]\
    \ += r;\n    return *this;\n  }\n\n  P &operator-=(const P &r) {\n    if(r.size()\
    \ > this->size()) this->resize(r.size());\n    for(int i = 0; i < r.size(); i++)\
    \ (*this)[i] -= r[i];\n    shrink();\n    return *this;\n  }\n\n  P &operator-=(const\
    \ T &r) {\n    if(this->empty()) this->resize(1);\n    (*this)[0] -= r;\n    shrink();\n\
    \    return *this;\n  }\n\n  P &operator*=(const T &v) {\n    const int n = (int)\
    \ this->size();\n    for(int k = 0; k < n; k++) (*this)[k] *= v;\n    return *this;\n\
    \  }\n\n  P &operator*=(const P &r) {\n    if(this->empty() || r.empty()) {\n\
    \      this->clear();\n      return *this;\n    }\n    assert(get_mult() != nullptr);\n\
    \    return *this = get_mult()(*this, r);\n  }\n\n  P &operator%=(const P &r)\
    \ { return *this -= *this / r * r; }\n\n  P operator-() const {\n    P ret(this->size());\n\
    \    for(int i = 0; i < this->size(); i++) ret[i] = -(*this)[i];\n    return ret;\n\
    \  }\n\n  P &operator/=(const P &r) {\n    if(this->size() < r.size()) {\n   \
    \   this->clear();\n      return *this;\n    }\n    int n = this->size() - r.size()\
    \ + 1;\n    return *this = (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n  }\n\
    \n  P dot(P r) const {\n    P ret(min(this->size(), r.size()));\n    for(int i\
    \ = 0; i < ret.size(); i++) ret[i] = (*this)[i] * r[i];\n    return ret;\n  }\n\
    \n  P pre(int sz) const { return P(begin(*this), begin(*this) + min((int) this->size(),\
    \ sz)); }\n\n  P operator>>(int sz) const {\n    if(this->size() <= sz) return\
    \ {};\n    P ret(*this);\n    ret.erase(ret.begin(), ret.begin() + sz);\n    return\
    \ ret;\n  }\n\n  P operator<<(int sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(),\
    \ sz, T(0));\n    return ret;\n  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n\
    \    if(deg != -1) ret.resize(deg, T(0));\n    reverse(begin(ret), end(ret));\n\
    \    return ret;\n  }\n\n  P diff() const {\n    const int n = (int) this->size();\n\
    \    P ret(max(0, n - 1));\n    for(int i = 1; i < n; i++) ret[i - 1] = (*this)[i]\
    \ * T(i);\n    return ret;\n  }\n\n  P integral() const {\n    const int n = (int)\
    \ this->size();\n    P ret(n + 1);\n    ret[0] = T(0);\n    for(int i = 0; i <\
    \ n; i++) ret[i + 1] = (*this)[i] / T(i + 1);\n    return ret;\n  }\n\n  // F(0)\
    \ must not be 0\n  P inv(int deg = -1) const {\n    assert(((*this)[0]) != T(0));\n\
    \    const int n = (int) this->size();\n    if(deg == -1) deg = n;\n    if(get_fft()\
    \ != nullptr) {\n      P ret(*this);\n      ret.resize(deg, T(0));\n      return\
    \ ret.inv_fast();\n    }\n    P ret({T(1) / (*this)[0]});\n    for(int i = 1;\
    \ i < deg; i <<= 1) {\n      ret = (ret + ret - ret * ret * pre(i << 1)).pre(i\
    \ << 1);\n    }\n    return ret.pre(deg);\n  }\n\n  // F(0) must be 1\n  P log(int\
    \ deg = -1) const {\n    assert((*this)[0] == 1);\n    const int n = (int) this->size();\n\
    \    if(deg == -1) deg = n;\n    return (this->diff() * this->inv(deg)).pre(deg\
    \ - 1).integral();\n  }\n\n  P sqrt(int deg = -1) const {\n    const int n = (int)\
    \ this->size();\n    if(deg == -1) deg = n;\n    if((*this)[0] == T(0)) {\n  \
    \    for(int i = 1; i < n; i++) {\n        if((*this)[i] != T(0)) {\n        \
    \  if(i & 1) return {};\n          if(deg - i / 2 <= 0) break;\n          auto\
    \ ret = (*this >> i).sqrt(deg - i / 2);\n          if(ret.empty()) return {};\n\
    \          ret = ret << (i / 2);\n          if(ret.size() < deg) ret.resize(deg,\
    \ T(0));\n          return ret;\n        }\n      }\n      return P(deg, 0);\n\
    \    }\n\n    P ret;\n    if(get_sqrt() == nullptr) {\n      assert((*this)[0]\
    \ == T(1));\n      ret = {T(1)};\n    } else {\n      auto sqr = get_sqrt()((*this)[0]);\n\
    \      if(sqr * sqr != (*this)[0]) return {};\n      ret = {T(sqr)};\n    }\n\n\
    \    T inv2 = T(1) / T(2);\n    for(int i = 1; i < deg; i <<= 1) {\n      ret\
    \ = (ret + pre(i << 1) * ret.inv(i << 1)) * inv2;\n    }\n    return ret.pre(deg);\n\
    \  }\n\n  // F(0) must be 0\n  P exp(int deg = -1) const {\n    assert((*this)[0]\
    \ == T(0));\n    const int n = (int) this->size();\n    if(deg == -1) deg = n;\n\
    \    if(get_fft() != nullptr) {\n      P ret(*this);\n      ret.resize(deg, T(0));\n\
    \      return ret.exp_rec();\n    }\n    P ret({T(1)});\n    for(int i = 1; i\
    \ < deg; i <<= 1) {\n      ret = (ret * (pre(i << 1) + T(1) - ret.log(i << 1))).pre(i\
    \ << 1);\n    }\n    return ret.pre(deg);\n  }\n\n\n  P online_convolution_exp(const\
    \ P &conv_coeff) const {\n    const int n = (int) conv_coeff.size();\n    assert((n\
    \ & (n - 1)) == 0);\n    vector< P > conv_ntt_coeff;\n    auto& fft = get_fft();\n\
    \    auto& ifft = get_ifft();\n    for(int i = n; i >= 1; i >>= 1) {\n      P\
    \ g(conv_coeff.pre(i));\n      fft(g);\n      conv_ntt_coeff.emplace_back(g);\n\
    \    }\n    P conv_arg(n), conv_ret(n);\n    auto rec = [&](auto rec, int l, int\
    \ r, int d) -> void {\n      if(r - l <= 16) {\n        for(int i = l; i < r;\
    \ i++) {\n          T sum = 0;\n          for(int j = l; j < i; j++) sum += conv_arg[j]\
    \ * conv_coeff[i - j];\n          conv_ret[i] += sum;\n          conv_arg[i] =\
    \ i == 0 ? T(1) : conv_ret[i] / i;\n        }\n      } else {\n        int m =\
    \ (l + r) / 2;\n        rec(rec, l, m, d + 1);\n        P pre(r - l);\n      \
    \  for(int i = 0; i < m - l; i++) pre[i] = conv_arg[l + i];\n        fft(pre);\n\
    \        for(int i = 0; i < r - l; i++) pre[i] *= conv_ntt_coeff[d][i];\n    \
    \    ifft(pre);\n        for(int i = 0; i < r - m; i++) conv_ret[m + i] += pre[m\
    \ + i - l];\n        rec(rec, m, r, d + 1);\n      }\n    };\n    rec(rec, 0,\
    \ n, 0);\n    return conv_arg;\n  }\n\n  P exp_rec() const {\n    assert((*this)[0]\
    \ == T(0));\n    const int n = (int) this->size();\n    int m = 1;\n    while(m\
    \ < n) m *= 2;\n    P conv_coeff(m);\n    for(int i = 1; i < n; i++) conv_coeff[i]\
    \ = (*this)[i] * i;\n    return online_convolution_exp(conv_coeff).pre(n);\n \
    \ }\n\n\n  P inv_fast() const {\n    assert(((*this)[0]) != T(0));\n\n    const\
    \ int n = (int) this->size();\n    P res{T(1) / (*this)[0]};\n\n    for(int d\
    \ = 1; d < n; d <<= 1) {\n      P f(2 * d), g(2 * d);\n      for(int j = 0; j\
    \ < min(n, 2 * d); j++) f[j] = (*this)[j];\n      for(int j = 0; j < d; j++) g[j]\
    \ = res[j];\n      get_fft()(f);\n      get_fft()(g);\n      for(int j = 0; j\
    \ < 2 * d; j++) f[j] *= g[j];\n      get_ifft()(f);\n      for(int j = 0; j <\
    \ d; j++) {\n        f[j] = 0;\n        f[j + d] = -f[j + d];\n      }\n     \
    \ get_fft()(f);\n      for(int j = 0; j < 2 * d; j++) f[j] *= g[j];\n      get_ifft()(f);\n\
    \      for(int j = 0; j < d; j++) f[j] = res[j];\n      res = f;\n    }\n    return\
    \ res.pre(n);\n  }\n\n  P pow(int64_t k, int deg = -1) const {\n    const int\
    \ n = (int) this->size();\n    if(deg == -1) deg = n;\n    for(int i = 0; i <\
    \ n; i++) {\n      if((*this)[i] != T(0)) {\n        T rev = T(1) / (*this)[i];\n\
    \        P ret = (((*this * rev) >> i).log() * k).exp() * ((*this)[i].pow(k));\n\
    \        if(i * k > deg) return P(deg, T(0));\n        ret = (ret << (i * k)).pre(deg);\n\
    \        if(ret.size() < deg) ret.resize(deg, T(0));\n        return ret;\n  \
    \    }\n    }\n    return *this;\n  }\n\n  T eval(T x) const {\n    T r = 0, w\
    \ = 1;\n    for(auto &v : *this) {\n      r += w * v;\n      w *= x;\n    }\n\
    \    return r;\n  }\n\n  P pow_mod(int64_t n, P mod) const {\n    P modinv = mod.rev().inv();\n\
    \    auto get_div = [&](P base) {\n      if(base.size() < mod.size()) {\n    \
    \    base.clear();\n        return base;\n      }\n      int n = base.size() -\
    \ mod.size() + 1;\n      return (base.rev().pre(n) * modinv.pre(n)).pre(n).rev(n);\n\
    \    };\n    P x(*this), ret{1};\n    while(n > 0) {\n      if(n & 1) {\n    \
    \    ret *= x;\n        ret -= get_div(ret) * mod;\n      }\n      x *= x;\n \
    \     x -= get_div(x) * mod;\n      n >>= 1;\n    }\n    return ret;\n  }\n};\n\
    #line 8 \"test/verify/yosupo-sparse-matrix-det.test.cpp\"\n\n#line 1 \"math/fps/berlekamp-massey.cpp\"\
    \ntemplate< class T >\nFormalPowerSeries< T > berlekamp_massey(const FormalPowerSeries<\
    \ T > &s) {\n  const int N = (int) s.size();\n  FormalPowerSeries< T > b = {T(-1)},\
    \ c = {T(-1)};\n  T y = T(1);\n  for(int ed = 1; ed <= N; ed++) {\n    int l =\
    \ int(c.size()), m = int(b.size());\n    T x = 0;\n    for(int i = 0; i < l; i++)\
    \ x += c[i] * s[ed - l + i];\n    b.emplace_back(0);\n    m++;\n    if(x == T(0))\
    \ continue;\n    T freq = x / y;\n    if(l < m) {\n      auto tmp = c;\n     \
    \ c.insert(begin(c), m - l, T(0));\n      for(int i = 0; i < m; i++) c[m - 1 -\
    \ i] -= freq * b[m - 1 - i];\n      b = tmp;\n      y = x;\n    } else {\n   \
    \   for(int i = 0; i < m; i++) c[l - 1 - i] -= freq * b[m - 1 - i];\n    }\n \
    \ }\n  return c;\n}\n#line 1 \"math/fps/sparse-matrix.cpp\"\ntemplate< typename\
    \ T >\nusing FPSGraph = vector< vector< pair< int, T > > >;\n\ntemplate< typename\
    \ T >\nFormalPowerSeries< T > random_poly(int n) {\n  mt19937 mt(1333333);\n \
    \ FormalPowerSeries< T > res(n);\n  uniform_int_distribution< int > rand(0, T::get_mod()\
    \ - 1);\n  for(int i = 0; i < n; i++) res[i] = rand(mt);\n  return res;\n}\n\n\
    template< typename T >\nFormalPowerSeries< T > next_poly(const FormalPowerSeries<\
    \ T > &dp, const FPSGraph< T > &g) {\n  const int N = (int) dp.size();\n  FormalPowerSeries<\
    \ T > nxt(N);\n  for(int i = 0; i < N; i++) {\n    for(auto &p : g[i]) nxt[p.first]\
    \ += p.second * dp[i];\n  }\n  return nxt;\n}\n\ntemplate< typename T >\nFormalPowerSeries<\
    \ T > minimum_poly(const FPSGraph< T > &g) {\n  const int N = (int) g.size();\n\
    \  auto dp = random_poly< T >(N), u = random_poly< T >(N);\n  FormalPowerSeries<\
    \ T > f(2 * N);\n  for(int i = 0; i < 2 * N; i++) {\n    for(auto &p : u.dot(dp))\
    \ f[i] += p;\n    dp = next_poly(dp, g);\n  }\n  return berlekamp_massey(f);\n\
    }\n\n/* O(N(N+S) + N log N log Q) (O(S): time complexity of nex) */\ntemplate<\
    \ typename T >\nFormalPowerSeries< T > sparse_pow(int64_t Q, FormalPowerSeries<\
    \ T > dp, const FPSGraph< T > &g) {\n  const int N = (int) dp.size();\n  auto\
    \ A = FormalPowerSeries< T >({0, 1}).pow_mod(Q, minimum_poly(g));\n  FormalPowerSeries<\
    \ T > res(N);\n  for(int i = 0; i < A.size(); i++) {\n    res += dp * A[i];\n\
    \    dp = next_poly(dp, g);\n  }\n  return res;\n}\n\n/* O(N(N+S)) (S: none-zero\
    \ elements)*/\ntemplate< typename T >\nT sparse_determinant(FPSGraph< T > g) {\n\
    \  using FPS = FormalPowerSeries< T >;\n  int N = (int) g.size();\n  auto C =\
    \ random_poly< T >(N);\n  for(int i = 0; i < N; i++) for(auto &p : g[i]) p.second\
    \ *= C[i];\n  auto u = minimum_poly(g);\n  T acdet = u[0];\n  if(N % 2 == 0) acdet\
    \ *= -1;\n  T cdet = 1;\n  for(int i = 0; i < N; i++) cdet *= C[i];\n  return\
    \ acdet / cdet;\n}\n#line 11 \"test/verify/yosupo-sparse-matrix-det.test.cpp\"\
    \n\nconst int MOD = 998244353;\nusing mint = ModInt< MOD >;\n\nint main() {\n\
    \  int N, K;\n  cin >> N >> K;\n  FPSGraph< mint > g(N);\n  for(int i = 0; i <\
    \ K; i++) {\n    int a, b, c;\n    cin >> a >> b >> c;\n    g[a].emplace_back(b,\
    \ c);\n  }\n  cout << sparse_determinant(g) << endl;\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/sparse_matrix_det\"\n\n\
    #include \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/mod-int.cpp\"\
    \n\n#include \"../../math/fps/formal-power-series.cpp\"\n\n#include \"../../math/fps/berlekamp-massey.cpp\"\
    \n#include \"../../math/fps/sparse-matrix.cpp\"\n\nconst int MOD = 998244353;\n\
    using mint = ModInt< MOD >;\n\nint main() {\n  int N, K;\n  cin >> N >> K;\n \
    \ FPSGraph< mint > g(N);\n  for(int i = 0; i < K; i++) {\n    int a, b, c;\n \
    \   cin >> a >> b >> c;\n    g[a].emplace_back(b, c);\n  }\n  cout << sparse_determinant(g)\
    \ << endl;\n}\n"
  dependsOn:
  - template/template.cpp
  - math/combinatorics/mod-int.cpp
  - math/fps/formal-power-series.cpp
  - math/fps/berlekamp-massey.cpp
  - math/fps/sparse-matrix.cpp
  isVerificationFile: true
  path: test/verify/yosupo-sparse-matrix-det.test.cpp
  requiredBy: []
  timestamp: '2019-12-12 22:16:00+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-sparse-matrix-det.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-sparse-matrix-det.test.cpp
- /verify/test/verify/yosupo-sparse-matrix-det.test.cpp.html
title: test/verify/yosupo-sparse-matrix-det.test.cpp
---
