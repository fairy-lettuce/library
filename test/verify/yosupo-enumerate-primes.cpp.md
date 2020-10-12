---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links:
    - https://judge.yosupo.jp/problem/enumerate_primes
  bundledCode: "Traceback (most recent call last):\n  File \"/opt/hostedtoolcache/Python/3.8.6/x64/lib/python3.8/site-packages/onlinejudge_verify/documentation/build.py\"\
    , line 71, in _render_source_code_stat\n    bundled_code = language.bundle(stat.path,\
    \ basedir=basedir).decode()\n  File \"/opt/hostedtoolcache/Python/3.8.6/x64/lib/python3.8/site-packages/onlinejudge_verify/languages/cplusplus.py\"\
    , line 191, in bundle\n    bundler.update(path)\n  File \"/opt/hostedtoolcache/Python/3.8.6/x64/lib/python3.8/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 399, in update\n    self.update(self._resolve(pathlib.Path(included), included_from=path))\n\
    \  File \"/opt/hostedtoolcache/Python/3.8.6/x64/lib/python3.8/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 258, in _resolve\n    raise BundleErrorAt(path, -1, \"no such header\"\
    )\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt: ../../math/number-theory/enumerate-prime.cpp:\
    \ line -1: no such header\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/enumerate_primes\"\n\n\
    #include \"../../template/template.cpp\"\n\n#include \"../../math/number-theory/enumerate-prime.cpp\"\
    \n\nint main() {\n  int N, A, B;\n  cin >> N >> A >> B;\n  auto d = enumerate_primes(N);\n\
    \  vector< int > ans;\n  for(int i = B; i < d.size(); i += A) {\n    ans.emplace_back(d[i]);\n\
    \  }\n  cout << d.size() << \" \" << ans.size() << \"\\n\";\n  cout << ans <<\
    \ \"\\n\";\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/yosupo-enumerate-primes.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/yosupo-enumerate-primes.cpp
layout: document
redirect_from:
- /library/test/verify/yosupo-enumerate-primes.cpp
- /library/test/verify/yosupo-enumerate-primes.cpp.html
title: test/verify/yosupo-enumerate-primes.cpp
---
