---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/number-theory/kth-root-integer.cpp
    title: Kth Root Integer
  - icon: ':heavy_check_mark:'
    path: math/number-theory/prime-table.cpp
    title: "Prime Table(\u7D20\u6570\u30C6\u30FC\u30D6\u30EB)"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-counting-primes.test.cpp
    title: test/verify/yosupo-counting-primes.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Prime Count(\u7D20\u6570\u306E\u500B\u6570)"
    links: []
  bundledCode: "#line 1 \"math/number-theory/kth-root-integer.cpp\"\n/**\n * @brief\
    \ Kth Root Integer\n * @docs docs/kth-root-integer.md\n */\nuint64_t kth_root_integer(uint64_t\
    \ a, int k) {\n  if(k == 1) return a;\n  auto check = [&](uint32_t x) {\n    uint64_t\
    \ mul = 1;\n    for(int j = 0; j < k; j++) {\n      if(__builtin_mul_overflow(mul,\
    \ x, &mul)) return false;\n    }\n    return mul <= a;\n  };\n  uint64_t ret =\
    \ 0;\n  for(int i = 31; i >= 0; i--) {\n    if(check(ret | (1u << i))) ret |=\
    \ 1u << i;\n  }\n  return ret;\n}\n#line 1 \"math/number-theory/prime-table.cpp\"\
    \n/**\n * @brief Prime Table(\u7D20\u6570\u30C6\u30FC\u30D6\u30EB)\n * @docs docs/prime-table.md\n\
    \ */\nvector< bool > prime_table(int n) {\n  vector< bool > prime(n + 1, true);\n\
    \  if(n >= 0) prime[0] = false;\n  if(n >= 1) prime[1] = false;\n  for(int i =\
    \ 2; i * i <= n; i++) {\n    if(!prime[i]) continue;\n    for(int j = i * i; j\
    \ <= n; j += i) {\n      prime[j] = false;\n    }\n  }\n  return prime;\n}\n#line\
    \ 3 \"math/number-theory/prime-count.cpp\"\n\n/**\n * @brief Prime Count(\u7D20\
    \u6570\u306E\u500B\u6570)\n */\ntemplate< int64_t LIM = 100000000000LL >\nstruct\
    \ PrimeCount {\nprivate:\n  int64_t sq;\n  vector< bool > prime;\n  vector< int64_t\
    \ > prime_sum, primes;\n\n  int64_t p2(int64_t x, int64_t y) {\n    if(x < 4)\
    \ return 0;\n    int64_t a = pi(y);\n    int64_t b = pi(kth_root_integer(x, 2));\n\
    \    if(a >= b) return 0;\n    int64_t sum = (a - 2) * (a + 1) / 2 - (b - 2) *\
    \ (b + 1) / 2;\n    for(int64_t i = a; i < b; i++) sum += pi(x / primes[i]);\n\
    \    return sum;\n  }\n\n  int64_t phi(int64_t m, int64_t n) {\n    if(m < 1)\
    \ return 0;\n    if(n > m) return 1;\n    if(n < 1) return m;\n    if(m <= primes[n\
    \ - 1] * primes[n - 1]) return pi(m) - n + 1;\n    if(m <= primes[n - 1] * primes[n\
    \ - 1] * primes[n - 1] && m <= sq) {\n      int64_t sx = pi(kth_root_integer(m,\
    \ 2));\n      int64_t ans = pi(m) - (sx + n - 2) * (sx - n + 1) / 2;\n      for(int64_t\
    \ i = n; i < sx; ++i) ans += pi(m / primes[i]);\n      return ans;\n    }\n  \
    \  return phi(m, n - 1) - phi(m / primes[n - 1], n - 1);\n  }\n\npublic:\n\n \
    \ PrimeCount() : sq(kth_root_integer(LIM, 2)), prime_sum(sq + 1) {\n    prime\
    \ = prime_table(sq);\n    for(int i = 1; i <= sq; i++) prime_sum[i] = prime_sum[i\
    \ - 1] + prime[i];\n    primes.reserve(prime_sum[sq]);\n    for(int i = 1; i <=\
    \ sq; i++) if(prime[i]) primes.push_back(i);\n  }\n\n  int64_t pi(int64_t n) {\n\
    \    if(n <= sq) return prime_sum[n];\n    int64_t m = kth_root_integer(n, 3);\n\
    \    int64_t a = pi(m);\n    return phi(n, a) + a - 1 - p2(n, m);\n  }\n};\n"
  code: "#include \"kth-root-integer.cpp\"\n#include \"prime-table.cpp\"\n\n/**\n\
    \ * @brief Prime Count(\u7D20\u6570\u306E\u500B\u6570)\n */\ntemplate< int64_t\
    \ LIM = 100000000000LL >\nstruct PrimeCount {\nprivate:\n  int64_t sq;\n  vector<\
    \ bool > prime;\n  vector< int64_t > prime_sum, primes;\n\n  int64_t p2(int64_t\
    \ x, int64_t y) {\n    if(x < 4) return 0;\n    int64_t a = pi(y);\n    int64_t\
    \ b = pi(kth_root_integer(x, 2));\n    if(a >= b) return 0;\n    int64_t sum =\
    \ (a - 2) * (a + 1) / 2 - (b - 2) * (b + 1) / 2;\n    for(int64_t i = a; i < b;\
    \ i++) sum += pi(x / primes[i]);\n    return sum;\n  }\n\n  int64_t phi(int64_t\
    \ m, int64_t n) {\n    if(m < 1) return 0;\n    if(n > m) return 1;\n    if(n\
    \ < 1) return m;\n    if(m <= primes[n - 1] * primes[n - 1]) return pi(m) - n\
    \ + 1;\n    if(m <= primes[n - 1] * primes[n - 1] * primes[n - 1] && m <= sq)\
    \ {\n      int64_t sx = pi(kth_root_integer(m, 2));\n      int64_t ans = pi(m)\
    \ - (sx + n - 2) * (sx - n + 1) / 2;\n      for(int64_t i = n; i < sx; ++i) ans\
    \ += pi(m / primes[i]);\n      return ans;\n    }\n    return phi(m, n - 1) -\
    \ phi(m / primes[n - 1], n - 1);\n  }\n\npublic:\n\n  PrimeCount() : sq(kth_root_integer(LIM,\
    \ 2)), prime_sum(sq + 1) {\n    prime = prime_table(sq);\n    for(int i = 1; i\
    \ <= sq; i++) prime_sum[i] = prime_sum[i - 1] + prime[i];\n    primes.reserve(prime_sum[sq]);\n\
    \    for(int i = 1; i <= sq; i++) if(prime[i]) primes.push_back(i);\n  }\n\n \
    \ int64_t pi(int64_t n) {\n    if(n <= sq) return prime_sum[n];\n    int64_t m\
    \ = kth_root_integer(n, 3);\n    int64_t a = pi(m);\n    return phi(n, a) + a\
    \ - 1 - p2(n, m);\n  }\n};\n"
  dependsOn:
  - math/number-theory/kth-root-integer.cpp
  - math/number-theory/prime-table.cpp
  isVerificationFile: false
  path: math/number-theory/prime-count.cpp
  requiredBy: []
  timestamp: '2021-07-17 08:42:53+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-counting-primes.test.cpp
documentation_of: math/number-theory/prime-count.cpp
layout: document
redirect_from:
- /library/math/number-theory/prime-count.cpp
- /library/math/number-theory/prime-count.cpp.html
title: "Prime Count(\u7D20\u6570\u306E\u500B\u6570)"
---
