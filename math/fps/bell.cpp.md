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
  bundledCode: "Traceback (most recent call last):\n  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/documentation/build.py\"\
    , line 71, in _render_source_code_stat\n    bundled_code = language.bundle(stat.path,\
    \ basedir=basedir, options={'include_paths': [basedir]}).decode()\n  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus.py\"\
    , line 187, in bundle\n    bundler.update(path)\n  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 401, in update\n    self.update(self._resolve(pathlib.Path(included), included_from=path))\n\
    \  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 260, in _resolve\n    raise BundleErrorAt(path, -1, \"no such header\"\
    )\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt: exp.cpp: line\
    \ -1: no such header\n"
  code: "#pragma once\n#include \"formal-power-series.cpp\"\n#include \"exp.cpp\"\n\
    \ntemplate< typename T >\nFormalPowerSeries< T > bell(int N) {\n  FormalPowerSeries<\
    \ T > poly(N + 1), ret(N + 1);\n  poly[1] = 1;\n  poly = poly.exp();\n  poly[0]\
    \ -= 1;\n  poly = poly.exp();\n  T mul = 1;\n  for(int i = 0; i <= N; i++) {\n\
    \    ret[i] = poly[i] * mul;\n    mul *= i + 1;\n  }\n  return ret;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/bell.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/bell.cpp
layout: document
redirect_from:
- /library/math/fps/bell.cpp
- /library/math/fps/bell.cpp.html
title: math/fps/bell.cpp
---
