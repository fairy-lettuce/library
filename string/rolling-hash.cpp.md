---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-alds-1-14-b.test.cpp
    title: test/verify/aoj-alds-1-14-b.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/rolling-hash.md
    document_title: "Rolling-Hash(\u30ED\u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\
      \u30E5)"
    links:
    - https://qiita.com/keymoon/items/11fac5627672a6d6a9f6
  bundledCode: "#line 1 \"string/rolling-hash.cpp\"\n/**\n * @brief Rolling-Hash(\u30ED\
    \u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\u30E5)\n * @see https://qiita.com/keymoon/items/11fac5627672a6d6a9f6\n\
    \ * @docs docs/rolling-hash.md\n */\nstruct RollingHash {\n  static const uint64_t\
    \ mod = (1ull << 61ull) - 1;\n  using uint128_t = __uint128_t;\n  vector< uint64_t\
    \ > power;\n  const uint64_t base;\n\n  static inline uint64_t add(uint64_t a,\
    \ uint64_t b) {\n    if((a += b) >= mod) a -= mod;\n    return a;\n  }\n\n  static\
    \ inline uint64_t mul(uint64_t a, uint64_t b) {\n    uint128_t c = (uint128_t)\
    \ a * b;\n    return add(c >> 61, c & mod);\n  }\n\n  static inline uint64_t generate_base()\
    \ {\n    mt19937_64 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \    uniform_int_distribution< uint64_t > rand(1, RollingHash::mod - 1);\n   \
    \ return rand(mt);\n  }\n\n  inline void expand(size_t sz) {\n    if(power.size()\
    \ < sz + 1) {\n      int pre_sz = (int) power.size();\n      power.resize(sz +\
    \ 1);\n      for(int i = pre_sz - 1; i < sz; i++) {\n        power[i + 1] = mul(power[i],\
    \ base);\n      }\n    }\n  }\n\n  explicit RollingHash(uint64_t base = generate_base())\
    \ : base(base), power{1} {}\n\n  vector< uint64_t > build(const string &s) const\
    \ {\n    int sz = s.size();\n    vector< uint64_t > hashed(sz + 1);\n    for(int\
    \ i = 0; i < sz; i++) {\n      hashed[i + 1] = add(mul(hashed[i], base), s[i]);\n\
    \    }\n    return hashed;\n  }\n\n  template< typename T >\n  vector< uint64_t\
    \ > build(const vector< T > &s) const {\n    int sz = s.size();\n    vector< uint64_t\
    \ > hashed(sz + 1);\n    for(int i = 0; i < sz; i++) {\n      hashed[i + 1] =\
    \ add(mul(hashed[i], base), s[i]);\n    }\n    return hashed;\n  }\n\n  uint64_t\
    \ query(const vector< uint64_t > &s, int l, int r) {\n    expand(r - l);\n   \
    \ return add(s[r], mod - mul(s[l], power[r - l]));\n  }\n\n  uint64_t combine(uint64_t\
    \ h1, uint64_t h2, size_t h2len) {\n    expand(h2len);\n    return add(mul(h1,\
    \ power[h2len]), h2);\n  }\n\n  int lcp(const vector< uint64_t > &a, int l1, int\
    \ r1, const vector< uint64_t > &b, int l2, int r2) {\n    int len = min(r1 - l1,\
    \ r2 - l2);\n    int low = 0, high = len + 1;\n    while(high - low > 1) {\n \
    \     int mid = (low + high) / 2;\n      if(query(a, l1, l1 + mid) == query(b,\
    \ l2, l2 + mid)) low = mid;\n      else high = mid;\n    }\n    return low;\n\
    \  }\n};\n"
  code: "/**\n * @brief Rolling-Hash(\u30ED\u30FC\u30EA\u30F3\u30B0\u30CF\u30C3\u30B7\
    \u30E5)\n * @see https://qiita.com/keymoon/items/11fac5627672a6d6a9f6\n * @docs\
    \ docs/rolling-hash.md\n */\nstruct RollingHash {\n  static const uint64_t mod\
    \ = (1ull << 61ull) - 1;\n  using uint128_t = __uint128_t;\n  vector< uint64_t\
    \ > power;\n  const uint64_t base;\n\n  static inline uint64_t add(uint64_t a,\
    \ uint64_t b) {\n    if((a += b) >= mod) a -= mod;\n    return a;\n  }\n\n  static\
    \ inline uint64_t mul(uint64_t a, uint64_t b) {\n    uint128_t c = (uint128_t)\
    \ a * b;\n    return add(c >> 61, c & mod);\n  }\n\n  static inline uint64_t generate_base()\
    \ {\n    mt19937_64 mt(chrono::steady_clock::now().time_since_epoch().count());\n\
    \    uniform_int_distribution< uint64_t > rand(1, RollingHash::mod - 1);\n   \
    \ return rand(mt);\n  }\n\n  inline void expand(size_t sz) {\n    if(power.size()\
    \ < sz + 1) {\n      int pre_sz = (int) power.size();\n      power.resize(sz +\
    \ 1);\n      for(int i = pre_sz - 1; i < sz; i++) {\n        power[i + 1] = mul(power[i],\
    \ base);\n      }\n    }\n  }\n\n  explicit RollingHash(uint64_t base = generate_base())\
    \ : base(base), power{1} {}\n\n  vector< uint64_t > build(const string &s) const\
    \ {\n    int sz = s.size();\n    vector< uint64_t > hashed(sz + 1);\n    for(int\
    \ i = 0; i < sz; i++) {\n      hashed[i + 1] = add(mul(hashed[i], base), s[i]);\n\
    \    }\n    return hashed;\n  }\n\n  template< typename T >\n  vector< uint64_t\
    \ > build(const vector< T > &s) const {\n    int sz = s.size();\n    vector< uint64_t\
    \ > hashed(sz + 1);\n    for(int i = 0; i < sz; i++) {\n      hashed[i + 1] =\
    \ add(mul(hashed[i], base), s[i]);\n    }\n    return hashed;\n  }\n\n  uint64_t\
    \ query(const vector< uint64_t > &s, int l, int r) {\n    expand(r - l);\n   \
    \ return add(s[r], mod - mul(s[l], power[r - l]));\n  }\n\n  uint64_t combine(uint64_t\
    \ h1, uint64_t h2, size_t h2len) {\n    expand(h2len);\n    return add(mul(h1,\
    \ power[h2len]), h2);\n  }\n\n  int lcp(const vector< uint64_t > &a, int l1, int\
    \ r1, const vector< uint64_t > &b, int l2, int r2) {\n    int len = min(r1 - l1,\
    \ r2 - l2);\n    int low = 0, high = len + 1;\n    while(high - low > 1) {\n \
    \     int mid = (low + high) / 2;\n      if(query(a, l1, l1 + mid) == query(b,\
    \ l2, l2 + mid)) low = mid;\n      else high = mid;\n    }\n    return low;\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: string/rolling-hash.cpp
  requiredBy: []
  timestamp: '2020-11-05 18:18:32+09:00'
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

* `RollingHash(base)`: 基数 `base` のローリングハッシュを構築する.
* `generate_base()`: $2^{61} - 1$ 以下の乱数を返す。これを `base` とすると Hack されにくい.
* `build(s)`: 文字列 `s` のハッシュテーブルを返す.
* `query(s, l, r)`: `s` の区間 $[l, r)$ のハッシュ値を返す.
* `combine(h1, h2, h2len)`: ハッシュ値 `h1` と長さ `h2len` のハッシュ値 `h2` を結合する. `power[h2len]` での配列外参照に注意(TODO 実装).
* `lcp(a, l1, r1, b, l2, r2)`: ハッシュテーブル `a` の区間 $[l1, r1)$ と, ハッシュテーブル `b` の区間 $[l2, r2)$ の文字列の最長共通接頭辞の長さを返す.

## 計算量

* `build()`: $O(n)$
* `lcp()`: $O(\log n)$
* クエリ: $O(1)$
