---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/fps/formal-power-series.cpp
    title: "Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\u7D1A\u6570)"
  - icon: ':heavy_check_mark:'
    path: math/fps/inv.cpp
    title: Inv ($\frac {1} {f(x)}$)
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bellnoulli-number.test.cpp
    title: test/verify/yosupo-bellnoulli-number.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 2 \"math/fps/formal-power-series.cpp\"\n\n/**\n * @brief Formal-Power-Series(\u5F62\
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
    };\n#line 3 \"math/fps/inv.cpp\"\n\n/**\n * @brief Inv ($\\frac {1} {f(x)}$)\n\
    \ */\ntemplate< typename T >\ntypename FormalPowerSeries< T >::P FormalPowerSeries<\
    \ T >::inv_fast() const {\n  assert(((*this)[0]) != T(0));\n\n  const int n =\
    \ (int) this->size();\n  P res{T(1) / (*this)[0]};\n\n  for(int d = 1; d < n;\
    \ d <<= 1) {\n    P f(2 * d), g(2 * d);\n    for(int j = 0; j < min(n, 2 * d);\
    \ j++) f[j] = (*this)[j];\n    for(int j = 0; j < d; j++) g[j] = res[j];\n   \
    \ get_fft()(f);\n    get_fft()(g);\n    for(int j = 0; j < 2 * d; j++) f[j] *=\
    \ g[j];\n    get_ifft()(f);\n    for(int j = 0; j < d; j++) {\n      f[j] = 0;\n\
    \      f[j + d] = -f[j + d];\n    }\n    get_fft()(f);\n    for(int j = 0; j <\
    \ 2 * d; j++) f[j] *= g[j];\n    get_ifft()(f);\n    for(int j = 0; j < d; j++)\
    \ f[j] = res[j];\n    res = f;\n  }\n  return res.pre(n);\n}\n\ntemplate< typename\
    \ T >\ntypename FormalPowerSeries< T >::P FormalPowerSeries< T >::inv(int deg)\
    \ const {\n  assert(((*this)[0]) != T(0));\n  const int n = (int) this->size();\n\
    \  if(deg == -1) deg = n;\n  if(get_fft() != nullptr) {\n    P ret(*this);\n \
    \   ret.resize(deg, T(0));\n    return ret.inv_fast();\n  }\n  P ret({T(1) / (*this)[0]});\n\
    \  for(int i = 1; i < deg; i <<= 1) {\n    ret = (ret + ret - ret * ret * pre(i\
    \ << 1)).pre(i << 1);\n  }\n  return ret.pre(deg);\n}\n#line 4 \"math/fps/bellnoulli.cpp\"\
    \n\ntemplate< typename T >\nFormalPowerSeries< T > bellnoulli(int N) {\n  FormalPowerSeries<\
    \ T > poly(N + 1);\n  poly[0] = T(1);\n  for(int i = 1; i <= N; i++) {\n    poly[i]\
    \ = poly[i - 1] / T(i + 1);\n  }\n  poly = poly.inv();\n  T tmp(1);\n  for(int\
    \ i = 1; i <= N; i++) {\n    tmp *= T(i);\n    poly[i] *= tmp;\n  }\n  return\
    \ poly;\n}\n"
  code: "#pragma once\n#include \"formal-power-series.cpp\"\n#include \"inv.cpp\"\n\
    \ntemplate< typename T >\nFormalPowerSeries< T > bellnoulli(int N) {\n  FormalPowerSeries<\
    \ T > poly(N + 1);\n  poly[0] = T(1);\n  for(int i = 1; i <= N; i++) {\n    poly[i]\
    \ = poly[i - 1] / T(i + 1);\n  }\n  poly = poly.inv();\n  T tmp(1);\n  for(int\
    \ i = 1; i <= N; i++) {\n    tmp *= T(i);\n    poly[i] *= tmp;\n  }\n  return\
    \ poly;\n}\n"
  dependsOn:
  - math/fps/formal-power-series.cpp
  - math/fps/inv.cpp
  isVerificationFile: false
  path: math/fps/bellnoulli.cpp
  requiredBy: []
  timestamp: '2020-10-21 14:13:55+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-bellnoulli-number.test.cpp
documentation_of: math/fps/bellnoulli.cpp
layout: document
redirect_from:
- /library/math/fps/bellnoulli.cpp
- /library/math/fps/bellnoulli.cpp.html
title: math/fps/bellnoulli.cpp
---
