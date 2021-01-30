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
  bundledCode: "#line 1 \"other/chrono-timer.cpp\"\nstruct ChronoTimer {\n  chrono::high_resolution_clock::time_point\
    \ st;\n\n  ChronoTimer() { reset(); }\n\n  void reset() {\n    st = chrono::high_resolution_clock::now();\n\
    \  }\n\n  chrono::milliseconds::rep elapsed() {\n    auto ed = chrono::high_resolution_clock::now();\n\
    \    return chrono::duration_cast< chrono::milliseconds >(ed - st).count();\n\
    \  }\n};\n"
  code: "struct ChronoTimer {\n  chrono::high_resolution_clock::time_point st;\n\n\
    \  ChronoTimer() { reset(); }\n\n  void reset() {\n    st = chrono::high_resolution_clock::now();\n\
    \  }\n\n  chrono::milliseconds::rep elapsed() {\n    auto ed = chrono::high_resolution_clock::now();\n\
    \    return chrono::duration_cast< chrono::milliseconds >(ed - st).count();\n\
    \  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/chrono-timer.cpp
  requiredBy: []
  timestamp: '2020-06-30 02:21:44+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/chrono-timer.cpp
layout: document
redirect_from:
- /library/other/chrono-timer.cpp
- /library/other/chrono-timer.cpp.html
title: other/chrono-timer.cpp
---
