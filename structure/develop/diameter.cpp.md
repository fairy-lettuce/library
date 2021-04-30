---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':x:'
    path: test/verify/aoj-grl-5-a-2.test.cpp
    title: test/verify/aoj-grl-5-a-2.test.cpp
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/develop/diameter.cpp\"\ntemplate< typename T >\n\
    struct Diameter {\n\n  using key_t = pair< bool, T >;\n  static const T inf =\
    \ numeric_limits< T >::max() / 3;\n\n  struct light_t {\n    T val, dia;\n\n \
    \   T top1, top2;\n    T diameter;\n\n    light_t() : top1(-inf), top2(-inf),\
    \ diameter(-inf) {}\n\n    void set_sum() {\n      top1 = val;\n      top2 = -inf;\n\
    \      diameter = dia;\n    }\n\n    void update(const light_t &p) {\n      if(top1\
    \ < p.top1) {\n        top2 = top1;\n        top1 = p.top1;\n        if(top2 <\
    \ p.top2) {\n          top2 = p.top2;\n        }\n      } else if(top2 < p.top1)\
    \ {\n        top2 = p.top1;\n      }\n      if(diameter < p.diameter) {\n    \
    \    diameter = p.diameter;\n      }\n    }\n  };\n\n  struct heavy_t {\n    bool\
    \ vertex;\n    T key;\n\n    T all, p_len, c_len, diameter;\n\n    heavy_t() :\
    \ all(0), p_len(-inf), c_len(-inf), diameter(-inf) {}\n\n    void set_key(const\
    \ key_t &x) {\n      vertex = x.first;\n      key = x.second;\n    }\n\n    void\
    \ update(const heavy_t &p, const heavy_t &c, const light_t &l) {\n      if(vertex)\
    \ {\n        all = p.all + c.all;\n        p_len = max({c.p_len, max(l.top1, p.p_len)\
    \ + c.all, -inf});\n        c_len = max({p.c_len, max(l.top1, c.c_len) + p.all,\
    \ -inf});\n        diameter = max({p.diameter, c.diameter, p.p_len + max(l.top1,\
    \ c.c_len), c.c_len + l.top1, l.top1 + l.top2, l.diameter, -inf});\n        if(key)\
    \ {\n          p_len = max(p_len, c.all);\n          c_len = max(c_len, p.all);\n\
    \          diameter = max({diameter, p.p_len, c.c_len, l.top1, T(0)});\n     \
    \   }\n      } else {\n        all = p.all + c.all + key;\n        p_len = max({c.p_len,\
    \ max(l.top1, p.p_len) + key + c.all, -inf});\n        c_len = max({p.c_len, max(l.top1,\
    \ c.c_len) + key + p.all, -inf});\n        diameter = max({p.diameter, c.diameter,\
    \ p.p_len + max(l.top1, c.c_len) + key, c.c_len + l.top1 + key, l.top1 + l.top2\
    \ + key, l.diameter, -inf});\n      }\n    }\n\n    light_t add() const {\n  \
    \    light_t x;\n      x.val = c_len;\n      x.dia = diameter;\n      return x;\n\
    \    }\n  };\n};\n"
  code: "template< typename T >\nstruct Diameter {\n\n  using key_t = pair< bool,\
    \ T >;\n  static const T inf = numeric_limits< T >::max() / 3;\n\n  struct light_t\
    \ {\n    T val, dia;\n\n    T top1, top2;\n    T diameter;\n\n    light_t() :\
    \ top1(-inf), top2(-inf), diameter(-inf) {}\n\n    void set_sum() {\n      top1\
    \ = val;\n      top2 = -inf;\n      diameter = dia;\n    }\n\n    void update(const\
    \ light_t &p) {\n      if(top1 < p.top1) {\n        top2 = top1;\n        top1\
    \ = p.top1;\n        if(top2 < p.top2) {\n          top2 = p.top2;\n        }\n\
    \      } else if(top2 < p.top1) {\n        top2 = p.top1;\n      }\n      if(diameter\
    \ < p.diameter) {\n        diameter = p.diameter;\n      }\n    }\n  };\n\n  struct\
    \ heavy_t {\n    bool vertex;\n    T key;\n\n    T all, p_len, c_len, diameter;\n\
    \n    heavy_t() : all(0), p_len(-inf), c_len(-inf), diameter(-inf) {}\n\n    void\
    \ set_key(const key_t &x) {\n      vertex = x.first;\n      key = x.second;\n\
    \    }\n\n    void update(const heavy_t &p, const heavy_t &c, const light_t &l)\
    \ {\n      if(vertex) {\n        all = p.all + c.all;\n        p_len = max({c.p_len,\
    \ max(l.top1, p.p_len) + c.all, -inf});\n        c_len = max({p.c_len, max(l.top1,\
    \ c.c_len) + p.all, -inf});\n        diameter = max({p.diameter, c.diameter, p.p_len\
    \ + max(l.top1, c.c_len), c.c_len + l.top1, l.top1 + l.top2, l.diameter, -inf});\n\
    \        if(key) {\n          p_len = max(p_len, c.all);\n          c_len = max(c_len,\
    \ p.all);\n          diameter = max({diameter, p.p_len, c.c_len, l.top1, T(0)});\n\
    \        }\n      } else {\n        all = p.all + c.all + key;\n        p_len\
    \ = max({c.p_len, max(l.top1, p.p_len) + key + c.all, -inf});\n        c_len =\
    \ max({p.c_len, max(l.top1, c.c_len) + key + p.all, -inf});\n        diameter\
    \ = max({p.diameter, c.diameter, p.p_len + max(l.top1, c.c_len) + key, c.c_len\
    \ + l.top1 + key, l.top1 + l.top2 + key, l.diameter, -inf});\n      }\n    }\n\
    \n    light_t add() const {\n      light_t x;\n      x.val = c_len;\n      x.dia\
    \ = diameter;\n      return x;\n    }\n  };\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/develop/diameter.cpp
  requiredBy: []
  timestamp: '2020-11-02 16:10:08+09:00'
  verificationStatus: LIBRARY_ALL_WA
  verifiedWith:
  - test/verify/aoj-grl-5-a-2.test.cpp
documentation_of: structure/develop/diameter.cpp
layout: document
redirect_from:
- /library/structure/develop/diameter.cpp
- /library/structure/develop/diameter.cpp.html
title: structure/develop/diameter.cpp
---
