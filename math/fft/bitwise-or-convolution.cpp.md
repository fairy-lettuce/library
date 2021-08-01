---
data:
  _extendedDependsOn:
  - icon: ':warning:'
    path: math/fft/subset-zeta-moebius-transform.cpp
    title: "Subset Zeta/Moebius Transform (\u4E0B\u4F4D\u96C6\u5408\u306E\u30BC\u30FC\
      \u30BF/\u30E1\u30D3\u30A6\u30B9\u5909\u63DB)"
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: "Bitwise Or Convolution (Bitwise-OR\u7573\u307F\u8FBC\u307F)"
    links: []
  bundledCode: "#line 1 \"math/fft/subset-zeta-moebius-transform.cpp\"\n/**\n * @brief\
    \ Subset Zeta/Moebius Transform (\u4E0B\u4F4D\u96C6\u5408\u306E\u30BC\u30FC\u30BF\
    /\u30E1\u30D3\u30A6\u30B9\u5909\u63DB)\n */\ntemplate< typename T >\nvoid subset_zeta_transform(vector<\
    \ T > &f) {\n  const int n = (int) f.size();\n  assert((n & (n - 1)) == 0);\n\
    \  for(int i = 1; i < n; i <<= 1) {\n    for(int j = 0; j < n; j += i << 1) {\n\
    \      for(int k = 0; k < i; k++) {\n        f[j + k + i] += f[j + k];\n     \
    \ }\n    }\n  }\n}\n\ntemplate< typename T >\nvoid subset_moebius_transform(vector<\
    \ T > &f) {\n  const int n = (int) f.size();\n  assert((n & (n - 1)) == 0);\n\
    \  for(int i = 1; i < n; i <<= 1) {\n    for(int j = 0; j < n; j += i << 1) {\n\
    \      for(int k = 0; k < i; k++) {\n        f[j + k + i] -= f[j + k];\n     \
    \ }\n    }\n  }\n}\n#line 2 \"math/fft/bitwise-or-convolution.cpp\"\n\n/**\n *\
    \ @brief Bitwise Or Convolution (Bitwise-OR\u7573\u307F\u8FBC\u307F)\n */\ntemplate<\
    \ typename T >\nvector< T > bitwise_or_convolution(vector< T > f, vector< T >\
    \ g) {\n  const int n = (int) f.size();\n  assert(f.size() == g.size());\n  assert((n\
    \ & (n - 1)) == 0);\n  subset_zeta_transform(f);\n  subset_zeta_transform(g);\n\
    \  for(int i = 0; i < n; i++) f[i] *= g[i];\n  subset_moebius_transform(f);\n\
    \  return f;\n}\n"
  code: "#include \"subset-zeta-moebius-transform.cpp\"\n\n/**\n * @brief Bitwise\
    \ Or Convolution (Bitwise-OR\u7573\u307F\u8FBC\u307F)\n */\ntemplate< typename\
    \ T >\nvector< T > bitwise_or_convolution(vector< T > f, vector< T > g) {\n  const\
    \ int n = (int) f.size();\n  assert(f.size() == g.size());\n  assert((n & (n -\
    \ 1)) == 0);\n  subset_zeta_transform(f);\n  subset_zeta_transform(g);\n  for(int\
    \ i = 0; i < n; i++) f[i] *= g[i];\n  subset_moebius_transform(f);\n  return f;\n\
    }\n"
  dependsOn:
  - math/fft/subset-zeta-moebius-transform.cpp
  isVerificationFile: false
  path: math/fft/bitwise-or-convolution.cpp
  requiredBy: []
  timestamp: '2021-08-01 19:41:34+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fft/bitwise-or-convolution.cpp
layout: document
redirect_from:
- /library/math/fft/bitwise-or-convolution.cpp
- /library/math/fft/bitwise-or-convolution.cpp.html
title: "Bitwise Or Convolution (Bitwise-OR\u7573\u307F\u8FBC\u307F)"
---
