---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-montmort-number-mod.test.cpp
    title: test/verify/yosupo-montmort-number-mod.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links: []
  bundledCode: "#line 1 \"math/combinatorics/arbitrary-mod-int.cpp\"\nstruct ArbitraryModInt\
    \ {\n\n  int x;\n\n  ArbitraryModInt() : x(0) {}\n\n  ArbitraryModInt(int64_t\
    \ y) : x(y >= 0 ? y % get_mod() : (get_mod() - (-y) % get_mod()) % get_mod())\
    \ {}\n\n  static int &get_mod() {\n    static int mod = 0;\n    return mod;\n\
    \  }\n\n  static void set_mod(int md) {\n    get_mod() = md;\n  }\n\n  ArbitraryModInt\
    \ &operator+=(const ArbitraryModInt &p) {\n    if((x += p.x) >= get_mod()) x -=\
    \ get_mod();\n    return *this;\n  }\n\n  ArbitraryModInt &operator-=(const ArbitraryModInt\
    \ &p) {\n    if((x += get_mod() - p.x) >= get_mod()) x -= get_mod();\n    return\
    \ *this;\n  }\n\n  ArbitraryModInt &operator*=(const ArbitraryModInt &p) {\n \
    \   unsigned long long a = (unsigned long long) x * p.x;\n    unsigned xh = (unsigned)\
    \ (a >> 32), xl = (unsigned) a, d, m;\n    asm(\"divl %4; \\n\\t\" : \"=a\" (d),\
    \ \"=d\" (m) : \"d\" (xh), \"a\" (xl), \"r\" (get_mod()));\n    x = m;\n    return\
    \ *this;\n  }\n\n  ArbitraryModInt &operator/=(const ArbitraryModInt &p) {\n \
    \   *this *= p.inverse();\n    return *this;\n  }\n\n  ArbitraryModInt operator-()\
    \ const { return ArbitraryModInt(-x); }\n\n  ArbitraryModInt operator+(const ArbitraryModInt\
    \ &p) const { return ArbitraryModInt(*this) += p; }\n\n  ArbitraryModInt operator-(const\
    \ ArbitraryModInt &p) const { return ArbitraryModInt(*this) -= p; }\n\n  ArbitraryModInt\
    \ operator*(const ArbitraryModInt &p) const { return ArbitraryModInt(*this) *=\
    \ p; }\n\n  ArbitraryModInt operator/(const ArbitraryModInt &p) const { return\
    \ ArbitraryModInt(*this) /= p; }\n\n  bool operator==(const ArbitraryModInt &p)\
    \ const { return x == p.x; }\n\n  bool operator!=(const ArbitraryModInt &p) const\
    \ { return x != p.x; }\n\n  ArbitraryModInt inverse() const {\n    int a = x,\
    \ b = get_mod(), u = 1, v = 0, t;\n    while(b > 0) {\n      t = a / b;\n    \
    \  swap(a -= t * b, b);\n      swap(u -= t * v, v);\n    }\n    return ArbitraryModInt(u);\n\
    \  }\n\n  ArbitraryModInt pow(int64_t n) const {\n    ArbitraryModInt ret(1),\
    \ mul(x);\n    while(n > 0) {\n      if(n & 1) ret *= mul;\n      mul *= mul;\n\
    \      n >>= 1;\n    }\n    return ret;\n  }\n\n  friend ostream &operator<<(ostream\
    \ &os, const ArbitraryModInt &p) {\n    return os << p.x;\n  }\n\n  friend istream\
    \ &operator>>(istream &is, ArbitraryModInt &a) {\n    int64_t t;\n    is >> t;\n\
    \    a = ArbitraryModInt(t);\n    return (is);\n  }\n};\n"
  code: "struct ArbitraryModInt {\n\n  int x;\n\n  ArbitraryModInt() : x(0) {}\n\n\
    \  ArbitraryModInt(int64_t y) : x(y >= 0 ? y % get_mod() : (get_mod() - (-y) %\
    \ get_mod()) % get_mod()) {}\n\n  static int &get_mod() {\n    static int mod\
    \ = 0;\n    return mod;\n  }\n\n  static void set_mod(int md) {\n    get_mod()\
    \ = md;\n  }\n\n  ArbitraryModInt &operator+=(const ArbitraryModInt &p) {\n  \
    \  if((x += p.x) >= get_mod()) x -= get_mod();\n    return *this;\n  }\n\n  ArbitraryModInt\
    \ &operator-=(const ArbitraryModInt &p) {\n    if((x += get_mod() - p.x) >= get_mod())\
    \ x -= get_mod();\n    return *this;\n  }\n\n  ArbitraryModInt &operator*=(const\
    \ ArbitraryModInt &p) {\n    unsigned long long a = (unsigned long long) x * p.x;\n\
    \    unsigned xh = (unsigned) (a >> 32), xl = (unsigned) a, d, m;\n    asm(\"\
    divl %4; \\n\\t\" : \"=a\" (d), \"=d\" (m) : \"d\" (xh), \"a\" (xl), \"r\" (get_mod()));\n\
    \    x = m;\n    return *this;\n  }\n\n  ArbitraryModInt &operator/=(const ArbitraryModInt\
    \ &p) {\n    *this *= p.inverse();\n    return *this;\n  }\n\n  ArbitraryModInt\
    \ operator-() const { return ArbitraryModInt(-x); }\n\n  ArbitraryModInt operator+(const\
    \ ArbitraryModInt &p) const { return ArbitraryModInt(*this) += p; }\n\n  ArbitraryModInt\
    \ operator-(const ArbitraryModInt &p) const { return ArbitraryModInt(*this) -=\
    \ p; }\n\n  ArbitraryModInt operator*(const ArbitraryModInt &p) const { return\
    \ ArbitraryModInt(*this) *= p; }\n\n  ArbitraryModInt operator/(const ArbitraryModInt\
    \ &p) const { return ArbitraryModInt(*this) /= p; }\n\n  bool operator==(const\
    \ ArbitraryModInt &p) const { return x == p.x; }\n\n  bool operator!=(const ArbitraryModInt\
    \ &p) const { return x != p.x; }\n\n  ArbitraryModInt inverse() const {\n    int\
    \ a = x, b = get_mod(), u = 1, v = 0, t;\n    while(b > 0) {\n      t = a / b;\n\
    \      swap(a -= t * b, b);\n      swap(u -= t * v, v);\n    }\n    return ArbitraryModInt(u);\n\
    \  }\n\n  ArbitraryModInt pow(int64_t n) const {\n    ArbitraryModInt ret(1),\
    \ mul(x);\n    while(n > 0) {\n      if(n & 1) ret *= mul;\n      mul *= mul;\n\
    \      n >>= 1;\n    }\n    return ret;\n  }\n\n  friend ostream &operator<<(ostream\
    \ &os, const ArbitraryModInt &p) {\n    return os << p.x;\n  }\n\n  friend istream\
    \ &operator>>(istream &is, ArbitraryModInt &a) {\n    int64_t t;\n    is >> t;\n\
    \    a = ArbitraryModInt(t);\n    return (is);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/arbitrary-mod-int.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:37:39+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-montmort-number-mod.test.cpp
documentation_of: math/combinatorics/arbitrary-mod-int.cpp
layout: document
redirect_from:
- /library/math/combinatorics/arbitrary-mod-int.cpp
- /library/math/combinatorics/arbitrary-mod-int.cpp.html
title: math/combinatorics/arbitrary-mod-int.cpp
---
