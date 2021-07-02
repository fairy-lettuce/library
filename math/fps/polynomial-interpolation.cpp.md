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
    , line 401, in update\n    self.update(self._resolve(pathlib.Path(included), included_from=path))\n\
    \  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 260, in _resolve\n    raise BundleErrorAt(path, -1, \"no such header\"\
    )\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt: inv.cpp: line\
    \ -1: no such header\n"
  code: "#include \"multipoint-evaluation.cpp\"\n#include \"diff.cpp\"\n\ntemplate<\
    \ class T >\nFormalPowerSeries< T > polynomial_interpolation(const FormalPowerSeries<\
    \ T > &xs, const vector< T > &ys) {\n  assert(xs.size() == ys.size());\n  using\
    \ FPS = FormalPowerSeries< T >;\n  PolyBuf< T > buf(xs);\n  FPS w = buf.query(0,\
    \ xs.size()).diff();\n  auto vs = multipoint_evaluation(w, xs, buf);\n  function<\
    \ FPS(int, int) > rec = [&](int l, int r) -> FPS {\n    if(r - l == 1) return\
    \ {ys[l] / vs[l]};\n    int m = (l + r) >> 1;\n    return rec(l, m) * buf.query(m,\
    \ r) + rec(m, r) * buf.query(l, m);\n  };\n  return rec(0, xs.size());\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/polynomial-interpolation.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/polynomial-interpolation.cpp
layout: document
redirect_from:
- /library/math/fps/polynomial-interpolation.cpp
- /library/math/fps/polynomial-interpolation.cpp.html
title: math/fps/polynomial-interpolation.cpp
---
