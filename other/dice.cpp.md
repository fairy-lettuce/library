---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"other/dice.cpp\"\nstruct Dice\n{\n  // int x, y;\n  int\
    \ l, r, f, b, d, u;\n\n  void RollN()\n  {\n    //  --y;\n    int buff = d;\n\
    \    d = f;\n    f = u;\n    u = b;\n    b = buff;\n  }\n\n  void RollS()\n  {\n\
    \    // ++y;\n    int buff = d;\n    d = b;\n    b = u;\n    u = f;\n    f = buff;\n\
    \  }\n\n  void RollL() // ----->\n  {\n    int buff = f;\n    f = l;\n    l =\
    \ b;\n    b = r;\n    r = buff;\n  }\n\n  void RollR() // <------\n  {\n    int\
    \ buff = f;\n    f = r;\n    r = b;\n    b = l;\n    l = buff;\n  }\n\n  void\
    \ RollE() // .o -> o.\n  {\n    // --x;\n    int buff = d;\n    d = l;\n    l\
    \ = u;\n    u = r;\n    r = buff;\n  }\n\n\n  void RollW() // o. -> .o\n  {\n\
    \    //  ++x;\n    int buff = d;\n    d = r;\n    r = u;\n    u = l;\n    l =\
    \ buff;\n  }\n\n\n  vector< Dice > makeDice()\n  {\n    vector< Dice > ret;\n\
    \    for(int i = 0; i < 6; i++) {\n      Dice d(*this);\n      if(i == 1) d.RollN();\n\
    \      if(i == 2) d.RollS();\n      if(i == 3) d.RollS(), d.RollS();\n      if(i\
    \ == 4) d.RollL();\n      if(i == 5) d.RollR();\n      for(int j = 0; j < 4; j++)\
    \ {\n        ret.emplace_back(d);\n        d.RollE();\n      }\n    }\n    return\
    \ (ret);\n  }\n};\n"
  code: "struct Dice\n{\n  // int x, y;\n  int l, r, f, b, d, u;\n\n  void RollN()\n\
    \  {\n    //  --y;\n    int buff = d;\n    d = f;\n    f = u;\n    u = b;\n  \
    \  b = buff;\n  }\n\n  void RollS()\n  {\n    // ++y;\n    int buff = d;\n   \
    \ d = b;\n    b = u;\n    u = f;\n    f = buff;\n  }\n\n  void RollL() // ----->\n\
    \  {\n    int buff = f;\n    f = l;\n    l = b;\n    b = r;\n    r = buff;\n \
    \ }\n\n  void RollR() // <------\n  {\n    int buff = f;\n    f = r;\n    r =\
    \ b;\n    b = l;\n    l = buff;\n  }\n\n  void RollE() // .o -> o.\n  {\n    //\
    \ --x;\n    int buff = d;\n    d = l;\n    l = u;\n    u = r;\n    r = buff;\n\
    \  }\n\n\n  void RollW() // o. -> .o\n  {\n    //  ++x;\n    int buff = d;\n \
    \   d = r;\n    r = u;\n    u = l;\n    l = buff;\n  }\n\n\n  vector< Dice > makeDice()\n\
    \  {\n    vector< Dice > ret;\n    for(int i = 0; i < 6; i++) {\n      Dice d(*this);\n\
    \      if(i == 1) d.RollN();\n      if(i == 2) d.RollS();\n      if(i == 3) d.RollS(),\
    \ d.RollS();\n      if(i == 4) d.RollL();\n      if(i == 5) d.RollR();\n     \
    \ for(int j = 0; j < 4; j++) {\n        ret.emplace_back(d);\n        d.RollE();\n\
    \      }\n    }\n    return (ret);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/dice.cpp
  requiredBy: []
  timestamp: '2019-07-20 01:29:30+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/dice.cpp
layout: document
redirect_from:
- /library/other/dice.cpp
- /library/other/dice.cpp.html
title: other/dice.cpp
---
