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
  bundledCode: "#line 1 \"math/combinatorics/vectorize-mod-int.cpp\"\n#include <immintrin.h>\n\
    #pragma GCC target (\"avx2\")\n\nstruct alignas(32) VectorizeModInt {\n  using\
    \ Mints = VectorizeModInt;\n  using i32 = int32_t;\n  using i64 = int64_t;\n \
    \ using u32 = uint32_t;\n  using u64 = uint64_t;\n\n  static __m256i m0, m1, m2,\
    \ r1;\n\n  template< typename Mint >\n  static void set_mod() {\n    r1 = _mm256_set1_epi32(Mint::r);\n\
    \    m0 = _mm256_setzero_si256();\n    m1 = _mm256_set1_epi32(Mint::get_mod());\n\
    \    m2 = _mm256_set1_epi32(Mint::get_mod() * 2);\n  }\n\n  __m256i x;\n\n  VectorizeModInt()\
    \ : x{} {}\n\n  inline VectorizeModInt(const i32 &v) : x(_mm256_set1_epi32(v))\
    \ {}\n\n  inline VectorizeModInt(const i32 &v0, const i32 &v1, const i32 &v2,\
    \ const i32 &v3,\n                         const i32 &v4, const i32 &v5, const\
    \ i32 &v6, const i32 &v7) :\n      x(_mm256_setr_epi32(v0, v1, v2, v3, v4, v5,\
    \ v6, v7)) {}\n\n  inline VectorizeModInt(const void *vs) : x(_mm256_loadu_si256((__m256i\
    \ *) vs)) {}\n\n  inline VectorizeModInt(const __m256i &x) : x(x) {}\n\n  inline\
    \ void store(const void *vs) {\n    _mm256_storeu_si256((__m256i *) vs, x);\n\
    \  }\n\n  static inline __m256i _mm256_mulhi_epi32(const __m256i &a, const __m256i\
    \ &b) {\n    auto prod02 = _mm256_mul_epu32(a, b);\n    auto prod13 = _mm256_mul_epu32(_mm256_shuffle_epi32(a,\
    \ 0xf5), _mm256_shuffle_epi32(b, 0xf5));\n    return _mm256_unpackhi_epi64(_mm256_unpacklo_epi32(prod02,\
    \ prod13), _mm256_unpackhi_epi32(prod02, prod13));\n  }\n\n  static inline __m256i\
    \ reduce(const __m256i &lo, const __m256i &hi) {\n    // u32(b >> 32) + mod -\
    \ u32((u64(u32(b) * r) * mod) >> 32)\n    return _mm256_add_epi32(_mm256_sub_epi32(hi,\
    \ _mm256_mulhi_epi32(_mm256_mullo_epi32(lo, r1), m1)), m1);\n  }\n\n  Mints inline\
    \ &operator+=(const Mints &p) {\n    // if(int(x += p.x - 2 * mod) < 0) x += 2\
    \ * mod;\n    const auto c = _mm256_sub_epi32(_mm256_add_epi32(x, p.x), m2);\n\
    \    x = _mm256_add_epi32(c, _mm256_and_si256(_mm256_cmpgt_epi32(m0, c), m2));\n\
    \    return *this;\n  }\n\n\n  Mints inline &operator-=(const Mints &p) {\n  \
    \  // if(int(x -= p.x) < 0) x += 2 * mod;\n    const auto c = _mm256_sub_epi32(x,\
    \ p.x);\n    x = _mm256_add_epi32(c, _mm256_and_si256(_mm256_cmpgt_epi32(m0, c),\
    \ m2));\n    return *this;\n  }\n\n  Mints inline &operator*=(const Mints &p)\
    \ {\n    x = reduce(_mm256_mullo_epi32(x, p.x), _mm256_mulhi_epi32(x, p.x));\n\
    \    return *this;\n  }\n\n  Mints inline operator+(const Mints &p) const { return\
    \ Mints(*this) += p; }\n\n  Mints inline operator-(const Mints &p) const { return\
    \ Mints(*this) -= p; }\n\n  Mints inline operator*(const Mints &p) const { return\
    \ Mints(*this) *= p; }\n};\n\n__attribute__((aligned(32))) __m256i VectorizeModInt::m0;\n\
    __attribute__((aligned(32))) __m256i VectorizeModInt::m1;\n__attribute__((aligned(32)))\
    \ __m256i VectorizeModInt::m2;\n__attribute__((aligned(32))) __m256i VectorizeModInt::r1;\n"
  code: "#include <immintrin.h>\n#pragma GCC target (\"avx2\")\n\nstruct alignas(32)\
    \ VectorizeModInt {\n  using Mints = VectorizeModInt;\n  using i32 = int32_t;\n\
    \  using i64 = int64_t;\n  using u32 = uint32_t;\n  using u64 = uint64_t;\n\n\
    \  static __m256i m0, m1, m2, r1;\n\n  template< typename Mint >\n  static void\
    \ set_mod() {\n    r1 = _mm256_set1_epi32(Mint::r);\n    m0 = _mm256_setzero_si256();\n\
    \    m1 = _mm256_set1_epi32(Mint::get_mod());\n    m2 = _mm256_set1_epi32(Mint::get_mod()\
    \ * 2);\n  }\n\n  __m256i x;\n\n  VectorizeModInt() : x{} {}\n\n  inline VectorizeModInt(const\
    \ i32 &v) : x(_mm256_set1_epi32(v)) {}\n\n  inline VectorizeModInt(const i32 &v0,\
    \ const i32 &v1, const i32 &v2, const i32 &v3,\n                         const\
    \ i32 &v4, const i32 &v5, const i32 &v6, const i32 &v7) :\n      x(_mm256_setr_epi32(v0,\
    \ v1, v2, v3, v4, v5, v6, v7)) {}\n\n  inline VectorizeModInt(const void *vs)\
    \ : x(_mm256_loadu_si256((__m256i *) vs)) {}\n\n  inline VectorizeModInt(const\
    \ __m256i &x) : x(x) {}\n\n  inline void store(const void *vs) {\n    _mm256_storeu_si256((__m256i\
    \ *) vs, x);\n  }\n\n  static inline __m256i _mm256_mulhi_epi32(const __m256i\
    \ &a, const __m256i &b) {\n    auto prod02 = _mm256_mul_epu32(a, b);\n    auto\
    \ prod13 = _mm256_mul_epu32(_mm256_shuffle_epi32(a, 0xf5), _mm256_shuffle_epi32(b,\
    \ 0xf5));\n    return _mm256_unpackhi_epi64(_mm256_unpacklo_epi32(prod02, prod13),\
    \ _mm256_unpackhi_epi32(prod02, prod13));\n  }\n\n  static inline __m256i reduce(const\
    \ __m256i &lo, const __m256i &hi) {\n    // u32(b >> 32) + mod - u32((u64(u32(b)\
    \ * r) * mod) >> 32)\n    return _mm256_add_epi32(_mm256_sub_epi32(hi, _mm256_mulhi_epi32(_mm256_mullo_epi32(lo,\
    \ r1), m1)), m1);\n  }\n\n  Mints inline &operator+=(const Mints &p) {\n    //\
    \ if(int(x += p.x - 2 * mod) < 0) x += 2 * mod;\n    const auto c = _mm256_sub_epi32(_mm256_add_epi32(x,\
    \ p.x), m2);\n    x = _mm256_add_epi32(c, _mm256_and_si256(_mm256_cmpgt_epi32(m0,\
    \ c), m2));\n    return *this;\n  }\n\n\n  Mints inline &operator-=(const Mints\
    \ &p) {\n    // if(int(x -= p.x) < 0) x += 2 * mod;\n    const auto c = _mm256_sub_epi32(x,\
    \ p.x);\n    x = _mm256_add_epi32(c, _mm256_and_si256(_mm256_cmpgt_epi32(m0, c),\
    \ m2));\n    return *this;\n  }\n\n  Mints inline &operator*=(const Mints &p)\
    \ {\n    x = reduce(_mm256_mullo_epi32(x, p.x), _mm256_mulhi_epi32(x, p.x));\n\
    \    return *this;\n  }\n\n  Mints inline operator+(const Mints &p) const { return\
    \ Mints(*this) += p; }\n\n  Mints inline operator-(const Mints &p) const { return\
    \ Mints(*this) -= p; }\n\n  Mints inline operator*(const Mints &p) const { return\
    \ Mints(*this) *= p; }\n};\n\n__attribute__((aligned(32))) __m256i VectorizeModInt::m0;\n\
    __attribute__((aligned(32))) __m256i VectorizeModInt::m1;\n__attribute__((aligned(32)))\
    \ __m256i VectorizeModInt::m2;\n__attribute__((aligned(32))) __m256i VectorizeModInt::r1;\n"
  dependsOn: []
  isVerificationFile: false
  path: math/combinatorics/vectorize-mod-int.cpp
  requiredBy: []
  timestamp: '2021-08-11 21:33:21+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/combinatorics/vectorize-mod-int.cpp
layout: document
redirect_from:
- /library/math/combinatorics/vectorize-mod-int.cpp
- /library/math/combinatorics/vectorize-mod-int.cpp.html
title: math/combinatorics/vectorize-mod-int.cpp
---
