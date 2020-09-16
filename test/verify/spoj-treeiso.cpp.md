---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    IGNORE: ''
    IGNORE_IF_CLANG: ''
    IGNORE_IF_GCC: ''
    links: []
  bundledCode: "#line 1 \"test/verify/spoj-treeiso.cpp\"\n#define IGNORE\n\nint main()\
    \ {\n  int T;\n  cin >> T;\n  while(T--) {\n    int N;\n    cin >> N;\n    UnWeightedGraph\
    \ x(N), y(N);\n    for(int i = 1; i < N; i++) {\n      int a, b;\n      cin >>\
    \ a >> b;\n      --a, --b;\n      x[a].emplace_back(b);\n      x[b].emplace_back(a);\n\
    \    }\n    for(int i = 1; i < N; i++) {\n      int a, b;\n      cin >> a >> b;\n\
    \      --a, --b;\n      y[a].emplace_back(b);\n      y[b].emplace_back(a);\n \
    \   }\n    if(tree_isomorphism(x, y)) cout << \"YES\\n\";\n    else cout << \"\
    NO\\n\";\n  }\n}\n"
  code: "#define IGNORE\n\nint main() {\n  int T;\n  cin >> T;\n  while(T--) {\n \
    \   int N;\n    cin >> N;\n    UnWeightedGraph x(N), y(N);\n    for(int i = 1;\
    \ i < N; i++) {\n      int a, b;\n      cin >> a >> b;\n      --a, --b;\n    \
    \  x[a].emplace_back(b);\n      x[b].emplace_back(a);\n    }\n    for(int i =\
    \ 1; i < N; i++) {\n      int a, b;\n      cin >> a >> b;\n      --a, --b;\n \
    \     y[a].emplace_back(b);\n      y[b].emplace_back(a);\n    }\n    if(tree_isomorphism(x,\
    \ y)) cout << \"YES\\n\";\n    else cout << \"NO\\n\";\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/spoj-treeiso.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/spoj-treeiso.cpp
layout: document
redirect_from:
- /library/test/verify/spoj-treeiso.cpp
- /library/test/verify/spoj-treeiso.cpp.html
title: test/verify/spoj-treeiso.cpp
---
