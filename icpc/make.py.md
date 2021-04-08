---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: py
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "Traceback (most recent call last):\n  File \"/opt/hostedtoolcache/Python/3.9.4/x64/lib/python3.9/site-packages/onlinejudge_verify/documentation/build.py\"\
    , line 71, in _render_source_code_stat\n    bundled_code = language.bundle(stat.path,\
    \ basedir=basedir, options={'include_paths': [basedir]}).decode()\n  File \"/opt/hostedtoolcache/Python/3.9.4/x64/lib/python3.9/site-packages/onlinejudge_verify/languages/python.py\"\
    , line 96, in bundle\n    raise NotImplementedError\nNotImplementedError\n"
  code: "import os\n\nprint(\"ICPC Library @ tapu\")\n\nfor f in os.listdir(\"..\"\
    ):\n  if not os.path.isdir(\"../\"+f):\n    continue\n  if f[0] == '.':\n    continue\n\
    \  if f == \"icpc\":\n    continue\n\n  print(\"-\"*50)\n  l = (50 - len(f)-2)//2\n\
    \  r = (50 - len(f)-2)-l\n  print(\"|\"+\" \"*l+f+\" \"*r+\"|\")\n  print(\"-\"\
    *50)\n  print()\n\n  for g in os.listdir(\"../\"+f):\n   name = g\n   fp = \"\
    ../\" + f + \"/\" + g\n   if not os.path.isfile(fp):\n     continue\n\n   print(\"\
    #\"*50)\n\n   l = (50-len(name)-2)//2\n   r = (50-len(name)-2)-l\n\n   print(\"\
    #\"*l+\" \"+name+\" \"+\"#\"*r)\n   print(\"#\"*50)\n   print(\"\")\n   with open(fp)\
    \ as tap:\n     print(tap.read())\n   print(\"\")\n"
  dependsOn: []
  isVerificationFile: false
  path: icpc/make.py
  requiredBy: []
  timestamp: '1970-01-01 00:00:00+00:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: icpc/make.py
layout: document
redirect_from:
- /library/icpc/make.py
- /library/icpc/make.py.html
title: icpc/make.py
---
