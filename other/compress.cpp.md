---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"other/compress.cpp\"\ntemplate< typename T >\nstruct Compress\
    \ {\n  vector< T > xs;\n\n  Compress() = default;\n\n  Compress(const vector<\
    \ T > &vs) {\n    add(vs);\n  }\n\n  Compress(const initializer_list< vector<\
    \ T > > &vs) {\n    for(auto &p : vs) add(p);\n  }\n\n  void add(const vector<\
    \ T > &vs) {\n    copy(begin(vs), end(vs), back_inserter(xs));\n  }\n\n  void\
    \ add(const T &x) {\n    xs.emplace_back(x);\n  }\n\n  void build() {\n    sort(begin(xs),\
    \ end(xs));\n    xs.erase(unique(begin(xs), end(xs)), end(xs));\n  }\n\n  vector<\
    \ int > get(const vector< T > &vs) const {\n    vector< int > ret;\n    transform(begin(vs),\
    \ end(vs), back_inserter(ret), [&](const T &x) {\n      return lower_bound(begin(xs),\
    \ end(xs), x) - begin(xs);\n    });\n    return ret;\n  }\n\n  int get(const T\
    \ &x) const {\n    return lower_bound(begin(xs), end(xs), x) - begin(xs);\n  }\n\
    \n  const T &operator[](int k) const {\n    return xs[k];\n  }\n};\n"
  code: "template< typename T >\nstruct Compress {\n  vector< T > xs;\n\n  Compress()\
    \ = default;\n\n  Compress(const vector< T > &vs) {\n    add(vs);\n  }\n\n  Compress(const\
    \ initializer_list< vector< T > > &vs) {\n    for(auto &p : vs) add(p);\n  }\n\
    \n  void add(const vector< T > &vs) {\n    copy(begin(vs), end(vs), back_inserter(xs));\n\
    \  }\n\n  void add(const T &x) {\n    xs.emplace_back(x);\n  }\n\n  void build()\
    \ {\n    sort(begin(xs), end(xs));\n    xs.erase(unique(begin(xs), end(xs)), end(xs));\n\
    \  }\n\n  vector< int > get(const vector< T > &vs) const {\n    vector< int >\
    \ ret;\n    transform(begin(vs), end(vs), back_inserter(ret), [&](const T &x)\
    \ {\n      return lower_bound(begin(xs), end(xs), x) - begin(xs);\n    });\n \
    \   return ret;\n  }\n\n  int get(const T &x) const {\n    return lower_bound(begin(xs),\
    \ end(xs), x) - begin(xs);\n  }\n\n  const T &operator[](int k) const {\n    return\
    \ xs[k];\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: other/compress.cpp
  requiredBy: []
  timestamp: '2019-08-02 17:12:26+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: other/compress.cpp
layout: document
redirect_from:
- /library/other/compress.cpp
- /library/other/compress.cpp.html
title: other/compress.cpp
---
