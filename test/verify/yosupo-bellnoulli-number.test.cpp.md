---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes: {}
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
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/bernoulli_number\"\n\n\
    #include \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/mod-int.cpp\"\
    \n#include \"../../math/fft/number-theoretic-transform-friendly-mod-int.cpp\"\n\
    \n#include \"../../math/fps/bellnoulli.cpp\"\n\nconst int MOD = 998244353;\nusing\
    \ mint = ModInt< MOD >;\n\nint main() {\n  NumberTheoreticTransformFriendlyModInt<\
    \ mint > ntt;\n  using FPS = FormalPowerSeries< mint >;\n  FPS::set_fft([&](FPS\
    \ &a) { ntt.ntt(a); }, [&](FPS &a) { ntt.intt(a); });\n\n  int N;\n  cin >> N;\n\
    \  cout << bellnoulli< mint >(N) << endl;\n}\n\n"
  dependsOn: []
  isVerificationFile: true
  path: test/verify/yosupo-bellnoulli-number.test.cpp
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: TEST_WRONG_ANSWER
  verifiedWith: []
documentation_of: test/verify/yosupo-bellnoulli-number.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-bellnoulli-number.test.cpp
- /verify/test/verify/yosupo-bellnoulli-number.test.cpp.html
title: test/verify/yosupo-bellnoulli-number.test.cpp
---
