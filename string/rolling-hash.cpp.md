---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-alds-1-14-b.test.cpp
    title: test/verify/aoj-alds-1-14-b.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    _deprecated_at_docs: docs/rolling-hash.md
    document_title: "Rolling-Hash(\u30ED\u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\
      \u30E5)"
    links:
    - https://qiita.com/keymoon/items/11fac5627672a6d6a9f6
  bundledCode: "#line 1 \"string/rolling-hash.cpp\"\n/**\n * @brief Rolling-Hash(\u30ED\
    \u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\u30E5)\n * @see https://qiita.com/keymoon/items/11fac5627672a6d6a9f6\n\
    \ * @docs docs/rolling-hash.md\n */\nstruct RollingHash {\n  static const uint64_t\
    \ mod = (1ull << 61ull) - 1;\n  using uint128_t = __uint128_t;\n  vector< uint64_t\
    \ > hashed, power;\n  const uint64_t base;\n\n  static inline uint64_t add(uint64_t\
    \ a, uint64_t b) {\n    if((a += b) >= mod) a -= mod;\n    return a;\n  }\n\n\
    \  static inline uint64_t mul(uint64_t a, uint64_t b) {\n    uint128_t c = (uint128_t)\
    \ a * b;\n    return add(c >> 61, c & mod);\n  }\n\n  static inline uint64_t generate_base()\
    \ {\n    mt19937_64 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \    uniform_int_distribution< uint64_t > rand(1, RollingHash::mod - 1);\n   \
    \ return rand(mt);\n  }\n\n  RollingHash() = default;\n\n  RollingHash(const string\
    \ &s, uint64_t base) : base(base) {\n    size_t sz = s.size();\n    hashed.assign(sz\
    \ + 1, 0);\n    power.assign(sz + 1, 0);\n    power[0] = 1;\n    for(int i = 0;\
    \ i < sz; i++) {\n      power[i + 1] = mul(power[i], base);\n      hashed[i +\
    \ 1] = add(mul(hashed[i], base), s[i]);\n    }\n  }\n\n  template< typename T\
    \ >\n  RollingHash(const vector< T > &s, uint64_t base) : base(base) {\n    size_t\
    \ sz = s.size();\n    hashed.assign(sz + 1, 0);\n    power.assign(sz + 1, 0);\n\
    \    power[0] = 1;\n    for(int i = 0; i < sz; i++) {\n      power[i + 1] = mul(power[i],\
    \ base);\n      hashed[i + 1] = add(mul(hashed[i], base), s[i]);\n    }\n  }\n\
    \n  uint64_t query(int l, int r) const {\n    return add(hashed[r], mod - mul(hashed[l],\
    \ power[r - l]));\n  }\n\n  uint64_t combine(uint64_t h1, uint64_t h2, size_t\
    \ h2len) const {\n    return add(mul(h1, power[h2len]), h2);\n  }\n\n  int lcp(const\
    \ RollingHash &b, int l1, int r1, int l2, int r2) const {\n    assert(base ==\
    \ b.base);\n    int len = min(r1 - l1, r2 - l2);\n    int low = 0, high = len\
    \ + 1;\n    while(high - low > 1) {\n      int mid = (low + high) / 2;\n     \
    \ if(query(l1, l1 + mid) == b.query(l2, l2 + mid)) low = mid;\n      else high\
    \ = mid;\n    }\n    return low;\n  }\n};\n"
  code: "/**\n * @brief Rolling-Hash(\u30ED\u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\
    \u30E5)\n * @see https://qiita.com/keymoon/items/11fac5627672a6d6a9f6\n * @docs\
    \ docs/rolling-hash.md\n */\nstruct RollingHash {\n  static const uint64_t mod\
    \ = (1ull << 61ull) - 1;\n  using uint128_t = __uint128_t;\n  vector< uint64_t\
    \ > hashed, power;\n  const uint64_t base;\n\n  static inline uint64_t add(uint64_t\
    \ a, uint64_t b) {\n    if((a += b) >= mod) a -= mod;\n    return a;\n  }\n\n\
    \  static inline uint64_t mul(uint64_t a, uint64_t b) {\n    uint128_t c = (uint128_t)\
    \ a * b;\n    return add(c >> 61, c & mod);\n  }\n\n  static inline uint64_t generate_base()\
    \ {\n    mt19937_64 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \    uniform_int_distribution< uint64_t > rand(1, RollingHash::mod - 1);\n   \
    \ return rand(mt);\n  }\n\n  RollingHash() = default;\n\n  RollingHash(const string\
    \ &s, uint64_t base) : base(base) {\n    size_t sz = s.size();\n    hashed.assign(sz\
    \ + 1, 0);\n    power.assign(sz + 1, 0);\n    power[0] = 1;\n    for(int i = 0;\
    \ i < sz; i++) {\n      power[i + 1] = mul(power[i], base);\n      hashed[i +\
    \ 1] = add(mul(hashed[i], base), s[i]);\n    }\n  }\n\n  template< typename T\
    \ >\n  RollingHash(const vector< T > &s, uint64_t base) : base(base) {\n    size_t\
    \ sz = s.size();\n    hashed.assign(sz + 1, 0);\n    power.assign(sz + 1, 0);\n\
    \    power[0] = 1;\n    for(int i = 0; i < sz; i++) {\n      power[i + 1] = mul(power[i],\
    \ base);\n      hashed[i + 1] = add(mul(hashed[i], base), s[i]);\n    }\n  }\n\
    \n  uint64_t query(int l, int r) const {\n    return add(hashed[r], mod - mul(hashed[l],\
    \ power[r - l]));\n  }\n\n  uint64_t combine(uint64_t h1, uint64_t h2, size_t\
    \ h2len) const {\n    return add(mul(h1, power[h2len]), h2);\n  }\n\n  int lcp(const\
    \ RollingHash &b, int l1, int r1, int l2, int r2) const {\n    assert(base ==\
    \ b.base);\n    int len = min(r1 - l1, r2 - l2);\n    int low = 0, high = len\
    \ + 1;\n    while(high - low > 1) {\n      int mid = (low + high) / 2;\n     \
    \ if(query(l1, l1 + mid) == b.query(l2, l2 + mid)) low = mid;\n      else high\
    \ = mid;\n    }\n    return low;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: string/rolling-hash.cpp
  requiredBy: []
  timestamp: '2020-05-10 01:03:47+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-alds-1-14-b.test.cpp
documentation_of: string/rolling-hash.cpp
layout: document
redirect_from:
- /library/string/rolling-hash.cpp
- /library/string/rolling-hash.cpp.html
title: "Rolling-Hash(\u30ED\u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\u30E5)"
---
## 概要

文字列の一致判定を mod $2^{61}-1$ のハッシュを用いて効率的に行う.

* `RollingHash(s, base)`: 文字列 $s$ のハッシュテーブルを構築する.
* `generate_base()`: $2^{61} - 1$ 以下の乱数を返す。これを `base` とすると Hack されにくい.
* `query(l, r)`: 区間 $[l, r)$ のハッシュ値を返す.
* `combine(h1, h2, h2len)`: ハッシュ値 `h1` と長さ `h2len` のハッシュ値 `h2` を結合する. `power[h2len]` での配列外参照に注意(TODO 実装).
* `lcp(b, l1, r1, l2, r2)`: 区間 $[l1, r1)$ と, ハッシュテーブルが `b` からなる区間 $[l2, r2)$ の文字列の最長共通接頭辞の長さを返す.

## 計算量

* 構築: $O(n)$
* `lcp()`: $O(\log n)$
* クエリ: $O(1)$
