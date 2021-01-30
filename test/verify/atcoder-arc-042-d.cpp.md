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
  bundledCode: "#line 1 \"test/verify/atcoder-arc-042-d.cpp\"\n#define IGNORE\n\n\
    int64_t mod_pow(int64_t x, int64_t n, int64_t mod) {\n  int64_t ret = 1;\n  while(n\
    \ > 0) {\n    if(n & 1) (ret *= x) %= mod;\n    (x *= x) %= mod;\n    n >>= 1;\n\
    \  }\n  return ret;\n}\n\nint main() {\n  int x, p, a, b;\n  cin >> x >> p >>\
    \ a >> b;\n\n  if(p <= a) {\n    int k = a / p;\n    a -= k * p;\n    b -= k *\
    \ p;\n  }\n\n  if((b - a + 1) <= 10000000) {\n    int64_t ret = infll;\n    auto\
    \ tmp = mod_pow(x, a, p);\n    for(int i = a; i <= b; i++) {\n      ret = min(ret,\
    \ tmp);\n      tmp = tmp * x % p;\n    }\n    cout << ret << endl;\n  } else {\n\
    \    for(int i = 1;; i++) {\n      int tmp = mod_log(x, i, p);\n      if((a <=\
    \ tmp && tmp <= b) || (a <= tmp + p && tmp + p <= b)) {\n        cout << i <<\
    \ endl;\n        break;\n      }\n    }\n  }\n}\n\n"
  code: "#define IGNORE\n\nint64_t mod_pow(int64_t x, int64_t n, int64_t mod) {\n\
    \  int64_t ret = 1;\n  while(n > 0) {\n    if(n & 1) (ret *= x) %= mod;\n    (x\
    \ *= x) %= mod;\n    n >>= 1;\n  }\n  return ret;\n}\n\nint main() {\n  int x,\
    \ p, a, b;\n  cin >> x >> p >> a >> b;\n\n  if(p <= a) {\n    int k = a / p;\n\
    \    a -= k * p;\n    b -= k * p;\n  }\n\n  if((b - a + 1) <= 10000000) {\n  \
    \  int64_t ret = infll;\n    auto tmp = mod_pow(x, a, p);\n    for(int i = a;\
    \ i <= b; i++) {\n      ret = min(ret, tmp);\n      tmp = tmp * x % p;\n    }\n\
    \    cout << ret << endl;\n  } else {\n    for(int i = 1;; i++) {\n      int tmp\
    \ = mod_log(x, i, p);\n      if((a <= tmp && tmp <= b) || (a <= tmp + p && tmp\
    \ + p <= b)) {\n        cout << i << endl;\n        break;\n      }\n    }\n \
    \ }\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-arc-042-d.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-arc-042-d.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-arc-042-d.cpp
- /library/test/verify/atcoder-arc-042-d.cpp.html
title: test/verify/atcoder-arc-042-d.cpp
---
