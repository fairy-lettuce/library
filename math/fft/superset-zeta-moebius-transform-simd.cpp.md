---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bitwise-and-convolution-2.test.cpp
    title: test/verify/yosupo-bitwise-and-convolution-2.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Superset Zeta/Moebius Transform SIMD (\u4E0A\u4F4D\u96C6\u5408\
      \u306E\u30BC\u30FC\u30BF/\u30E1\u30D3\u30A6\u30B9\u5909\u63DB, SIMD)"
    links: []
  bundledCode: "#line 1 \"math/fft/superset-zeta-moebius-transform-simd.cpp\"\n#include\
    \ <immintrin.h>\n\n/**\n * @brief Superset Zeta/Moebius Transform SIMD (\u4E0A\
    \u4F4D\u96C6\u5408\u306E\u30BC\u30FC\u30BF/\u30E1\u30D3\u30A6\u30B9\u5909\u63DB\
    , SIMD)\n */\n__attribute__((target(\"avx2\")))\nvoid superset_zeta_transform_simd(int\
    \ *buf, int mod, int n) {\n  assert((n & (n - 1)) == 0);\n  auto m_zero = _mm256_set1_epi32(0);\n\
    \  auto m_mod_one = _mm256_set1_epi32(mod - 1);\n  auto m_mod = _mm256_set1_epi32(mod);\n\
    \  auto m_zero2 = _mm_set1_epi32(0);\n  auto m_mod_one2 = _mm_set1_epi32(mod -\
    \ 1);\n  auto m_mod2 = _mm_set1_epi32(mod);\n  for(int i = 1; i < n; i <<= 1)\
    \ {\n    for(int j = 0; j < n; j += i << 1) {\n      if(i <= 2) {\n        for(int\
    \ k = 0; k < i; k++) {\n          buf[j + k] += buf[j + k + i];\n          if(buf[j\
    \ + k] >= mod) buf[j + k] -= mod;\n        }\n      } else if(i == 4) {\n    \
    \    for(int k = 0; k < i; k += 4) {\n          auto a = _mm_loadu_si128((__m128i\
    \ *) (buf + j + k));\n          auto b = _mm_loadu_si128((__m128i *) (buf + j\
    \ + k + i));\n          a = _mm_add_epi32(a, b);\n          a = _mm_sub_epi32(a,\
    \ _mm_and_si128(_mm_cmpgt_epi32(a, m_mod_one2), m_mod2));\n          _mm_storeu_si128((__m128i\
    \ *) (buf + j + k), a);\n        }\n      } else {\n        for(int k = 0; k <\
    \ i; k += 8) {\n          auto a = _mm256_loadu_si256((__m256i *) (buf + j + k));\n\
    \          auto b = _mm256_loadu_si256((__m256i *) (buf + j + k + i));\n     \
    \     a = _mm256_add_epi32(a, b);\n          a = _mm256_sub_epi32(a, _mm256_and_si256(_mm256_cmpgt_epi32(a,\
    \ m_mod_one), m_mod));\n          _mm256_storeu_si256((__m256i *) (buf + j + k),\
    \ a);\n        }\n      }\n    }\n  }\n}\n\n\n__attribute__((target(\"avx2\")))\n\
    void superset_moebius_transform_simd(int *buf, int mod, int n) {\n  assert((n\
    \ & (n - 1)) == 0);\n  auto m_zero = _mm256_set1_epi32(0);\n  auto m_mod = _mm256_set1_epi32(mod);\n\
    \  auto m_zero2 = _mm_set1_epi32(0);\n  auto m_mod2 = _mm_set1_epi32(mod);\n \
    \ for(int i = 1; i < n; i <<= 1) {\n    for(int j = 0; j < n; j += i << 1) {\n\
    \      if(i <= 2) {\n        for(int k = 0; k < i; k++) {\n          buf[j + k]\
    \ += mod - buf[j + k + i];\n          if(buf[j + k] >= mod) buf[j + k] -= mod;\n\
    \        }\n      } else if(i == 4) {\n        for(int k = 0; k < i; k += 4) {\n\
    \          auto a = _mm_loadu_si128((__m128i * )(buf + j + k));\n          auto\
    \ b = _mm_loadu_si128((__m128i * )(buf + j + k + i));\n          a = _mm_sub_epi32(a,\
    \ b);\n          a = _mm_add_epi32(a, _mm_and_si128(_mm_cmpgt_epi32(m_zero2, a),\
    \ m_mod2));\n          _mm_storeu_si128((__m128i * )(buf + j + k), a);\n     \
    \   }\n      } else {\n        for(int k = 0; k < i; k += 8) {\n          auto\
    \ a = _mm256_loadu_si256((__m256i * )(buf + j + k));\n          auto b = _mm256_loadu_si256((__m256i\
    \ * )(buf + j + k + i));\n          a = _mm256_sub_epi32(a, b);\n          a =\
    \ _mm256_add_epi32(a, _mm256_and_si256(_mm256_cmpgt_epi32(m_zero, a), m_mod));\n\
    \          _mm256_storeu_si256((__m256i * )(buf + j + k), a);\n        }\n   \
    \   }\n    }\n  }\n}\n\ntemplate< int mod >\nint *bitwise_and_convolution_simd(int\
    \ *f, int *g, int n) {\n  assert((n & (n - 1)) == 0);\n  superset_zeta_transform_simd(f,\
    \ mod, n);\n  superset_zeta_transform_simd(g, mod, n);\n  for(int i = 0; i < n;\
    \ i++) f[i] = (1uLL * f[i] * g[i]) % mod;\n  superset_moebius_transform_simd(f,\
    \ mod, n);\n  return f;\n}\n"
  code: "#include <immintrin.h>\n\n/**\n * @brief Superset Zeta/Moebius Transform\
    \ SIMD (\u4E0A\u4F4D\u96C6\u5408\u306E\u30BC\u30FC\u30BF/\u30E1\u30D3\u30A6\u30B9\
    \u5909\u63DB, SIMD)\n */\n__attribute__((target(\"avx2\")))\nvoid superset_zeta_transform_simd(int\
    \ *buf, int mod, int n) {\n  assert((n & (n - 1)) == 0);\n  auto m_zero = _mm256_set1_epi32(0);\n\
    \  auto m_mod_one = _mm256_set1_epi32(mod - 1);\n  auto m_mod = _mm256_set1_epi32(mod);\n\
    \  auto m_zero2 = _mm_set1_epi32(0);\n  auto m_mod_one2 = _mm_set1_epi32(mod -\
    \ 1);\n  auto m_mod2 = _mm_set1_epi32(mod);\n  for(int i = 1; i < n; i <<= 1)\
    \ {\n    for(int j = 0; j < n; j += i << 1) {\n      if(i <= 2) {\n        for(int\
    \ k = 0; k < i; k++) {\n          buf[j + k] += buf[j + k + i];\n          if(buf[j\
    \ + k] >= mod) buf[j + k] -= mod;\n        }\n      } else if(i == 4) {\n    \
    \    for(int k = 0; k < i; k += 4) {\n          auto a = _mm_loadu_si128((__m128i\
    \ *) (buf + j + k));\n          auto b = _mm_loadu_si128((__m128i *) (buf + j\
    \ + k + i));\n          a = _mm_add_epi32(a, b);\n          a = _mm_sub_epi32(a,\
    \ _mm_and_si128(_mm_cmpgt_epi32(a, m_mod_one2), m_mod2));\n          _mm_storeu_si128((__m128i\
    \ *) (buf + j + k), a);\n        }\n      } else {\n        for(int k = 0; k <\
    \ i; k += 8) {\n          auto a = _mm256_loadu_si256((__m256i *) (buf + j + k));\n\
    \          auto b = _mm256_loadu_si256((__m256i *) (buf + j + k + i));\n     \
    \     a = _mm256_add_epi32(a, b);\n          a = _mm256_sub_epi32(a, _mm256_and_si256(_mm256_cmpgt_epi32(a,\
    \ m_mod_one), m_mod));\n          _mm256_storeu_si256((__m256i *) (buf + j + k),\
    \ a);\n        }\n      }\n    }\n  }\n}\n\n\n__attribute__((target(\"avx2\")))\n\
    void superset_moebius_transform_simd(int *buf, int mod, int n) {\n  assert((n\
    \ & (n - 1)) == 0);\n  auto m_zero = _mm256_set1_epi32(0);\n  auto m_mod = _mm256_set1_epi32(mod);\n\
    \  auto m_zero2 = _mm_set1_epi32(0);\n  auto m_mod2 = _mm_set1_epi32(mod);\n \
    \ for(int i = 1; i < n; i <<= 1) {\n    for(int j = 0; j < n; j += i << 1) {\n\
    \      if(i <= 2) {\n        for(int k = 0; k < i; k++) {\n          buf[j + k]\
    \ += mod - buf[j + k + i];\n          if(buf[j + k] >= mod) buf[j + k] -= mod;\n\
    \        }\n      } else if(i == 4) {\n        for(int k = 0; k < i; k += 4) {\n\
    \          auto a = _mm_loadu_si128((__m128i * )(buf + j + k));\n          auto\
    \ b = _mm_loadu_si128((__m128i * )(buf + j + k + i));\n          a = _mm_sub_epi32(a,\
    \ b);\n          a = _mm_add_epi32(a, _mm_and_si128(_mm_cmpgt_epi32(m_zero2, a),\
    \ m_mod2));\n          _mm_storeu_si128((__m128i * )(buf + j + k), a);\n     \
    \   }\n      } else {\n        for(int k = 0; k < i; k += 8) {\n          auto\
    \ a = _mm256_loadu_si256((__m256i * )(buf + j + k));\n          auto b = _mm256_loadu_si256((__m256i\
    \ * )(buf + j + k + i));\n          a = _mm256_sub_epi32(a, b);\n          a =\
    \ _mm256_add_epi32(a, _mm256_and_si256(_mm256_cmpgt_epi32(m_zero, a), m_mod));\n\
    \          _mm256_storeu_si256((__m256i * )(buf + j + k), a);\n        }\n   \
    \   }\n    }\n  }\n}\n\ntemplate< int mod >\nint *bitwise_and_convolution_simd(int\
    \ *f, int *g, int n) {\n  assert((n & (n - 1)) == 0);\n  superset_zeta_transform_simd(f,\
    \ mod, n);\n  superset_zeta_transform_simd(g, mod, n);\n  for(int i = 0; i < n;\
    \ i++) f[i] = (1uLL * f[i] * g[i]) % mod;\n  superset_moebius_transform_simd(f,\
    \ mod, n);\n  return f;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fft/superset-zeta-moebius-transform-simd.cpp
  requiredBy: []
  timestamp: '2021-08-02 00:08:15+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-bitwise-and-convolution-2.test.cpp
documentation_of: math/fft/superset-zeta-moebius-transform-simd.cpp
layout: document
redirect_from:
- /library/math/fft/superset-zeta-moebius-transform-simd.cpp
- /library/math/fft/superset-zeta-moebius-transform-simd.cpp.html
title: "Superset Zeta/Moebius Transform SIMD (\u4E0A\u4F4D\u96C6\u5408\u306E\u30BC\
  \u30FC\u30BF/\u30E1\u30D3\u30A6\u30B9\u5909\u63DB, SIMD)"
---
