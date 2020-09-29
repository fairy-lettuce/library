---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-factorize.test.cpp
    title: test/verify/yosupo-factorize.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    links:
    - http://miller-rabin.appspot.com/
  bundledCode: "#line 1 \"math/number-theory/fast-prime-factorization.cpp\"\nnamespace\
    \ FastPrimeFactorization {\n\n  template< typename word, typename dword, typename\
    \ sword >\n  struct UnsafeMod {\n    UnsafeMod() : x(0) {}\n\n    UnsafeMod(word\
    \ _x) : x(init(_x)) {}\n\n    bool operator==(const UnsafeMod &rhs) const {\n\
    \      return x == rhs.x;\n    }\n\n    bool operator!=(const UnsafeMod &rhs)\
    \ const {\n      return x != rhs.x;\n    }\n\n    UnsafeMod &operator+=(const\
    \ UnsafeMod &rhs) {\n      if((x += rhs.x) >= mod) x -= mod;\n      return *this;\n\
    \    }\n\n    UnsafeMod &operator-=(const UnsafeMod &rhs) {\n      if(sword(x\
    \ -= rhs.x) < 0) x += mod;\n      return *this;\n    }\n\n    UnsafeMod &operator*=(const\
    \ UnsafeMod &rhs) {\n      x = reduce(dword(x) * rhs.x);\n      return *this;\n\
    \    }\n\n    UnsafeMod operator+(const UnsafeMod &rhs) const {\n      return\
    \ UnsafeMod(*this) += rhs;\n    }\n\n    UnsafeMod operator-(const UnsafeMod &rhs)\
    \ const {\n      return UnsafeMod(*this) -= rhs;\n    }\n\n    UnsafeMod operator*(const\
    \ UnsafeMod &rhs) const {\n      return UnsafeMod(*this) *= rhs;\n    }\n\n  \
    \  UnsafeMod pow(uint64_t e) const {\n      UnsafeMod ret(1);\n      for(UnsafeMod\
    \ base = *this; e; e >>= 1, base *= base) {\n        if(e & 1) ret *= base;\n\
    \      }\n      return ret;\n    }\n\n    word get() const {\n      return reduce(x);\n\
    \    }\n\n    static constexpr int word_bits = sizeof(word) * 8;\n\n    static\
    \ word modulus() {\n      return mod;\n    }\n\n    static word init(word w) {\n\
    \      return reduce(dword(w) * r2);\n    }\n\n    static void set_mod(word m)\
    \ {\n      mod = m;\n      inv = mul_inv(mod);\n      r2 = -dword(mod) % mod;\n\
    \    }\n\n    static word reduce(dword x) {\n      word y = word(x >> word_bits)\
    \ - word((dword(word(x) * inv) * mod) >> word_bits);\n      return sword(y) <\
    \ 0 ? y + mod : y;\n    }\n\n    static word mul_inv(word n, int e = 6, word x\
    \ = 1) {\n      return !e ? x : mul_inv(n, e - 1, x * (2 - x * n));\n    }\n\n\
    \    static word mod, inv, r2;\n\n    word x;\n  };\n\n  using uint128_t = __uint128_t;\n\
    \n  using Mod64 = UnsafeMod< uint64_t, uint128_t, int64_t >;\n  template<> uint64_t\
    \ Mod64::mod = 0;\n  template<> uint64_t Mod64::inv = 0;\n  template<> uint64_t\
    \ Mod64::r2 = 0;\n\n  using Mod32 = UnsafeMod< uint32_t, uint64_t, int32_t >;\n\
    \  template<> uint32_t Mod32::mod = 0;\n  template<> uint32_t Mod32::inv = 0;\n\
    \  template<> uint32_t Mod32::r2 = 0;\n\n  bool miller_rabin_primality_test_uint64(uint64_t\
    \ n) {\n    Mod64::set_mod(n);\n    uint64_t d = n - 1;\n    while(d % 2 == 0)\
    \ d /= 2;\n    Mod64 e{1}, rev{n - 1};\n    // http://miller-rabin.appspot.com/\
    \  < 2^64\n    for(uint64_t a : {2, 325, 9375, 28178, 450775, 9780504, 1795265022})\
    \ {\n      if(n <= a) break;\n      uint64_t t = d;\n      Mod64 y = Mod64(a).pow(t);\n\
    \      while(t != n - 1 && y != e && y != rev) {\n        y *= y;\n        t *=\
    \ 2;\n      }\n      if(y != rev && t % 2 == 0) return false;\n    }\n    return\
    \ true;\n  }\n\n  bool miller_rabin_primality_test_uint32(uint32_t n) {\n    Mod32::set_mod(n);\n\
    \    uint32_t d = n - 1;\n    while(d % 2 == 0) d /= 2;\n    Mod32 e{1}, rev{n\
    \ - 1};\n    for(uint32_t a : {2, 7, 61}) {\n      if(n <= a) break;\n      uint32_t\
    \ t = d;\n      Mod32 y = Mod32(a).pow(t);\n      while(t != n - 1 && y != e &&\
    \ y != rev) {\n        y *= y;\n        t *= 2;\n      }\n      if(y != rev &&\
    \ t % 2 == 0) return false;\n    }\n    return true;\n  }\n\n  bool is_prime(uint64_t\
    \ n) {\n    if(n == 2) return true;\n    if(n == 1 || n % 2 == 0) return false;\n\
    \    if(n < uint64_t(1) << 31) return miller_rabin_primality_test_uint32(n);\n\
    \    return miller_rabin_primality_test_uint64(n);\n  }\n\n  uint64_t pollard_rho(uint64_t\
    \ n) {\n    if(is_prime(n)) return n;\n    if(n % 2 == 0) return 2;\n    Mod64::set_mod(n);\n\
    \    uint64_t d;\n    Mod64 one{1};\n    for(Mod64 c{one};; c += one) {\n    \
    \  Mod64 x{2}, y{2};\n      do {\n        x = x * x + c;\n        y = y * y +\
    \ c;\n        y = y * y + c;\n        d = __gcd((x - y).get(), n);\n      } while(d\
    \ == 1);\n      if(d < n) return d;\n    }\n    assert(0);\n  }\n\n  vector< uint64_t\
    \ > prime_factor(uint64_t n) {\n    if(n <= 1) return {};\n    uint64_t p = pollard_rho(n);\n\
    \    if(p == n) return {p};\n    auto l = prime_factor(p);\n    auto r = prime_factor(n\
    \ / p);\n    copy(begin(r), end(r), back_inserter(l));\n    return l;\n  }\n};\n"
  code: "namespace FastPrimeFactorization {\n\n  template< typename word, typename\
    \ dword, typename sword >\n  struct UnsafeMod {\n    UnsafeMod() : x(0) {}\n\n\
    \    UnsafeMod(word _x) : x(init(_x)) {}\n\n    bool operator==(const UnsafeMod\
    \ &rhs) const {\n      return x == rhs.x;\n    }\n\n    bool operator!=(const\
    \ UnsafeMod &rhs) const {\n      return x != rhs.x;\n    }\n\n    UnsafeMod &operator+=(const\
    \ UnsafeMod &rhs) {\n      if((x += rhs.x) >= mod) x -= mod;\n      return *this;\n\
    \    }\n\n    UnsafeMod &operator-=(const UnsafeMod &rhs) {\n      if(sword(x\
    \ -= rhs.x) < 0) x += mod;\n      return *this;\n    }\n\n    UnsafeMod &operator*=(const\
    \ UnsafeMod &rhs) {\n      x = reduce(dword(x) * rhs.x);\n      return *this;\n\
    \    }\n\n    UnsafeMod operator+(const UnsafeMod &rhs) const {\n      return\
    \ UnsafeMod(*this) += rhs;\n    }\n\n    UnsafeMod operator-(const UnsafeMod &rhs)\
    \ const {\n      return UnsafeMod(*this) -= rhs;\n    }\n\n    UnsafeMod operator*(const\
    \ UnsafeMod &rhs) const {\n      return UnsafeMod(*this) *= rhs;\n    }\n\n  \
    \  UnsafeMod pow(uint64_t e) const {\n      UnsafeMod ret(1);\n      for(UnsafeMod\
    \ base = *this; e; e >>= 1, base *= base) {\n        if(e & 1) ret *= base;\n\
    \      }\n      return ret;\n    }\n\n    word get() const {\n      return reduce(x);\n\
    \    }\n\n    static constexpr int word_bits = sizeof(word) * 8;\n\n    static\
    \ word modulus() {\n      return mod;\n    }\n\n    static word init(word w) {\n\
    \      return reduce(dword(w) * r2);\n    }\n\n    static void set_mod(word m)\
    \ {\n      mod = m;\n      inv = mul_inv(mod);\n      r2 = -dword(mod) % mod;\n\
    \    }\n\n    static word reduce(dword x) {\n      word y = word(x >> word_bits)\
    \ - word((dword(word(x) * inv) * mod) >> word_bits);\n      return sword(y) <\
    \ 0 ? y + mod : y;\n    }\n\n    static word mul_inv(word n, int e = 6, word x\
    \ = 1) {\n      return !e ? x : mul_inv(n, e - 1, x * (2 - x * n));\n    }\n\n\
    \    static word mod, inv, r2;\n\n    word x;\n  };\n\n  using uint128_t = __uint128_t;\n\
    \n  using Mod64 = UnsafeMod< uint64_t, uint128_t, int64_t >;\n  template<> uint64_t\
    \ Mod64::mod = 0;\n  template<> uint64_t Mod64::inv = 0;\n  template<> uint64_t\
    \ Mod64::r2 = 0;\n\n  using Mod32 = UnsafeMod< uint32_t, uint64_t, int32_t >;\n\
    \  template<> uint32_t Mod32::mod = 0;\n  template<> uint32_t Mod32::inv = 0;\n\
    \  template<> uint32_t Mod32::r2 = 0;\n\n  bool miller_rabin_primality_test_uint64(uint64_t\
    \ n) {\n    Mod64::set_mod(n);\n    uint64_t d = n - 1;\n    while(d % 2 == 0)\
    \ d /= 2;\n    Mod64 e{1}, rev{n - 1};\n    // http://miller-rabin.appspot.com/\
    \  < 2^64\n    for(uint64_t a : {2, 325, 9375, 28178, 450775, 9780504, 1795265022})\
    \ {\n      if(n <= a) break;\n      uint64_t t = d;\n      Mod64 y = Mod64(a).pow(t);\n\
    \      while(t != n - 1 && y != e && y != rev) {\n        y *= y;\n        t *=\
    \ 2;\n      }\n      if(y != rev && t % 2 == 0) return false;\n    }\n    return\
    \ true;\n  }\n\n  bool miller_rabin_primality_test_uint32(uint32_t n) {\n    Mod32::set_mod(n);\n\
    \    uint32_t d = n - 1;\n    while(d % 2 == 0) d /= 2;\n    Mod32 e{1}, rev{n\
    \ - 1};\n    for(uint32_t a : {2, 7, 61}) {\n      if(n <= a) break;\n      uint32_t\
    \ t = d;\n      Mod32 y = Mod32(a).pow(t);\n      while(t != n - 1 && y != e &&\
    \ y != rev) {\n        y *= y;\n        t *= 2;\n      }\n      if(y != rev &&\
    \ t % 2 == 0) return false;\n    }\n    return true;\n  }\n\n  bool is_prime(uint64_t\
    \ n) {\n    if(n == 2) return true;\n    if(n == 1 || n % 2 == 0) return false;\n\
    \    if(n < uint64_t(1) << 31) return miller_rabin_primality_test_uint32(n);\n\
    \    return miller_rabin_primality_test_uint64(n);\n  }\n\n  uint64_t pollard_rho(uint64_t\
    \ n) {\n    if(is_prime(n)) return n;\n    if(n % 2 == 0) return 2;\n    Mod64::set_mod(n);\n\
    \    uint64_t d;\n    Mod64 one{1};\n    for(Mod64 c{one};; c += one) {\n    \
    \  Mod64 x{2}, y{2};\n      do {\n        x = x * x + c;\n        y = y * y +\
    \ c;\n        y = y * y + c;\n        d = __gcd((x - y).get(), n);\n      } while(d\
    \ == 1);\n      if(d < n) return d;\n    }\n    assert(0);\n  }\n\n  vector< uint64_t\
    \ > prime_factor(uint64_t n) {\n    if(n <= 1) return {};\n    uint64_t p = pollard_rho(n);\n\
    \    if(p == n) return {p};\n    auto l = prime_factor(p);\n    auto r = prime_factor(n\
    \ / p);\n    copy(begin(r), end(r), back_inserter(l));\n    return l;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: math/number-theory/fast-prime-factorization.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:36:31+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-factorize.test.cpp
documentation_of: math/number-theory/fast-prime-factorization.cpp
layout: document
redirect_from:
- /library/math/number-theory/fast-prime-factorization.cpp
- /library/math/number-theory/fast-prime-factorization.cpp.html
title: math/number-theory/fast-prime-factorization.cpp
---
