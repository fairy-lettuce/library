---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: math/fps/diff.cpp
    title: Diff $f'(x)$
  - icon: ':heavy_check_mark:'
    path: math/fps/exp.cpp
    title: Exp $e^{f(x)}$
  - icon: ':heavy_check_mark:'
    path: math/fps/integral.cpp
    title: Integral $\int f(x) dx$
  - icon: ':heavy_check_mark:'
    path: math/fps/inv.cpp
    title: Inv $\frac {1} {f(x)}$
  - icon: ':heavy_check_mark:'
    path: math/fps/log.cpp
    title: Log $\log {f(x)}$
  - icon: ':heavy_check_mark:'
    path: math/fps/sqrt.cpp
    title: Sqrt $\sqrt {f(x)}$
  _extendedVerifiedWith:
  - icon: ':x:'
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
  - icon: ':x:'
    path: test/verify/yosupo-multipoint-evaluation.test.cpp
    title: test/verify/yosupo-multipoint-evaluation.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-partition-function.test.cpp
    title: test/verify/yosupo-partition-function.test.cpp
  - icon: ':x:'
    path: test/verify/yosupo-polynomial-interpolation.test.cpp
    title: test/verify/yosupo-polynomial-interpolation.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sparse-matrix-det.test.cpp
    title: test/verify/yosupo-sparse-matrix-det.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
    title: test/verify/yosupo-sqrt-of-formal-power-series.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':question:'
  attributes:
    document_title: "Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\u7D1A\u6570)"
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
    \  }\n\n  P &operator%=(const P &r) {\n    return *this -= *this / r * r;\n  }\n\
    \n  P operator-() const {\n    P ret(this->size());\n    for(int i = 0; i < this->size();\
    \ i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n  P &operator/=(const P\
    \ &r) {\n    if(this->size() < r.size()) {\n      this->clear();\n      return\
    \ *this;\n    }\n    int n = this->size() - r.size() + 1;\n    return *this =\
    \ (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n  }\n\n  P dot(P r) const {\n\
    \    P ret(min(this->size(), r.size()));\n    for(int i = 0; i < ret.size(); i++)\
    \ ret[i] = (*this)[i] * r[i];\n    return ret;\n  }\n\n  P pre(int sz) const {\n\
    \    return P(begin(*this), begin(*this) + min((int) this->size(), sz));\n  }\n\
    \n  P operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n    P\
    \ ret(*this);\n    ret.erase(ret.begin(), ret.begin() + sz);\n    return ret;\n\
    \  }\n\n  P operator<<(int sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(),\
    \ sz, T(0));\n    return ret;\n  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n\
    \    if(deg != -1) ret.resize(deg, T(0));\n    reverse(begin(ret), end(ret));\n\
    \    return ret;\n  }\n\n  P diff() const;\n\n  P integral() const;\n\n  // F(0)\
    \ must not be 0\n  P inv_fast() const;\n\n  P inv(int deg = -1) const;\n\n  //\
    \ F(0) must be 1\n  P log(int deg = -1) const;\n\n  P sqrt(int deg = -1) const;\n\
    \  \n  // F(0) must be 0\n  P exp_fast(int deg = -1) const;\n\n  P exp(int deg\
    \ = -1) const;\n\n  P pow(int64_t k, int deg = -1) const {\n    const int n =\
    \ (int) this->size();\n    if(deg == -1) deg = n;\n    for(int i = 0; i < n; i++)\
    \ {\n      if((*this)[i] != T(0)) {\n        T rev = T(1) / (*this)[i];\n    \
    \    P ret = (((*this * rev) >> i).log() * k).exp() * ((*this)[i].pow(k));\n \
    \       if(i * k > deg) return P(deg, T(0));\n        ret = (ret << (i * k)).pre(deg);\n\
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
  code: "#pragma once\n\n/**\n * @brief Formal-Power-Series(\u5F62\u5F0F\u7684\u51AA\
    \u7D1A\u6570)\n */\ntemplate< typename T >\nstruct FormalPowerSeries : vector<\
    \ T > {\n  using vector< T >::vector;\n  using P = FormalPowerSeries;\n\n  using\
    \ MULT = function< vector< T >(P, P) >;\n  using FFT = function< void(P &) >;\n\
    \  using SQRT = function< T(T) >;\n\n  static MULT &get_mult() {\n    static MULT\
    \ mult = nullptr;\n    return mult;\n  }\n\n  static void set_mult(MULT f) {\n\
    \    get_mult() = f;\n  }\n\n  static FFT &get_fft() {\n    static FFT fft = nullptr;\n\
    \    return fft;\n  }\n\n  static FFT &get_ifft() {\n    static FFT ifft = nullptr;\n\
    \    return ifft;\n  }\n\n  static void set_fft(FFT f, FFT g) {\n    get_fft()\
    \ = f;\n    get_ifft() = g;\n  }\n\n  static SQRT &get_sqrt() {\n    static SQRT\
    \ sqr = nullptr;\n    return sqr;\n  }\n\n  static void set_sqrt(SQRT sqr) {\n\
    \    get_sqrt() = sqr;\n  }\n\n  void shrink() {\n    while(this->size() && this->back()\
    \ == T(0)) this->pop_back();\n  }\n\n  P operator+(const P &r) const { return\
    \ P(*this) += r; }\n\n  P operator+(const T &v) const { return P(*this) += v;\
    \ }\n\n  P operator-(const P &r) const { return P(*this) -= r; }\n\n  P operator-(const\
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
    \  }\n\n  P &operator%=(const P &r) {\n    return *this -= *this / r * r;\n  }\n\
    \n  P operator-() const {\n    P ret(this->size());\n    for(int i = 0; i < this->size();\
    \ i++) ret[i] = -(*this)[i];\n    return ret;\n  }\n\n  P &operator/=(const P\
    \ &r) {\n    if(this->size() < r.size()) {\n      this->clear();\n      return\
    \ *this;\n    }\n    int n = this->size() - r.size() + 1;\n    return *this =\
    \ (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);\n  }\n\n  P dot(P r) const {\n\
    \    P ret(min(this->size(), r.size()));\n    for(int i = 0; i < ret.size(); i++)\
    \ ret[i] = (*this)[i] * r[i];\n    return ret;\n  }\n\n  P pre(int sz) const {\n\
    \    return P(begin(*this), begin(*this) + min((int) this->size(), sz));\n  }\n\
    \n  P operator>>(int sz) const {\n    if(this->size() <= sz) return {};\n    P\
    \ ret(*this);\n    ret.erase(ret.begin(), ret.begin() + sz);\n    return ret;\n\
    \  }\n\n  P operator<<(int sz) const {\n    P ret(*this);\n    ret.insert(ret.begin(),\
    \ sz, T(0));\n    return ret;\n  }\n\n  P rev(int deg = -1) const {\n    P ret(*this);\n\
    \    if(deg != -1) ret.resize(deg, T(0));\n    reverse(begin(ret), end(ret));\n\
    \    return ret;\n  }\n\n  P diff() const;\n\n  P integral() const;\n\n  // F(0)\
    \ must not be 0\n  P inv_fast() const;\n\n  P inv(int deg = -1) const;\n\n  //\
    \ F(0) must be 1\n  P log(int deg = -1) const;\n\n  P sqrt(int deg = -1) const;\n\
    \  \n  // F(0) must be 0\n  P exp_fast(int deg = -1) const;\n\n  P exp(int deg\
    \ = -1) const;\n\n  P pow(int64_t k, int deg = -1) const {\n    const int n =\
    \ (int) this->size();\n    if(deg == -1) deg = n;\n    for(int i = 0; i < n; i++)\
    \ {\n      if((*this)[i] != T(0)) {\n        T rev = T(1) / (*this)[i];\n    \
    \    P ret = (((*this * rev) >> i).log() * k).exp() * ((*this)[i].pow(k));\n \
    \       if(i * k > deg) return P(deg, T(0));\n        ret = (ret << (i * k)).pre(deg);\n\
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
  requiredBy:
  - math/fps/log.cpp
  - math/fps/exp.cpp
  - math/fps/integral.cpp
  - math/fps/inv.cpp
  - math/fps/sqrt.cpp
  - math/fps/diff.cpp
  timestamp: '2020-10-21 02:08:50+09:00'
  verificationStatus: LIBRARY_SOME_WA
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
