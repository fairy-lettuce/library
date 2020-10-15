---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bellnoulli-number.test.cpp
    title: test/verify/yosupo-bellnoulli-number.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-exp-of-formal-power-series.test.cpp
    title: test/verify/yosupo-exp-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-find-linear-recurrence.test.cpp
    title: test/verify/yosupo-find-linear-recurrence.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-inv-of-formal-power-series.test.cpp
    title: test/verify/yosupo-inv-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-log-of-formal-power-series.test.cpp
    title: test/verify/yosupo-log-of-formal-power-series.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-partition-function.test.cpp
    title: test/verify/yosupo-partition-function.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sparse-matrix-det.test.cpp
    title: test/verify/yosupo-sparse-matrix-det.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
    title: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\u7D1A\u6570)"
    links: []
  bundledCode: "#line 1 \"math/fps/formal-power-series.cpp\"\n/**\n * @brief Formal-Power-Series(\u5F62\
    \u5F0F\u7684\u51AA\u7D1A\u6570)\n */\ntemplate< typename T >\nstruct FormalPowerSeries\
    \ : vector< T > {\n  using vector< T >::vector;\n  using P = FormalPowerSeries;\n\
    \n  using MULT = function< vector< T >(P, P) >;\n  using FFT = function< void(P\
    \ &) >;\n  using SQRT = function< T(T) >;\n\n  static MULT &get_mult() {\n   \
    \ static MULT mult = nullptr;\n    return mult;\n  }\n\n  static void set_mult(MULT\
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
    \    auto ret = get_mult()(*this, r);\n    return *this = P(begin(ret), end(ret));\n\
    \  }\n\n  P &operator%=(const P &r) { return *this -= *this / r * r; }\n\n  P\
    \ operator-() const {\n    P ret(this->size());\n    for(int i = 0; i < this->size();\
    \ i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n  P &operator/=(const P\
    \ &r) {\n    if(this->size() < r.size()) {\n      this->clear();\n      return\
    \ *this;\n    }\n    int n = this->size() - r.size() + 1;\n    return *this =\
    \ (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n  }\n\n  P dot(P r) const {\n\
    \    P ret(min(this->size(), r.size()));\n    for(int i = 0; i < ret.size(); i++)\
    \ ret[i] = (*this)[i] * r[i];\n    return ret;\n  }\n\n  P pre(int sz) const {\
    \ return P(begin(*this), begin(*this) + min((int) this->size(), sz)); }\n\n  P\
    \ operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n    P ret(*this);\n\
    \    ret.erase(ret.begin(), ret.begin() + sz);\n    return ret;\n  }\n\n  P operator<<(int\
    \ sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(), sz, T(0));\n   \
    \ return ret;\n  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n    if(deg\
    \ != -1) ret.resize(deg, T(0));\n    reverse(begin(ret), end(ret));\n    return\
    \ ret;\n  }\n\n  P diff() const {\n    const int n = (int) this->size();\n   \
    \ P ret(max(0, n - 1));\n    for(int i = 1; i < n; i++) ret[i - 1] = (*this)[i]\
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
    \      return ret.exp_fast(deg);\n    }\n    P ret({T(1)});\n    for(int i = 1;\
    \ i < deg; i <<= 1) {\n      ret = (ret * (pre(i << 1) + T(1) - ret.log(i << 1))).pre(i\
    \ << 1);\n    }\n    return ret.pre(deg);\n  }\n\n  P exp_fast(int deg) const\
    \ {\n    if(deg == -1) deg = this->size();\n    assert((*this)[0] == T(0));\n\n\
    \    P inv;\n    inv.reserve(deg + 1);\n    inv.push_back(T(0));\n    inv.push_back(T(1));\n\
    \n    auto inplace_integral = [&](P &F) -> void {\n      const int n = (int) F.size();\n\
    \      auto mod = T::get_mod();\n      while((int) inv.size() <= n) {\n      \
    \  int i = inv.size();\n        inv.push_back((-inv[mod % i]) * (mod / i));\n\
    \      }\n      F.insert(begin(F), T(0));\n      for(int i = 1; i <= n; i++) F[i]\
    \ *= inv[i];\n    };\n\n    auto inplace_diff = [](P &F) -> void {\n      if(F.empty())\
    \ return;\n      F.erase(begin(F));\n      T coeff = 1, one = 1;\n      for(int\
    \ i = 0; i < (int) F.size(); i++) {\n        F[i] *= coeff;\n        coeff +=\
    \ one;\n      }\n    };\n\n    P b{1, 1 < (int) this->size() ? (*this)[1] : 0},\
    \ c{1}, z1, z2{1, 1};\n    for(int m = 2; m < deg; m *= 2) {\n      auto y = b;\n\
    \      y.resize(2 * m);\n      get_fft()(y);\n      z1 = z2;\n      P z(m);\n\
    \      for(int i = 0; i < m; ++i) z[i] = y[i] * z1[i];\n      get_ifft()(z);\n\
    \      fill(begin(z), begin(z) + m / 2, T(0));\n      get_fft()(z);\n      for(int\
    \ i = 0; i < m; ++i) z[i] *= -z1[i];\n      get_ifft()(z);\n      c.insert(end(c),\
    \ begin(z) + m / 2, end(z));\n      z2 = c;\n      z2.resize(2 * m);\n      get_fft()(z2);\n\
    \      P x(begin(*this), begin(*this) + min< int >(this->size(), m));\n      inplace_diff(x);\n\
    \      x.push_back(T(0));\n      get_fft()(x);\n      for(int i = 0; i < m; ++i)\
    \ x[i] *= y[i];\n      get_ifft()(x);\n      x -= b.diff();\n      x.resize(2\
    \ * m);\n      for(int i = 0; i < m - 1; ++i) x[m + i] = x[i], x[i] = T(0);\n\
    \      get_fft()(x);\n      for(int i = 0; i < 2 * m; ++i) x[i] *= z2[i];\n  \
    \    get_ifft()(x);\n      x.pop_back();\n      inplace_integral(x);\n      for(int\
    \ i = m; i < min< int >(this->size(), 2 * m); ++i) x[i] += (*this)[i];\n     \
    \ fill(begin(x), begin(x) + m, T(0));\n      get_fft()(x);\n      for(int i =\
    \ 0; i < 2 * m; ++i) x[i] *= y[i];\n      get_ifft()(x);\n      b.insert(end(b),\
    \ begin(x) + m, end(x));\n    }\n    return P{begin(b), begin(b) + deg};\n  }\n\
    \n\n  P inv_fast() const {\n    assert(((*this)[0]) != T(0));\n\n    const int\
    \ n = (int) this->size();\n    P res{T(1) / (*this)[0]};\n\n    for(int d = 1;\
    \ d < n; d <<= 1) {\n      P f(2 * d), g(2 * d);\n      for(int j = 0; j < min(n,\
    \ 2 * d); j++) f[j] = (*this)[j];\n      for(int j = 0; j < d; j++) g[j] = res[j];\n\
    \      get_fft()(f);\n      get_fft()(g);\n      for(int j = 0; j < 2 * d; j++)\
    \ f[j] *= g[j];\n      get_ifft()(f);\n      for(int j = 0; j < d; j++) {\n  \
    \      f[j] = 0;\n        f[j + d] = -f[j + d];\n      }\n      get_fft()(f);\n\
    \      for(int j = 0; j < 2 * d; j++) f[j] *= g[j];\n      get_ifft()(f);\n  \
    \    for(int j = 0; j < d; j++) f[j] = res[j];\n      res = f;\n    }\n    return\
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
    \     x -= get_div(x) * mod;\n      n >>= 1;\n    }\n    return ret;\n  }\n};\n"
  code: "/**\n * @brief Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\u7D1A\u6570)\n\
    \ */\ntemplate< typename T >\nstruct FormalPowerSeries : vector< T > {\n  using\
    \ vector< T >::vector;\n  using P = FormalPowerSeries;\n\n  using MULT = function<\
    \ vector< T >(P, P) >;\n  using FFT = function< void(P &) >;\n  using SQRT = function<\
    \ T(T) >;\n\n  static MULT &get_mult() {\n    static MULT mult = nullptr;\n  \
    \  return mult;\n  }\n\n  static void set_mult(MULT f) {\n    get_mult() = f;\n\
    \  }\n\n  static FFT &get_fft() {\n    static FFT fft = nullptr;\n    return fft;\n\
    \  }\n\n  static FFT &get_ifft() {\n    static FFT ifft = nullptr;\n    return\
    \ ifft;\n  }\n\n  static void set_fft(FFT f, FFT g) {\n    get_fft() = f;\n  \
    \  get_ifft() = g;\n  }\n\n  static SQRT &get_sqrt() {\n    static SQRT sqr =\
    \ nullptr;\n    return sqr;\n  }\n\n  static void set_sqrt(SQRT sqr) {\n    get_sqrt()\
    \ = sqr;\n  }\n\n  void shrink() {\n    while(this->size() && this->back() ==\
    \ T(0)) this->pop_back();\n  }\n\n  P operator+(const P &r) const { return P(*this)\
    \ += r; }\n\n  P operator+(const T &v) const { return P(*this) += v; }\n\n  P\
    \ operator-(const P &r) const { return P(*this) -= r; }\n\n  P operator-(const\
    \ T &v) const { return P(*this) -= v; }\n\n  P operator*(const P &r) const { return\
    \ P(*this) *= r; }\n\n  P operator*(const T &v) const { return P(*this) *= v;\
    \ }\n\n  P operator/(const P &r) const { return P(*this) /= r; }\n\n  P operator%(const\
    \ P &r) const { return P(*this) %= r; }\n\n  P &operator+=(const P &r) {\n   \
    \ if(r.size() > this->size()) this->resize(r.size());\n    for(int i = 0; i <\
    \ r.size(); i++) (*this)[i] += r[i];\n    return *this;\n  }\n\n  P &operator+=(const\
    \ T &r) {\n    if(this->empty()) this->resize(1);\n    (*this)[0] += r;\n    return\
    \ *this;\n  }\n\n  P &operator-=(const P &r) {\n    if(r.size() > this->size())\
    \ this->resize(r.size());\n    for(int i = 0; i < r.size(); i++) (*this)[i] -=\
    \ r[i];\n    shrink();\n    return *this;\n  }\n\n  P &operator-=(const T &r)\
    \ {\n    if(this->empty()) this->resize(1);\n    (*this)[0] -= r;\n    shrink();\n\
    \    return *this;\n  }\n\n  P &operator*=(const T &v) {\n    const int n = (int)\
    \ this->size();\n    for(int k = 0; k < n; k++) (*this)[k] *= v;\n    return *this;\n\
    \  }\n\n  P &operator*=(const P &r) {\n    if(this->empty() || r.empty()) {\n\
    \      this->clear();\n      return *this;\n    }\n    assert(get_mult() != nullptr);\n\
    \    auto ret = get_mult()(*this, r);\n    return *this = P(begin(ret), end(ret));\n\
    \  }\n\n  P &operator%=(const P &r) { return *this -= *this / r * r; }\n\n  P\
    \ operator-() const {\n    P ret(this->size());\n    for(int i = 0; i < this->size();\
    \ i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n  P &operator/=(const P\
    \ &r) {\n    if(this->size() < r.size()) {\n      this->clear();\n      return\
    \ *this;\n    }\n    int n = this->size() - r.size() + 1;\n    return *this =\
    \ (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n  }\n\n  P dot(P r) const {\n\
    \    P ret(min(this->size(), r.size()));\n    for(int i = 0; i < ret.size(); i++)\
    \ ret[i] = (*this)[i] * r[i];\n    return ret;\n  }\n\n  P pre(int sz) const {\
    \ return P(begin(*this), begin(*this) + min((int) this->size(), sz)); }\n\n  P\
    \ operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n    P ret(*this);\n\
    \    ret.erase(ret.begin(), ret.begin() + sz);\n    return ret;\n  }\n\n  P operator<<(int\
    \ sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(), sz, T(0));\n   \
    \ return ret;\n  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n    if(deg\
    \ != -1) ret.resize(deg, T(0));\n    reverse(begin(ret), end(ret));\n    return\
    \ ret;\n  }\n\n  P diff() const {\n    const int n = (int) this->size();\n   \
    \ P ret(max(0, n - 1));\n    for(int i = 1; i < n; i++) ret[i - 1] = (*this)[i]\
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
    \      return ret.exp_fast(deg);\n    }\n    P ret({T(1)});\n    for(int i = 1;\
    \ i < deg; i <<= 1) {\n      ret = (ret * (pre(i << 1) + T(1) - ret.log(i << 1))).pre(i\
    \ << 1);\n    }\n    return ret.pre(deg);\n  }\n\n  P exp_fast(int deg) const\
    \ {\n    if(deg == -1) deg = this->size();\n    assert((*this)[0] == T(0));\n\n\
    \    P inv;\n    inv.reserve(deg + 1);\n    inv.push_back(T(0));\n    inv.push_back(T(1));\n\
    \n    auto inplace_integral = [&](P &F) -> void {\n      const int n = (int) F.size();\n\
    \      auto mod = T::get_mod();\n      while((int) inv.size() <= n) {\n      \
    \  int i = inv.size();\n        inv.push_back((-inv[mod % i]) * (mod / i));\n\
    \      }\n      F.insert(begin(F), T(0));\n      for(int i = 1; i <= n; i++) F[i]\
    \ *= inv[i];\n    };\n\n    auto inplace_diff = [](P &F) -> void {\n      if(F.empty())\
    \ return;\n      F.erase(begin(F));\n      T coeff = 1, one = 1;\n      for(int\
    \ i = 0; i < (int) F.size(); i++) {\n        F[i] *= coeff;\n        coeff +=\
    \ one;\n      }\n    };\n\n    P b{1, 1 < (int) this->size() ? (*this)[1] : 0},\
    \ c{1}, z1, z2{1, 1};\n    for(int m = 2; m < deg; m *= 2) {\n      auto y = b;\n\
    \      y.resize(2 * m);\n      get_fft()(y);\n      z1 = z2;\n      P z(m);\n\
    \      for(int i = 0; i < m; ++i) z[i] = y[i] * z1[i];\n      get_ifft()(z);\n\
    \      fill(begin(z), begin(z) + m / 2, T(0));\n      get_fft()(z);\n      for(int\
    \ i = 0; i < m; ++i) z[i] *= -z1[i];\n      get_ifft()(z);\n      c.insert(end(c),\
    \ begin(z) + m / 2, end(z));\n      z2 = c;\n      z2.resize(2 * m);\n      get_fft()(z2);\n\
    \      P x(begin(*this), begin(*this) + min< int >(this->size(), m));\n      inplace_diff(x);\n\
    \      x.push_back(T(0));\n      get_fft()(x);\n      for(int i = 0; i < m; ++i)\
    \ x[i] *= y[i];\n      get_ifft()(x);\n      x -= b.diff();\n      x.resize(2\
    \ * m);\n      for(int i = 0; i < m - 1; ++i) x[m + i] = x[i], x[i] = T(0);\n\
    \      get_fft()(x);\n      for(int i = 0; i < 2 * m; ++i) x[i] *= z2[i];\n  \
    \    get_ifft()(x);\n      x.pop_back();\n      inplace_integral(x);\n      for(int\
    \ i = m; i < min< int >(this->size(), 2 * m); ++i) x[i] += (*this)[i];\n     \
    \ fill(begin(x), begin(x) + m, T(0));\n      get_fft()(x);\n      for(int i =\
    \ 0; i < 2 * m; ++i) x[i] *= y[i];\n      get_ifft()(x);\n      b.insert(end(b),\
    \ begin(x) + m, end(x));\n    }\n    return P{begin(b), begin(b) + deg};\n  }\n\
    \n\n  P inv_fast() const {\n    assert(((*this)[0]) != T(0));\n\n    const int\
    \ n = (int) this->size();\n    P res{T(1) / (*this)[0]};\n\n    for(int d = 1;\
    \ d < n; d <<= 1) {\n      P f(2 * d), g(2 * d);\n      for(int j = 0; j < min(n,\
    \ 2 * d); j++) f[j] = (*this)[j];\n      for(int j = 0; j < d; j++) g[j] = res[j];\n\
    \      get_fft()(f);\n      get_fft()(g);\n      for(int j = 0; j < 2 * d; j++)\
    \ f[j] *= g[j];\n      get_ifft()(f);\n      for(int j = 0; j < d; j++) {\n  \
    \      f[j] = 0;\n        f[j + d] = -f[j + d];\n      }\n      get_fft()(f);\n\
    \      for(int j = 0; j < 2 * d; j++) f[j] *= g[j];\n      get_ifft()(f);\n  \
    \    for(int j = 0; j < d; j++) f[j] = res[j];\n      res = f;\n    }\n    return\
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
    \     x -= get_div(x) * mod;\n      n >>= 1;\n    }\n    return ret;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/formal-power-series.cpp
  requiredBy: []
  timestamp: '2020-10-15 14:44:09+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-exp-of-formal-power-series.test.cpp
  - test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
  - test/verify/yosupo-find-linear-recurrence.test.cpp
  - test/verify/yosupo-polynomial-interpolation.test.cpp
  - test/verify/yosupo-log-of-formal-power-series.test.cpp
  - test/verify/yosupo-partition-function.test.cpp
  - test/verify/yosupo-bellnoulli-number.test.cpp
  - test/verify/yosupo-multipoint-evaluation.test.cpp
  - test/verify/yosupo-sparse-matrix-det.test.cpp
  - test/verify/yosupo-inv-of-formal-power-series.test.cpp
documentation_of: math/fps/formal-power-series.cpp
layout: document
redirect_from:
- /library/math/fps/formal-power-series.cpp
- /library/math/fps/formal-power-series.cpp.html
title: "Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\u7D1A\u6570)"
---
