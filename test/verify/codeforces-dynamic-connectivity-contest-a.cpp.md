---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"test/verify/codeforces-dynamic-connectivity-contest-a.cpp\"\
    \n#define IGNORE\n\nint main() {\n  FILE *in, *out;\n  in = fopen(\"connect.in\"\
    , \"r\");\n  out = fopen(\"connect.out\", \"w\");\n\n  int N, Q;\n  fscanf(in,\
    \ \"%d %d\", &N, &Q);\n  OfflineDynamicConnectivity odc(N, Q);\n  vector< char\
    \ > T(Q);\n  for(int i = 0; i < Q; i++) {\n    fscanf(in, \" %c\", &T[i]);\n \
    \   if(T[i] == '+' || T[i] == '-') {\n      int x, y;\n      fscanf(in, \"%d %d\"\
    , &x, &y);\n      --x, --y;\n      if(T[i] == '+') odc.insert(i, x, y);\n    \
    \  else odc.erase(i, x, y);\n    }\n  }\n  odc.build();\n  odc.run([&](int k)\
    \ {\n    if(T[k] == '?') fprintf(out, \"%d\\n\", odc.comp);\n  });\n}\n\n"
  code: "#define IGNORE\n\nint main() {\n  FILE *in, *out;\n  in = fopen(\"connect.in\"\
    , \"r\");\n  out = fopen(\"connect.out\", \"w\");\n\n  int N, Q;\n  fscanf(in,\
    \ \"%d %d\", &N, &Q);\n  OfflineDynamicConnectivity odc(N, Q);\n  vector< char\
    \ > T(Q);\n  for(int i = 0; i < Q; i++) {\n    fscanf(in, \" %c\", &T[i]);\n \
    \   if(T[i] == '+' || T[i] == '-') {\n      int x, y;\n      fscanf(in, \"%d %d\"\
    , &x, &y);\n      --x, --y;\n      if(T[i] == '+') odc.insert(i, x, y);\n    \
    \  else odc.erase(i, x, y);\n    }\n  }\n  odc.build();\n  odc.run([&](int k)\
    \ {\n    if(T[k] == '?') fprintf(out, \"%d\\n\", odc.comp);\n  });\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/codeforces-dynamic-connectivity-contest-a.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/codeforces-dynamic-connectivity-contest-a.cpp
layout: document
redirect_from:
- /library/test/verify/codeforces-dynamic-connectivity-contest-a.cpp
- /library/test/verify/codeforces-dynamic-connectivity-contest-a.cpp.html
title: test/verify/codeforces-dynamic-connectivity-contest-a.cpp
---
