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
    )\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt: inv.cpp: line\
    \ -1: no such header\n"
  code: "#include \"formal-power-series.cpp\"\n#include \"inv.cpp\"\n\ntemplate< typename\
    \ T >\nstruct PolyBuf {\n  using FPS = FormalPowerSeries< T >;\n  const FPS xs;\n\
    \  using pi = pair< int, int >;\n  map< pi, FPS > buf;\n\n  PolyBuf(const FPS\
    \ &xs) : xs(xs) {}\n\n  const FPS &query(int l, int r) {\n    if(buf.count({l,\
    \ r})) return buf[{l, r}];\n    if(l + 1 == r) return buf[{l, r}] = {-xs[l], 1};\n\
    \    return buf[{l, r}] = query(l, (l + r) >> 1) * query((l + r) >> 1, r);\n \
    \ }\n};\n\n\ntemplate< typename T >\nFormalPowerSeries< T > multipoint_evaluation(const\
    \ FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs, PolyBuf< T > &buf)\
    \ {\n  using FPS = FormalPowerSeries< T >;\n  FPS ret;\n  const int B = 64;\n\
    \  function< void(FPS, int, int) > rec = [&](FPS a, int l, int r) -> void {\n\
    \    a %= buf.query(l, r);\n    if(a.size() <= B) {\n      for(int i = l; i <\
    \ r; i++) ret.emplace_back(a(xs[i]));\n      return;\n    }\n    rec(a, l, (l\
    \ + r) >> 1);\n    rec(a, (l + r) >> 1, r);\n  };\n  rec(as, 0, xs.size());\n\
    \  return ret;\n};\n\ntemplate< typename T >\nFormalPowerSeries< T > multipoint_evaluation(const\
    \ FormalPowerSeries< T > &as, const FormalPowerSeries< T > &xs) {\n  PolyBuf<\
    \ T > buff(xs);\n  return multipoint_evaluation(as, xs, buff);\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: math/fps/multipoint-evaluation.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: math/fps/multipoint-evaluation.cpp
layout: document
redirect_from:
- /library/math/fps/multipoint-evaluation.cpp
- /library/math/fps/multipoint-evaluation.cpp.html
title: math/fps/multipoint-evaluation.cpp
---
