---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Formal-Power-Series-Friendly-NTT(NTTmod\u7528\u5F62\u5F0F\u7684\
      \u51AA\u7D1A\u6570)"
    links:
    - https://judge.yosupo.jp/problem/convolution_mod
    - https://judge.yosupo.jp/problem/exp_of_formal_power_series
    - https://judge.yosupo.jp/problem/inv_of_formal_power_series
    - https://judge.yosupo.jp/problem/log_of_formal_power_series
    - https://judge.yosupo.jp/problem/polynomial_taylor_shift
    - https://judge.yosupo.jp/problem/pow_of_formal_power_series
    - https://judge.yosupo.jp/problem/sqrt_of_formal_power_series
  bundledCode: "#line 1 \"math/fps/formal-power-series-friendly-ntt.cpp\"\n/**\n *\
    \ @brief Formal-Power-Series-Friendly-NTT(NTTmod\u7528\u5F62\u5F0F\u7684\u51AA\
    \u7D1A\u6570)\n */\ntemplate< typename T >\nstruct FormalPowerSeriesFriendlyNTT\
    \ : vector< T > {\n  using vector< T >::vector;\n  using P = FormalPowerSeriesFriendlyNTT;\n\
    \  using NTT = NumberTheoreticTransformFriendlyModInt< T >;\n\n  P pre(int deg)\
    \ const {\n    return P(begin(*this), begin(*this) + min((int) this->size(), deg));\n\
    \  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n    if(deg != -1) ret.resize(deg,\
    \ T(0));\n    reverse(begin(ret), end(ret));\n    return ret;\n  }\n\n  void shrink()\
    \ {\n    while(this->size() && this->back() == T(0)) this->pop_back();\n  }\n\n\
    \  P operator+(const P &r) const { return P(*this) += r; }\n\n  P operator+(const\
    \ T &v) const { return P(*this) += v; }\n\n  P operator-(const P &r) const { return\
    \ P(*this) -= r; }\n\n  P operator-(const T &v) const { return P(*this) -= v;\
    \ }\n\n  P operator*(const P &r) const { return P(*this) *= r; }\n\n  P operator*(const\
    \ T &v) const { return P(*this) *= v; }\n\n  P operator/(const P &r) const { return\
    \ P(*this) /= r; }\n\n  P operator%(const P &r) const { return P(*this) %= r;\
    \ }\n\n  P &operator+=(const P &r) {\n    if(r.size() > this->size()) this->resize(r.size());\n\
    \    for(int i = 0; i < r.size(); i++) (*this)[i] += r[i];\n    return *this;\n\
    \  }\n\n  P &operator-=(const P &r) {\n    if(r.size() > this->size()) this->resize(r.size());\n\
    \    for(int i = 0; i < r.size(); i++) (*this)[i] -= r[i];\n    return *this;\n\
    \  }\n\n  // https://judge.yosupo.jp/problem/convolution_mod\n  P &operator*=(const\
    \ P &r) {\n    if(this->empty() || r.empty()) {\n      this->clear();\n      return\
    \ *this;\n    }\n    auto ret = NTT::multiply(*this, r);\n    return *this = {begin(ret),\
    \ end(ret)};\n  }\n\n  P &operator/=(const P &r) {\n    if(this->size() < r.size())\
    \ {\n      this->clear();\n      return *this;\n    }\n    int n = this->size()\
    \ - r.size() + 1;\n    return *this = (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n\
    \  }\n\n  P &operator%=(const P &r) {\n    return *this -= *this / r * r;\n  }\n\
    \n  P operator-() const {\n    P ret(this->size());\n    for(int i = 0; i < this->size();\
    \ i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n  P &operator+=(const T\
    \ &r) {\n    if(this->empty()) this->resize(1);\n    (*this)[0] += r;\n    return\
    \ *this;\n  }\n\n  P &operator-=(const T &r) {\n    if(this->empty()) this->resize(1);\n\
    \    (*this)[0] -= r;\n    return *this;\n  }\n\n  P &operator*=(const T &v) {\n\
    \    for(int i = 0; i < this->size(); i++) (*this)[i] *= v;\n    return *this;\n\
    \  }\n\n  P dot(P r) const {\n    P ret(min(this->size(), r.size()));\n    for(int\
    \ i = 0; i < ret.size(); i++) ret[i] = (*this)[i] * r[i];\n    return ret;\n \
    \ }\n\n  P operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n\
    \    P ret(*this);\n    ret.erase(ret.begin(), ret.begin() + sz);\n    return\
    \ ret;\n  }\n\n  P operator<<(int sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(),\
    \ sz, T(0));\n    return ret;\n  }\n\n  T operator()(T x) const {\n    T r = 0,\
    \ w = 1;\n    for(auto &v : *this) {\n      r += w * v;\n      w *= x;\n    }\n\
    \    return r;\n  }\n\n  P diff() const {\n    const int n = (int) this->size();\n\
    \    P ret(max(0, n - 1));\n    for(int i = 1; i < n; i++) ret[i - 1] = (*this)[i]\
    \ * T(i);\n    return ret;\n  }\n\n  P integral() const {\n    const int n = (int)\
    \ this->size();\n    P ret(n + 1);\n    ret[0] = T(0);\n    for(int i = 0; i <\
    \ n; i++) ret[i + 1] = (*this)[i] / T(i + 1);\n    return ret;\n  }\n\n  // https://judge.yosupo.jp/problem/inv_of_formal_power_series\n\
    \  // F(0) must not be 0\n  P inv(int deg = -1) const {\n    assert(((*this)[0])\
    \ != T(0));\n    const int n = (int) this->size();\n    if(deg == -1) deg = n;\n\
    \n    P res(deg);\n    res[0] = {T(1) / (*this)[0]};\n    for(int d = 1; d < n;\
    \ d <<= 1) {\n      P f(2 * d), g(2 * d);\n      for(int j = 0; j < min(n, 2 *\
    \ d); j++) f[j] = (*this)[j];\n      for(int j = 0; j < d; j++) g[j] = res[j];\n\
    \      NTT::ntt(f);\n      NTT::ntt(g);\n      f = f.dot(g);\n      NTT::intt(f);\n\
    \      for(int j = 0; j < d; j++) f[j] = 0;\n      NTT::ntt(f);\n      for(int\
    \ j = 0; j < 2 * d; j++) f[j] *= g[j];\n      NTT::intt(f);\n      for(int j =\
    \ d; j < min(2 * d, deg); j++) res[j] = -f[j];\n    }\n    return res;\n  }\n\n\
    \  // https://judge.yosupo.jp/problem/log_of_formal_power_series\n  // F(0) must\
    \ be 1\n  P log(int deg = -1) const {\n    assert((*this)[0] == T(1));\n    const\
    \ int n = (int) this->size();\n    if(deg == -1) deg = n;\n    return (this->diff()\
    \ * this->inv(deg)).pre(deg - 1).integral();\n  }\n\n  // https://judge.yosupo.jp/problem/sqrt_of_formal_power_series\n\
    \  P sqrt(int deg = -1, const function< T(T) > &get_sqrt = [](T) { return T(1);\
    \ }) const {\n    const int n = (int) this->size();\n    if(deg == -1) deg = n;\n\
    \    if((*this)[0] == T(0)) {\n      for(int i = 1; i < n; i++) {\n        if((*this)[i]\
    \ != T(0)) {\n          if(i & 1) return {};\n          if(deg - i / 2 <= 0) break;\n\
    \          auto ret = (*this >> i).sqrt(deg - i / 2, get_sqrt);\n          if(ret.empty())\
    \ return {};\n          ret = ret << (i / 2);\n          if(ret.size() < deg)\
    \ ret.resize(deg, T(0));\n          return ret;\n        }\n      }\n      return\
    \ P(deg, 0);\n    }\n    auto sqr = T(get_sqrt((*this)[0]));\n    if(sqr * sqr\
    \ != (*this)[0]) return {};\n    P ret{sqr};\n    T inv2 = T(1) / T(2);\n    for(int\
    \ i = 1; i < deg; i <<= 1) {\n      ret = (ret + pre(i << 1) * ret.inv(i << 1))\
    \ * inv2;\n    }\n    return ret.pre(deg);\n  }\n\n  P sqrt(const function< T(T)\
    \ > &get_sqrt, int deg = -1) const {\n    return sqrt(deg, get_sqrt);\n  }\n\n\
    \  // https://judge.yosupo.jp/problem/exp_of_formal_power_series\n  // F(0) must\
    \ be 0\n  P exp(int deg = -1) const {\n    if(deg == -1) deg = this->size();\n\
    \    assert((*this)[0] == T(0));\n\n    P inv;\n    inv.reserve(deg + 1);\n  \
    \  inv.push_back(T(0));\n    inv.push_back(T(1));\n\n    auto inplace_integral\
    \ = [&](P &F) -> void {\n      const int n = (int) F.size();\n      auto mod =\
    \ T::get_mod();\n      while((int) inv.size() <= n) {\n        int i = inv.size();\n\
    \        inv.push_back((-inv[mod % i]) * (mod / i));\n      }\n      F.insert(begin(F),\
    \ T(0));\n      for(int i = 1; i <= n; i++) F[i] *= inv[i];\n    };\n\n    auto\
    \ inplace_diff = [](P &F) -> void {\n      if(F.empty()) return;\n      F.erase(begin(F));\n\
    \      T coeff = 1, one = 1;\n      for(int i = 0; i < (int) F.size(); i++) {\n\
    \        F[i] *= coeff;\n        coeff += one;\n      }\n    };\n\n    P b{1,\
    \ 1 < (int) this->size() ? (*this)[1] : 0}, c{1}, z1, z2{1, 1};\n    for(int m\
    \ = 2; m < deg; m *= 2) {\n      auto y = b;\n      y.resize(2 * m);\n      NTT::ntt(y);\n\
    \      z1 = z2;\n      P z(m);\n      for(int i = 0; i < m; ++i) z[i] = y[i] *\
    \ z1[i];\n      NTT::intt(z);\n      fill(begin(z), begin(z) + m / 2, T(0));\n\
    \      NTT::ntt(z);\n      for(int i = 0; i < m; ++i) z[i] *= -z1[i];\n      NTT::intt(z);\n\
    \      c.insert(end(c), begin(z) + m / 2, end(z));\n      z2 = c;\n      z2.resize(2\
    \ * m);\n      NTT::ntt(z2);\n      P x(begin(*this), begin(*this) + min< int\
    \ >(this->size(), m));\n      inplace_diff(x);\n      x.push_back(T(0));\n   \
    \   NTT::ntt(x);\n      for(int i = 0; i < m; ++i) x[i] *= y[i];\n      NTT::intt(x);\n\
    \      x -= b.diff();\n      x.resize(2 * m);\n      for(int i = 0; i < m - 1;\
    \ ++i) x[m + i] = x[i], x[i] = T(0);\n      NTT::ntt(x);\n      for(int i = 0;\
    \ i < 2 * m; ++i) x[i] *= z2[i];\n      NTT::intt(x);\n      x.pop_back();\n \
    \     inplace_integral(x);\n      for(int i = m; i < min< int >(this->size(),\
    \ 2 * m); ++i) x[i] += (*this)[i];\n      fill(begin(x), begin(x) + m, T(0));\n\
    \      NTT::ntt(x);\n      for(int i = 0; i < 2 * m; ++i) x[i] *= y[i];\n    \
    \  NTT::intt(x);\n      b.insert(end(b), begin(x) + m, end(x));\n    }\n    return\
    \ P{begin(b), begin(b) + deg};\n  }\n\n  // https://judge.yosupo.jp/problem/pow_of_formal_power_series\n\
    \  P pow(int64_t k, int deg = -1) const {\n    const int n = (int) this->size();\n\
    \    if(deg == -1) deg = n;\n    for(int i = 0; i < n; i++) {\n      if((*this)[i]\
    \ != T(0)) {\n        T rev = T(1) / (*this)[i];\n        P ret = (((*this * rev)\
    \ >> i).log() * k).exp() * ((*this)[i].pow(k));\n        if(i * k > deg) return\
    \ P(deg, T(0));\n        ret = (ret << (i * k)).pre(deg);\n        if(ret.size()\
    \ < deg) ret.resize(deg, T(0));\n        return ret;\n      }\n    }\n    return\
    \ *this;\n  }\n\n  P mod_pow(int64_t k, P g) const {\n    P modinv = g.rev().inv();\n\
    \    auto get_div = [&](P base) {\n      if(base.size() < g.size()) {\n      \
    \  base.clear();\n        return base;\n      }\n      int n = base.size() - g.size()\
    \ + 1;\n      return (base.rev().pre(n) * modinv.pre(n)).pre(n).rev(n);\n    };\n\
    \    P x(*this), ret{1};\n    while(k > 0) {\n      if(k & 1) {\n        ret *=\
    \ x;\n        ret -= get_div(ret) * g;\n      }\n      x *= x;\n      x -= get_div(x)\
    \ * g;\n      k >>= 1;\n    }\n    return ret;\n  }\n\n  // https://judge.yosupo.jp/problem/polynomial_taylor_shift\n\
    \  P taylor_shift(T c) const {\n    int n = (int) this->size();\n    vector< T\
    \ > fact(n), rfact(n);\n    fact[0] = rfact[0] = T(1);\n    for(int i = 1; i <\
    \ n; i++) fact[i] = fact[i - 1] * T(i);\n    rfact[n - 1] = T(1) / fact[n - 1];\n\
    \    for(int i = n - 1; i > 1; i--) rfact[i - 1] = rfact[i] * T(i);\n    P p(*this);\n\
    \    for(int i = 0; i < n; i++) p[i] *= fact[i];\n    p = p.rev();\n    P bs(n,\
    \ T(1));\n    for(int i = 1; i < n; i++) bs[i] = bs[i - 1] * c * rfact[i] * fact[i\
    \ - 1];\n    p = (p * bs).pre(n);\n    p = p.rev();\n    for(int i = 0; i < n;\
    \ i++) p[i] *= rfact[i];\n    return p;\n  }\n};\n\ntemplate< typename Mint >\n\
    using FPS = FormalPowerSeriesFriendlyNTT< Mint >;\n"
  code: "/**\n * @brief Formal-Power-Series-Friendly-NTT(NTTmod\u7528\u5F62\u5F0F\u7684\
    \u51AA\u7D1A\u6570)\n */\ntemplate< typename T >\nstruct FormalPowerSeriesFriendlyNTT\
    \ : vector< T > {\n  using vector< T >::vector;\n  using P = FormalPowerSeriesFriendlyNTT;\n\
    \  using NTT = NumberTheoreticTransformFriendlyModInt< T >;\n\n  P pre(int deg)\
    \ const {\n    return P(begin(*this), begin(*this) + min((int) this->size(), deg));\n\
    \  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n    if(deg != -1) ret.resize(deg,\
    \ T(0));\n    reverse(begin(ret), end(ret));\n    return ret;\n  }\n\n  void shrink()\
    \ {\n    while(this->size() && this->back() == T(0)) this->pop_back();\n  }\n\n\
    \  P operator+(const P &r) const { return P(*this) += r; }\n\n  P operator+(const\
    \ T &v) const { return P(*this) += v; }\n\n  P operator-(const P &r) const { return\
    \ P(*this) -= r; }\n\n  P operator-(const T &v) const { return P(*this) -= v;\
    \ }\n\n  P operator*(const P &r) const { return P(*this) *= r; }\n\n  P operator*(const\
    \ T &v) const { return P(*this) *= v; }\n\n  P operator/(const P &r) const { return\
    \ P(*this) /= r; }\n\n  P operator%(const P &r) const { return P(*this) %= r;\
    \ }\n\n  P &operator+=(const P &r) {\n    if(r.size() > this->size()) this->resize(r.size());\n\
    \    for(int i = 0; i < r.size(); i++) (*this)[i] += r[i];\n    return *this;\n\
    \  }\n\n  P &operator-=(const P &r) {\n    if(r.size() > this->size()) this->resize(r.size());\n\
    \    for(int i = 0; i < r.size(); i++) (*this)[i] -= r[i];\n    return *this;\n\
    \  }\n\n  // https://judge.yosupo.jp/problem/convolution_mod\n  P &operator*=(const\
    \ P &r) {\n    if(this->empty() || r.empty()) {\n      this->clear();\n      return\
    \ *this;\n    }\n    auto ret = NTT::multiply(*this, r);\n    return *this = {begin(ret),\
    \ end(ret)};\n  }\n\n  P &operator/=(const P &r) {\n    if(this->size() < r.size())\
    \ {\n      this->clear();\n      return *this;\n    }\n    int n = this->size()\
    \ - r.size() + 1;\n    return *this = (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n\
    \  }\n\n  P &operator%=(const P &r) {\n    return *this -= *this / r * r;\n  }\n\
    \n  P operator-() const {\n    P ret(this->size());\n    for(int i = 0; i < this->size();\
    \ i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n  P &operator+=(const T\
    \ &r) {\n    if(this->empty()) this->resize(1);\n    (*this)[0] += r;\n    return\
    \ *this;\n  }\n\n  P &operator-=(const T &r) {\n    if(this->empty()) this->resize(1);\n\
    \    (*this)[0] -= r;\n    return *this;\n  }\n\n  P &operator*=(const T &v) {\n\
    \    for(int i = 0; i < this->size(); i++) (*this)[i] *= v;\n    return *this;\n\
    \  }\n\n  P dot(P r) const {\n    P ret(min(this->size(), r.size()));\n    for(int\
    \ i = 0; i < ret.size(); i++) ret[i] = (*this)[i] * r[i];\n    return ret;\n \
    \ }\n\n  P operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n\
    \    P ret(*this);\n    ret.erase(ret.begin(), ret.begin() + sz);\n    return\
    \ ret;\n  }\n\n  P operator<<(int sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(),\
    \ sz, T(0));\n    return ret;\n  }\n\n  T operator()(T x) const {\n    T r = 0,\
    \ w = 1;\n    for(auto &v : *this) {\n      r += w * v;\n      w *= x;\n    }\n\
    \    return r;\n  }\n\n  P diff() const {\n    const int n = (int) this->size();\n\
    \    P ret(max(0, n - 1));\n    for(int i = 1; i < n; i++) ret[i - 1] = (*this)[i]\
    \ * T(i);\n    return ret;\n  }\n\n  P integral() const {\n    const int n = (int)\
    \ this->size();\n    P ret(n + 1);\n    ret[0] = T(0);\n    for(int i = 0; i <\
    \ n; i++) ret[i + 1] = (*this)[i] / T(i + 1);\n    return ret;\n  }\n\n  // https://judge.yosupo.jp/problem/inv_of_formal_power_series\n\
    \  // F(0) must not be 0\n  P inv(int deg = -1) const {\n    assert(((*this)[0])\
    \ != T(0));\n    const int n = (int) this->size();\n    if(deg == -1) deg = n;\n\
    \n    P res(deg);\n    res[0] = {T(1) / (*this)[0]};\n    for(int d = 1; d < n;\
    \ d <<= 1) {\n      P f(2 * d), g(2 * d);\n      for(int j = 0; j < min(n, 2 *\
    \ d); j++) f[j] = (*this)[j];\n      for(int j = 0; j < d; j++) g[j] = res[j];\n\
    \      NTT::ntt(f);\n      NTT::ntt(g);\n      f = f.dot(g);\n      NTT::intt(f);\n\
    \      for(int j = 0; j < d; j++) f[j] = 0;\n      NTT::ntt(f);\n      for(int\
    \ j = 0; j < 2 * d; j++) f[j] *= g[j];\n      NTT::intt(f);\n      for(int j =\
    \ d; j < min(2 * d, deg); j++) res[j] = -f[j];\n    }\n    return res;\n  }\n\n\
    \  // https://judge.yosupo.jp/problem/log_of_formal_power_series\n  // F(0) must\
    \ be 1\n  P log(int deg = -1) const {\n    assert((*this)[0] == T(1));\n    const\
    \ int n = (int) this->size();\n    if(deg == -1) deg = n;\n    return (this->diff()\
    \ * this->inv(deg)).pre(deg - 1).integral();\n  }\n\n  // https://judge.yosupo.jp/problem/sqrt_of_formal_power_series\n\
    \  P sqrt(int deg = -1, const function< T(T) > &get_sqrt = [](T) { return T(1);\
    \ }) const {\n    const int n = (int) this->size();\n    if(deg == -1) deg = n;\n\
    \    if((*this)[0] == T(0)) {\n      for(int i = 1; i < n; i++) {\n        if((*this)[i]\
    \ != T(0)) {\n          if(i & 1) return {};\n          if(deg - i / 2 <= 0) break;\n\
    \          auto ret = (*this >> i).sqrt(deg - i / 2, get_sqrt);\n          if(ret.empty())\
    \ return {};\n          ret = ret << (i / 2);\n          if(ret.size() < deg)\
    \ ret.resize(deg, T(0));\n          return ret;\n        }\n      }\n      return\
    \ P(deg, 0);\n    }\n    auto sqr = T(get_sqrt((*this)[0]));\n    if(sqr * sqr\
    \ != (*this)[0]) return {};\n    P ret{sqr};\n    T inv2 = T(1) / T(2);\n    for(int\
    \ i = 1; i < deg; i <<= 1) {\n      ret = (ret + pre(i << 1) * ret.inv(i << 1))\
    \ * inv2;\n    }\n    return ret.pre(deg);\n  }\n\n  P sqrt(const function< T(T)\
    \ > &get_sqrt, int deg = -1) const {\n    return sqrt(deg, get_sqrt);\n  }\n\n\
    \  // https://judge.yosupo.jp/problem/exp_of_formal_power_series\n  // F(0) must\
    \ be 0\n  P exp(int deg = -1) const {\n    if(deg == -1) deg = this->size();\n\
    \    assert((*this)[0] == T(0));\n\n    P inv;\n    inv.reserve(deg + 1);\n  \
    \  inv.push_back(T(0));\n    inv.push_back(T(1));\n\n    auto inplace_integral\
    \ = [&](P &F) -> void {\n      const int n = (int) F.size();\n      auto mod =\
    \ T::get_mod();\n      while((int) inv.size() <= n) {\n        int i = inv.size();\n\
    \        inv.push_back((-inv[mod % i]) * (mod / i));\n      }\n      F.insert(begin(F),\
    \ T(0));\n      for(int i = 1; i <= n; i++) F[i] *= inv[i];\n    };\n\n    auto\
    \ inplace_diff = [](P &F) -> void {\n      if(F.empty()) return;\n      F.erase(begin(F));\n\
    \      T coeff = 1, one = 1;\n      for(int i = 0; i < (int) F.size(); i++) {\n\
    \        F[i] *= coeff;\n        coeff += one;\n      }\n    };\n\n    P b{1,\
    \ 1 < (int) this->size() ? (*this)[1] : 0}, c{1}, z1, z2{1, 1};\n    for(int m\
    \ = 2; m < deg; m *= 2) {\n      auto y = b;\n      y.resize(2 * m);\n      NTT::ntt(y);\n\
    \      z1 = z2;\n      P z(m);\n      for(int i = 0; i < m; ++i) z[i] = y[i] *\
    \ z1[i];\n      NTT::intt(z);\n      fill(begin(z), begin(z) + m / 2, T(0));\n\
    \      NTT::ntt(z);\n      for(int i = 0; i < m; ++i) z[i] *= -z1[i];\n      NTT::intt(z);\n\
    \      c.insert(end(c), begin(z) + m / 2, end(z));\n      z2 = c;\n      z2.resize(2\
    \ * m);\n      NTT::ntt(z2);\n      P x(begin(*this), begin(*this) + min< int\
    \ >(this->size(), m));\n      inplace_diff(x);\n      x.push_back(T(0));\n   \
    \   NTT::ntt(x);\n      for(int i = 0; i < m; ++i) x[i] *= y[i];\n      NTT::intt(x);\n\
    \      x -= b.diff();\n      x.resize(2 * m);\n      for(int i = 0; i < m - 1;\
    \ ++i) x[m + i] = x[i], x[i] = T(0);\n      NTT::ntt(x);\n      for(int i = 0;\
    \ i < 2 * m; ++i) x[i] *= z2[i];\n      NTT::intt(x);\n      x.pop_back();\n \
    \     inplace_integral(x);\n      for(int i = m; i < min< int >(this->size(),\
    \ 2 * m); ++i) x[i] += (*this)[i];\n      fill(begin(x), begin(x) + m, T(0));\n\
    \      NTT::ntt(x);\n      for(int i = 0; i < 2 * m; ++i) x[i] *= y[i];\n    \
    \  NTT::intt(x);\n      b.insert(end(b), begin(x) + m, end(x));\n    }\n    return\
    \ P{begin(b), begin(b) + deg};\n  }\n\n  // https://judge.yosupo.jp/problem/pow_of_formal_power_series\n\
    \  P pow(int64_t k, int deg = -1) const {\n    const int n = (int) this->size();\n\
    \    if(deg == -1) deg = n;\n    for(int i = 0; i < n; i++) {\n      if((*this)[i]\
    \ != T(0)) {\n        T rev = T(1) / (*this)[i];\n        P ret = (((*this * rev)\
    \ >> i).log() * k).exp() * ((*this)[i].pow(k));\n        if(i * k > deg) return\
    \ P(deg, T(0));\n        ret = (ret << (i * k)).pre(deg);\n        if(ret.size()\
    \ < deg) ret.resize(deg, T(0));\n        return ret;\n      }\n    }\n    return\
    \ *this;\n  }\n\n  P mod_pow(int64_t k, P g) const {\n    P modinv = g.rev().inv();\n\
    \    auto get_div = [&](P base) {\n      if(base.size() < g.size()) {\n      \
    \  base.clear();\n        return base;\n      }\n      int n = base.size() - g.size()\
    \ + 1;\n      return (base.rev().pre(n) * modinv.pre(n)).pre(n).rev(n);\n    };\n\
    \    P x(*this), ret{1};\n    while(k > 0) {\n      if(k & 1) {\n        ret *=\
    \ x;\n        ret -= get_div(ret) * g;\n      }\n      x *= x;\n      x -= get_div(x)\
    \ * g;\n      k >>= 1;\n    }\n    return ret;\n  }\n\n  // https://judge.yosupo.jp/problem/polynomial_taylor_shift\n\
    \  P taylor_shift(T c) const {\n    int n = (int) this->size();\n    vector< T\
    \ > fact(n), rfact(n);\n    fact[0] = rfact[0] = T(1);\n    for(int i = 1; i <\
    \ n; i++) fact[i] = fact[i - 1] * T(i);\n    rfact[n - 1] = T(1) / fact[n - 1];\n\
    \    for(int i = n - 1; i > 1; i--) rfact[i - 1] = rfact[i] * T(i);\n    P p(*this);\n\
    \    for(int i = 0; i < n; i++) p[i] *= fact[i];\n    p = p.rev();\n    P bs(n,\
    \ T(1));\n    for(int i = 1; i < n; i++) bs[i] = bs[i - 1] * c * rfact[i] * fact[i\
    \ - 1];\n    p = (p * bs).pre(n);\n    p = p.rev();\n    for(int i = 0; i < n;\
    \ i++) p[i] *= rfact[i];\n    return p;\n  }\n};\n\ntemplate< typename Mint >\n\
    using FPS = FormalPowerSeriesFriendlyNTT< Mint >;\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/formal-power-series-friendly-ntt.cpp
  requiredBy: []
  timestamp: '2021-06-27 01:10:39+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/formal-power-series-friendly-ntt.cpp
layout: document
redirect_from:
- /library/math/fps/formal-power-series-friendly-ntt.cpp
- /library/math/fps/formal-power-series-friendly-ntt.cpp.html
title: "Formal-Power-Series-Friendly-NTT(NTTmod\u7528\u5F62\u5F0F\u7684\u51AA\u7D1A\
  \u6570)"
---
