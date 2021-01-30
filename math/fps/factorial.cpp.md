---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/fps/factorial.cpp\"\ntemplate< typename T >\nT factorial(int64_t\
    \ n) {\n  if(n >= T::get_mod()) return 0;\n  if(n == 0) return 1;\n\n  const int64_t\
    \ sn = sqrt(n);\n  const T sn_inv = T(1) / sn;\n\n  Combination< modint > comb(sn);\n\
    \  using P = vector< T >;\n\n  ArbitraryModConvolution< T > fft;\n  using FPS\
    \ = FormalPowerSeries< T >;\n  auto mult = [&](const typename FPS::P &a, const\
    \ typename FPS::P &b) {\n    auto ret = fft.multiply(a, b);\n    return typename\
    \ FPS::P(ret.begin(), ret.end());\n  };\n  FPS::set_fft(mult);\n\n\n  auto shift\
    \ = [&](const P &f, T dx) {\n    int n = (int) f.size();\n    T a = dx * sn_inv;\n\
    \    auto p1 = P(f);\n    for(int i = 0; i < n; i++) {\n      T d = comb.rfact(i)\
    \ * comb.rfact((n - 1) - i);\n      if(((n - 1 - i) & 1)) d = -d;\n      p1[i]\
    \ *= d;\n    }\n    auto p2 = P(2 * n);\n    for(int i = 0; i < p2.size(); i++)\
    \ {\n      p2[i] = (a.x + i - n) <= 0 ? 1 : a + i - n;\n    }\n    for(int i =\
    \ 1; i < p2.size(); i++) {\n      p2[i] *= p2[i - 1];\n    }\n    T prod = p2[2\
    \ * n - 1];\n    T prod_inv = T(1) / prod;\n    for(int i = 2 * n - 1; i > 0;\
    \ --i) {\n      p2[i] = prod_inv * p2[i - 1];\n      prod_inv *= a + i - n;\n\
    \    }\n    p2[0] = prod_inv;\n    auto p3 = fft.multiply(p1, p2, (int) p2.size());\n\
    \    p1 = P(p3.begin() + p1.size(), p3.begin() + p2.size());\n    prod = 1;\n\
    \    for(int i = 0; i < n; i++) {\n      prod *= a + n - 1 - i;\n    }\n    for(int\
    \ i = n - 1; i >= 0; --i) {\n      p1[i] *= prod;\n      prod *= p2[n + i] * (a\
    \ + i - n);\n    }\n    return p1;\n  };\n  function< P(int) > rec = [&](int64_t\
    \ n) {\n    if(n == 1) return P({1, 1 + sn});\n    int64_t nh = n >> 1;\n    auto\
    \ a1 = rec(nh);\n    auto a2 = shift(a1, nh);\n    auto b1 = shift(a1, sn * nh);\n\
    \    auto b2 = shift(a1, sn * nh + nh);\n    for(int i = 0; i <= nh; i++) a1[i]\
    \ *= a2[i];\n    for(int i = 1; i <= nh; i++) a1.emplace_back(b1[i] * b2[i]);\n\
    \    if(n & 1) {\n      for(int64_t i = 0; i < n; i++) {\n        a1[i] *= n +\
    \ 1LL * sn * i;\n      }\n      T prod = 1;\n      for(int64_t i = 1LL * n * sn;\
    \ i < 1LL * n * sn + n; i++) {\n        prod *= (i + 1);\n      }\n      a1.push_back(prod);\n\
    \    }\n    return a1;\n  };\n  auto vs = rec(sn);\n  T ret = 1;\n  for(int64_t\
    \ i = 0; i < sn; i++) ret *= vs[i];\n  for(int64_t i = 1LL * sn * sn + 1; i <=\
    \ n; i++) ret *= i;\n  return ret;\n}\n"
  code: "template< typename T >\nT factorial(int64_t n) {\n  if(n >= T::get_mod())\
    \ return 0;\n  if(n == 0) return 1;\n\n  const int64_t sn = sqrt(n);\n  const\
    \ T sn_inv = T(1) / sn;\n\n  Combination< modint > comb(sn);\n  using P = vector<\
    \ T >;\n\n  ArbitraryModConvolution< T > fft;\n  using FPS = FormalPowerSeries<\
    \ T >;\n  auto mult = [&](const typename FPS::P &a, const typename FPS::P &b)\
    \ {\n    auto ret = fft.multiply(a, b);\n    return typename FPS::P(ret.begin(),\
    \ ret.end());\n  };\n  FPS::set_fft(mult);\n\n\n  auto shift = [&](const P &f,\
    \ T dx) {\n    int n = (int) f.size();\n    T a = dx * sn_inv;\n    auto p1 =\
    \ P(f);\n    for(int i = 0; i < n; i++) {\n      T d = comb.rfact(i) * comb.rfact((n\
    \ - 1) - i);\n      if(((n - 1 - i) & 1)) d = -d;\n      p1[i] *= d;\n    }\n\
    \    auto p2 = P(2 * n);\n    for(int i = 0; i < p2.size(); i++) {\n      p2[i]\
    \ = (a.x + i - n) <= 0 ? 1 : a + i - n;\n    }\n    for(int i = 1; i < p2.size();\
    \ i++) {\n      p2[i] *= p2[i - 1];\n    }\n    T prod = p2[2 * n - 1];\n    T\
    \ prod_inv = T(1) / prod;\n    for(int i = 2 * n - 1; i > 0; --i) {\n      p2[i]\
    \ = prod_inv * p2[i - 1];\n      prod_inv *= a + i - n;\n    }\n    p2[0] = prod_inv;\n\
    \    auto p3 = fft.multiply(p1, p2, (int) p2.size());\n    p1 = P(p3.begin() +\
    \ p1.size(), p3.begin() + p2.size());\n    prod = 1;\n    for(int i = 0; i < n;\
    \ i++) {\n      prod *= a + n - 1 - i;\n    }\n    for(int i = n - 1; i >= 0;\
    \ --i) {\n      p1[i] *= prod;\n      prod *= p2[n + i] * (a + i - n);\n    }\n\
    \    return p1;\n  };\n  function< P(int) > rec = [&](int64_t n) {\n    if(n ==\
    \ 1) return P({1, 1 + sn});\n    int64_t nh = n >> 1;\n    auto a1 = rec(nh);\n\
    \    auto a2 = shift(a1, nh);\n    auto b1 = shift(a1, sn * nh);\n    auto b2\
    \ = shift(a1, sn * nh + nh);\n    for(int i = 0; i <= nh; i++) a1[i] *= a2[i];\n\
    \    for(int i = 1; i <= nh; i++) a1.emplace_back(b1[i] * b2[i]);\n    if(n &\
    \ 1) {\n      for(int64_t i = 0; i < n; i++) {\n        a1[i] *= n + 1LL * sn\
    \ * i;\n      }\n      T prod = 1;\n      for(int64_t i = 1LL * n * sn; i < 1LL\
    \ * n * sn + n; i++) {\n        prod *= (i + 1);\n      }\n      a1.push_back(prod);\n\
    \    }\n    return a1;\n  };\n  auto vs = rec(sn);\n  T ret = 1;\n  for(int64_t\
    \ i = 0; i < sn; i++) ret *= vs[i];\n  for(int64_t i = 1LL * sn * sn + 1; i <=\
    \ n; i++) ret *= i;\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/factorial.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/factorial.cpp
layout: document
redirect_from:
- /library/math/fps/factorial.cpp
- /library/math/fps/factorial.cpp.html
title: math/fps/factorial.cpp
---
