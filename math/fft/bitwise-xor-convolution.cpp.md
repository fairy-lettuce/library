---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/fft/fast-walsh-hadamard-transform.cpp
    title: "Fast Walsh Hadamard Transform (\u9AD8\u901F\u30A6\u30A9\u30EB\u30B7\u30E5\
      \u30A2\u30C0\u30DE\u30FC\u30EB\u5909\u63DB)"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/yosupo-bitwise-xor-convolution.test.cpp
    title: test/verify/yosupo-bitwise-xor-convolution.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Bitwise Xor Convolution (Bitwise-XOR\u7573\u307F\u8FBC\u307F)"
    links: []
  bundledCode: "#line 1 \"math/fft/fast-walsh-hadamard-transform.cpp\"\n/**\n * @brief\
    \ Fast Walsh Hadamard Transform (\u9AD8\u901F\u30A6\u30A9\u30EB\u30B7\u30E5\u30A2\
    \u30C0\u30DE\u30FC\u30EB\u5909\u63DB)\n */\ntemplate< typename T >\nvoid fast_walsh_hadamard_transform(vector<\
    \ T > &f, bool inv = false) {\n  const int n = (int) f.size();\n  assert((n &\
    \ (n - 1)) == 0);\n  for(int i = 1; i < n; i <<= 1) {\n    for(int j = 0; j <\
    \ n; j += i << 1) {\n      for(int k = 0; k < i; k++) {\n        T s = f[j + k],\
    \ t = f[j + k + i];\n        f[j + k] = s + t;\n        f[j + k + i] = s - t;\n\
    \      }\n    }\n  }\n  if(inv) {\n    T inv_n = T(1) / n;\n    for(auto &x :\
    \ f) x *= inv_n;\n  }\n}\n#line 2 \"math/fft/bitwise-xor-convolution.cpp\"\n\n\
    /**\n * @brief Bitwise Xor Convolution (Bitwise-XOR\u7573\u307F\u8FBC\u307F)\n\
    \ */\ntemplate< typename T >\nvector< T > bitwise_xor_convolution(vector< T >\
    \ f, vector< T > g) {\n  const int n = (int) f.size();\n  assert(f.size() == g.size());\n\
    \  assert((n & (n - 1)) == 0);\n  fast_walsh_hadamard_transform(f, false);\n \
    \ fast_walsh_hadamard_transform(g, false);\n  for(int i = 0; i < n; i++) f[i]\
    \ *= g[i];\n  fast_walsh_hadamard_transform(f, true);\n  return f;\n}\n"
  code: "#include \"fast-walsh-hadamard-transform.cpp\"\n\n/**\n * @brief Bitwise\
    \ Xor Convolution (Bitwise-XOR\u7573\u307F\u8FBC\u307F)\n */\ntemplate< typename\
    \ T >\nvector< T > bitwise_xor_convolution(vector< T > f, vector< T > g) {\n \
    \ const int n = (int) f.size();\n  assert(f.size() == g.size());\n  assert((n\
    \ & (n - 1)) == 0);\n  fast_walsh_hadamard_transform(f, false);\n  fast_walsh_hadamard_transform(g,\
    \ false);\n  for(int i = 0; i < n; i++) f[i] *= g[i];\n  fast_walsh_hadamard_transform(f,\
    \ true);\n  return f;\n}\n"
  dependsOn:
  - math/fft/fast-walsh-hadamard-transform.cpp
  isVerificationFile: false
  path: math/fft/bitwise-xor-convolution.cpp
  requiredBy: []
  timestamp: '2021-08-01 19:15:32+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/yosupo-bitwise-xor-convolution.test.cpp
documentation_of: math/fft/bitwise-xor-convolution.cpp
layout: document
redirect_from:
- /library/math/fft/bitwise-xor-convolution.cpp
- /library/math/fft/bitwise-xor-convolution.cpp.html
title: "Bitwise Xor Convolution (Bitwise-XOR\u7573\u307F\u8FBC\u307F)"
---
