---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes: {}
  bundledCode: "Traceback (most recent call last):\n  File \"/opt/hostedtoolcache/Python/3.9.6/x64/lib/python3.9/site-packages/onlinejudge_verify/documentation/build.py\"\
    , line 71, in _render_source_code_stat\n    bundled_code = language.bundle(stat.path,\
    \ basedir=basedir, options={'include_paths': [basedir]}).decode()\n  File \"/opt/hostedtoolcache/Python/3.9.6/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus.py\"\
    , line 187, in bundle\n    bundler.update(path)\n  File \"/opt/hostedtoolcache/Python/3.9.6/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 401, in update\n    self.update(self._resolve(pathlib.Path(included), included_from=path))\n\
    \  File \"/opt/hostedtoolcache/Python/3.9.6/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 260, in _resolve\n    raise BundleErrorAt(path, -1, \"no such header\"\
    )\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt: ../../math/number-theory/kth-root.cpp:\
    \ line -1: no such header\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/counting_primes\"\n\n#include\
    \ \"../../template/template.cpp\"\n\n#include \"../../math/number-theory/kth-root.cpp\"\
    \n#include \"../../math/number-theory/prime-table.cpp\"\n#include \"../../math/number-theory/prime-count.cpp\"\
    \n\nint main() {\n  int64_t n;\n  cin >> n;\n  PrimeCount<> pc;\n  cout << pc.pi(n)\
    \ << \"\\n\";\n}\n"
  dependsOn: []
  isVerificationFile: true
  path: test/verify/yosupo-counting-primes.test.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: TEST_WRONG_ANSWER
  verifiedWith: []
documentation_of: test/verify/yosupo-counting-primes.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-counting-primes.test.cpp
- /verify/test/verify/yosupo-counting-primes.test.cpp.html
title: test/verify/yosupo-counting-primes.test.cpp
---
