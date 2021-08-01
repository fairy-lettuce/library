---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/fft/superset-zeta-moebius-transform.cpp
    title: "Superset Zeta/Moebius Transform (\u4E0A\u4F4D\u96C6\u5408\u306E\u30BC\u30FC\
      \u30BF/\u30E1\u30D3\u30A6\u30B9\u5909\u63DB)"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bitwise-and-convolution.test.cpp
    title: test/verify/yosupo-bitwise-and-convolution.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Bitwise And Convolution (Bitwise-AND\u7573\u307F\u8FBC\u307F)"
    links: []
  bundledCode: "#line 1 \"math/fft/superset-zeta-moebius-transform.cpp\"\n/**\n *\
    \ @brief Superset Zeta/Moebius Transform (\u4E0A\u4F4D\u96C6\u5408\u306E\u30BC\
    \u30FC\u30BF/\u30E1\u30D3\u30A6\u30B9\u5909\u63DB)\n */\ntemplate< typename T\
    \ >\nvoid superset_zeta_transform(vector< T > &f) {\n  const int n = (int) f.size();\n\
    \  assert((n & (n - 1)) == 0);\n  for(int i = 1; i < n; i <<= 1) {\n    for(int\
    \ j = 0; j < n; j += i << 1) {\n      for(int k = 0; k < i; k++) {\n        f[j\
    \ + k] += f[j + k + i];\n      }\n    }\n  }\n}\n\ntemplate< typename T >\nvoid\
    \ superset_moebius_transform(vector< T > &f) {\n  const int n = (int) f.size();\n\
    \  assert((n & (n - 1)) == 0);\n  for(int i = 1; i < n; i <<= 1) {\n    for(int\
    \ j = 0; j < n; j += i << 1) {\n      for(int k = 0; k < i; k++) {\n        f[j\
    \ + k] -= f[j + k + i];\n      }\n    }\n  }\n}\n#line 2 \"math/fft/bitwise-and-convolution.cpp\"\
    \n\n/**\n * @brief Bitwise And Convolution (Bitwise-AND\u7573\u307F\u8FBC\u307F\
    )\n */\ntemplate< typename T >\nvector< T > bitwise_and_convolution(vector< T\
    \ > f, vector< T > g) {\n  const int n = (int) f.size();\n  assert(f.size() ==\
    \ g.size());\n  assert((n & (n - 1)) == 0);\n  superset_zeta_transform(f);\n \
    \ superset_zeta_transform(g);\n  for(int i = 0; i < n; i++) f[i] *= g[i];\n  superset_moebius_transform(f);\n\
    \  return f;\n}\n"
  code: "#include \"superset-zeta-moebius-transform.cpp\"\n\n/**\n * @brief Bitwise\
    \ And Convolution (Bitwise-AND\u7573\u307F\u8FBC\u307F)\n */\ntemplate< typename\
    \ T >\nvector< T > bitwise_and_convolution(vector< T > f, vector< T > g) {\n \
    \ const int n = (int) f.size();\n  assert(f.size() == g.size());\n  assert((n\
    \ & (n - 1)) == 0);\n  superset_zeta_transform(f);\n  superset_zeta_transform(g);\n\
    \  for(int i = 0; i < n; i++) f[i] *= g[i];\n  superset_moebius_transform(f);\n\
    \  return f;\n}\n"
  dependsOn:
  - math/fft/superset-zeta-moebius-transform.cpp
  isVerificationFile: false
  path: math/fft/bitwise-and-convolution.cpp
  requiredBy: []
  timestamp: '2021-08-01 19:41:34+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-bitwise-and-convolution.test.cpp
documentation_of: math/fft/bitwise-and-convolution.cpp
layout: document
redirect_from:
- /library/math/fft/bitwise-and-convolution.cpp
- /library/math/fft/bitwise-and-convolution.cpp.html
title: "Bitwise And Convolution (Bitwise-AND\u7573\u307F\u8FBC\u307F)"
---
