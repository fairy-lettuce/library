---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/combinatorics/mod-int-2.cpp\"\nstatic constexpr uint32_t\
    \ mul_inv(uint32_t n, int e = 5, uint32_t x = 1) {\n  return e == 0 ? x : mul_inv(n,\
    \ e - 1, x * (2 - x * n));\n}\n\ntemplate< uint32_t mod, bool fast = false >\n\
    struct ModInt2 {\n  using u32 = uint32_t;\n  using u64 = uint64_t;\n\n  static\
    \ constexpr u32 inv = mul_inv(mod);\n  static constexpr u32 r2 = -uint64_t(mod)\
    \ % mod;\n\n  uint32_t x;\n\n  ModInt2() : x(0) {}\n\n  ModInt2(const int64_t\
    \ &y)\n      : x(reduce(u64(fast ? y : (y >= 0 ? y % mod : (mod - (-y) % mod)\
    \ % mod)) * r2)) {}\n\n  u32 reduce(const u64 &w) const {\n    return u32(w >>\
    \ 32) + mod - u32((u64(u32(w) * inv) * mod) >> 32);\n  }\n\n  ModInt2 &operator+=(const\
    \ ModInt2 &p) {\n    if(int(x += p.x - 2 * mod) < 0) x += 2 * mod;\n    return\
    \ *this;\n  }\n\n  ModInt2 &operator-=(const ModInt2 &p) {\n    if(int(x -= p.x)\
    \ < 0) x += 2 * mod;\n    return *this;\n  }\n\n  ModInt2 &operator*=(const ModInt2\
    \ &p) {\n    x = reduce(uint64_t(x) * p.x);\n    return *this;\n  }\n\n  ModInt2\
    \ &operator/=(const ModInt2 &p) {\n    *this *= p.inverse();\n    return *this;\n\
    \  }\n\n  ModInt2 operator-() const { return ModInt2() - *this; }\n\n  ModInt2\
    \ operator+(const ModInt2 &p) const { return ModInt2(*this) += p; }\n\n  ModInt2\
    \ operator-(const ModInt2 &p) const { return ModInt2(*this) -= p; }\n\n  ModInt2\
    \ operator*(const ModInt2 &p) const { return ModInt2(*this) *= p; }\n\n  ModInt2\
    \ operator/(const ModInt2 &p) const { return ModInt2(*this) /= p; }\n\n  bool\
    \ operator==(const ModInt2 &p) const { return get() == p.get(); }\n\n  bool operator!=(const\
    \ ModInt2 &p) const { return get() != p.get(); }\n\n  int get() const { return\
    \ reduce(x) % mod; }\n\n  ModInt2 pow(int64_t n) const {\n    ModInt2 ret(1),\
    \ mul(*this);\n    while(n > 0) {\n      if(n & 1) ret *= mul;\n      mul *= mul;\n\
    \      n >>= 1;\n    }\n    return ret;\n  }\n\n  ModInt2 inverse() const {\n\
    \    return pow(mod - 2);\n  }\n\n  friend ostream &operator<<(ostream &os, const\
    \ ModInt2 &p) {\n    return os << p.get();\n  }\n\n  friend istream &operator>>(istream\
    \ &is, ModInt2 &a) {\n    int64_t t;\n    is >> t;\n    a = ModInt2< mod, fast\
    \ >(t);\n    return (is);\n  }\n\n  static int get_mod() { return mod; }\n};\n\
    \nusing modint = ModInt2< mod >;\n"
  code: "static constexpr uint32_t mul_inv(uint32_t n, int e = 5, uint32_t x = 1)\
    \ {\n  return e == 0 ? x : mul_inv(n, e - 1, x * (2 - x * n));\n}\n\ntemplate<\
    \ uint32_t mod, bool fast = false >\nstruct ModInt2 {\n  using u32 = uint32_t;\n\
    \  using u64 = uint64_t;\n\n  static constexpr u32 inv = mul_inv(mod);\n  static\
    \ constexpr u32 r2 = -uint64_t(mod) % mod;\n\n  uint32_t x;\n\n  ModInt2() : x(0)\
    \ {}\n\n  ModInt2(const int64_t &y)\n      : x(reduce(u64(fast ? y : (y >= 0 ?\
    \ y % mod : (mod - (-y) % mod) % mod)) * r2)) {}\n\n  u32 reduce(const u64 &w)\
    \ const {\n    return u32(w >> 32) + mod - u32((u64(u32(w) * inv) * mod) >> 32);\n\
    \  }\n\n  ModInt2 &operator+=(const ModInt2 &p) {\n    if(int(x += p.x - 2 * mod)\
    \ < 0) x += 2 * mod;\n    return *this;\n  }\n\n  ModInt2 &operator-=(const ModInt2\
    \ &p) {\n    if(int(x -= p.x) < 0) x += 2 * mod;\n    return *this;\n  }\n\n \
    \ ModInt2 &operator*=(const ModInt2 &p) {\n    x = reduce(uint64_t(x) * p.x);\n\
    \    return *this;\n  }\n\n  ModInt2 &operator/=(const ModInt2 &p) {\n    *this\
    \ *= p.inverse();\n    return *this;\n  }\n\n  ModInt2 operator-() const { return\
    \ ModInt2() - *this; }\n\n  ModInt2 operator+(const ModInt2 &p) const { return\
    \ ModInt2(*this) += p; }\n\n  ModInt2 operator-(const ModInt2 &p) const { return\
    \ ModInt2(*this) -= p; }\n\n  ModInt2 operator*(const ModInt2 &p) const { return\
    \ ModInt2(*this) *= p; }\n\n  ModInt2 operator/(const ModInt2 &p) const { return\
    \ ModInt2(*this) /= p; }\n\n  bool operator==(const ModInt2 &p) const { return\
    \ get() == p.get(); }\n\n  bool operator!=(const ModInt2 &p) const { return get()\
    \ != p.get(); }\n\n  int get() const { return reduce(x) % mod; }\n\n  ModInt2\
    \ pow(int64_t n) const {\n    ModInt2 ret(1), mul(*this);\n    while(n > 0) {\n\
    \      if(n & 1) ret *= mul;\n      mul *= mul;\n      n >>= 1;\n    }\n    return\
    \ ret;\n  }\n\n  ModInt2 inverse() const {\n    return pow(mod - 2);\n  }\n\n\
    \  friend ostream &operator<<(ostream &os, const ModInt2 &p) {\n    return os\
    \ << p.get();\n  }\n\n  friend istream &operator>>(istream &is, ModInt2 &a) {\n\
    \    int64_t t;\n    is >> t;\n    a = ModInt2< mod, fast >(t);\n    return (is);\n\
    \  }\n\n  static int get_mod() { return mod; }\n};\n\nusing modint = ModInt2<\
    \ mod >;\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/mod-int-2.cpp
  requiredBy: []
  timestamp: '2020-01-22 22:52:06+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/mod-int-2.cpp
layout: document
redirect_from:
- /library/math/combinatorics/mod-int-2.cpp
- /library/math/combinatorics/mod-int-2.cpp.html
title: math/combinatorics/mod-int-2.cpp
---
