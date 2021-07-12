---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/flow/bipartite-matching.hpp
    title: "Bipartite-Matching(\u4E8C\u90E8\u30B0\u30E9\u30D5\u306E\u6700\u5927\u30DE\
      \u30C3\u30C1\u30F3\u30B0)"
  - icon: ':heavy_check_mark:'
    path: graph/graph-template.hpp
    title: graph/graph-template.hpp
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_7_A
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_7_A
  bundledCode: "Traceback (most recent call last):\n  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/documentation/build.py\"\
    , line 71, in _render_source_code_stat\n    bundled_code = language.bundle(stat.path,\
    \ basedir=basedir, options={'include_paths': [basedir]}).decode()\n  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus.py\"\
    , line 187, in bundle\n    bundler.update(path)\n  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 401, in update\n    self.update(self._resolve(pathlib.Path(included), included_from=path))\n\
    \  File \"/opt/hostedtoolcache/Python/3.9.5/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/cplusplus_bundle.py\"\
    , line 312, in update\n    raise BundleErrorAt(path, i + 1, \"#pragma once found\
    \ in a non-first line\")\nonlinejudge_verify.languages.cplusplus_bundle.BundleErrorAt:\
    \ graph/flow/bipartite-matching.hpp: line 5: #pragma once found in a non-first\
    \ line\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_7_A\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../graph/flow/bipartite-matching.hpp\"\
    \n\nint main() {\n  int X, Y, E;\n  scanf(\"%d %d %d\", &X, &Y, &E);\n  BipartiteMatching\
    \ bm(X + Y);\n  for(int i = 0; i < E; i++) {\n    int a, b;\n    scanf(\"%d %d\"\
    , &a, &b);\n    bm.add_edge(a, X + b);\n  }\n  printf(\"%d\\n\", bm.bipartite_matching());\n\
    }\n"
  dependsOn:
  - template/template.cpp
  - graph/flow/bipartite-matching.hpp
  - graph/graph-template.hpp
  isVerificationFile: true
  path: test/verify/aoj-grl-7-a.test.cpp
  requiredBy: []
  timestamp: '2021-07-01 02:53:34+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-grl-7-a.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-grl-7-a.test.cpp
- /verify/test/verify/aoj-grl-7-a.test.cpp.html
title: test/verify/aoj-grl-7-a.test.cpp
---
