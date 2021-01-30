---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: graph/shortest-path/warshall-floyd.cpp
    title: graph/shortest-path/warshall-floyd.cpp
  - icon: ':heavy_check_mark:'
    path: graph/template.cpp
    title: graph/template.cpp
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
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C
  bundledCode: "#line 1 \"test/verify/aoj-grl-1-c.test.cpp\"\n#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C\"\
    \n\n#line 1 \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace\
    \ std;\n\nusing int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll\
    \ = (1LL << 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup()\
    \ {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed\
    \ << setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
    \n\ntemplate< typename T1, typename T2 >\nostream &operator<<(ostream &os, const\
    \ pair< T1, T2 >& p) {\n  os << p.first << \" \" << p.second;\n  return os;\n\
    }\n\ntemplate< typename T1, typename T2 >\nistream &operator>>(istream &is, pair<\
    \ T1, T2 > &p) {\n  is >> p.first >> p.second;\n  return is;\n}\n\ntemplate< typename\
    \ T >\nostream &operator<<(ostream &os, const vector< T > &v) {\n  for(int i =\
    \ 0; i < (int) v.size(); i++) {\n    os << v[i] << (i + 1 != v.size() ? \" \"\
    \ : \"\");\n  }\n  return os;\n}\n\ntemplate< typename T >\nistream &operator>>(istream\
    \ &is, vector< T > &v) {\n  for(T &in : v) is >> in;\n  return is;\n}\n\ntemplate<\
    \ typename T1, typename T2 >\ninline bool chmax(T1 &a, T2 b) { return a < b &&\
    \ (a = b, true); }\n\ntemplate< typename T1, typename T2 >\ninline bool chmin(T1\
    \ &a, T2 b) { return a > b && (a = b, true); }\n\ntemplate< typename T = int64\
    \ >\nvector< T > make_v(size_t a) {\n  return vector< T >(a);\n}\n\ntemplate<\
    \ typename T, typename... Ts >\nauto make_v(size_t a, Ts... ts) {\n  return vector<\
    \ decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));\n}\n\ntemplate< typename\
    \ T, typename V >\ntypename enable_if< is_class< T >::value == 0 >::type fill_v(T\
    \ &t, const V &v) {\n  t = v;\n}\n\ntemplate< typename T, typename V >\ntypename\
    \ enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {\n  for(auto\
    \ &e : t) fill_v(e, v);\n}\n\ntemplate< typename F >\nstruct FixPoint : F {\n\
    \  FixPoint(F &&f) : F(forward< F >(f)) {}\n \n  template< typename... Args >\n\
    \  decltype(auto) operator()(Args &&... args) const {\n    return F::operator()(*this,\
    \ forward< Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 1 \"graph/template.cpp\"\
    \ntemplate< typename T >\nstruct edge {\n  int src, to;\n  T cost;\n\n  edge(int\
    \ to, T cost) : src(-1), to(to), cost(cost) {}\n\n  edge(int src, int to, T cost)\
    \ : src(src), to(to), cost(cost) {}\n\n  edge &operator=(const int &x) {\n   \
    \ to = x;\n    return *this;\n  }\n\n  operator int() const { return to; }\n};\n\
    \ntemplate< typename T >\nusing Edges = vector< edge< T > >;\ntemplate< typename\
    \ T >\nusing WeightedGraph = vector< Edges< T > >;\nusing UnWeightedGraph = vector<\
    \ vector< int > >;\ntemplate< typename T >\nusing Matrix = vector< vector< T >\
    \ >;\n#line 5 \"test/verify/aoj-grl-1-c.test.cpp\"\n\n#line 1 \"graph/shortest-path/warshall-floyd.cpp\"\
    \ntemplate< typename T >\nvoid warshall_floyd(Matrix< T > &g, T INF) {\n  for(int\
    \ k = 0; k < g.size(); k++) {\n    for(int i = 0; i < g.size(); i++) {\n     \
    \ for(int j = 0; j < g.size(); j++) {\n        if(g[i][k] == INF || g[k][j] ==\
    \ INF) continue;\n        g[i][j] = min(g[i][j], g[i][k] + g[k][j]);\n      }\n\
    \    }\n  }\n}\n#line 7 \"test/verify/aoj-grl-1-c.test.cpp\"\n\nint main() {\n\
    \  int V, E;\n  scanf(\"%d %d\", &V, &E);\n  Matrix< int > mat(V, vector< int\
    \ >(V, INT_MAX));\n  for(int i = 0; i < V; i++) mat[i][i] = 0;\n  for(int i =\
    \ 0; i < E; i++) {\n    int x, y, z;\n    scanf(\"%d %d %d\", &x, &y, &z);\n \
    \   mat[x][y] = z;\n  }\n  warshall_floyd(mat, INT_MAX);\n  for(int i = 0; i <\
    \ V; i++) {\n    if(mat[i][i] < 0) {\n      puts(\"NEGATIVE CYCLE\");\n      return\
    \ 0;\n    }\n  }\n  for(int i = 0; i < V; i++) {\n    for(int j = 0; j < V; j++)\
    \ {\n      if(j > 0) putchar(' ');\n      if(mat[i][j] == INT_MAX) printf(\"INF\"\
    );\n      else printf(\"%d\", mat[i][j]);\n    }\n    putchar('\\n');\n  }\n}\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_1_C\"\
    \n\n#include \"../../template/template.cpp\"\n#include \"../../graph/template.cpp\"\
    \n\n#include \"../../graph/shortest-path/warshall-floyd.cpp\"\n\nint main() {\n\
    \  int V, E;\n  scanf(\"%d %d\", &V, &E);\n  Matrix< int > mat(V, vector< int\
    \ >(V, INT_MAX));\n  for(int i = 0; i < V; i++) mat[i][i] = 0;\n  for(int i =\
    \ 0; i < E; i++) {\n    int x, y, z;\n    scanf(\"%d %d %d\", &x, &y, &z);\n \
    \   mat[x][y] = z;\n  }\n  warshall_floyd(mat, INT_MAX);\n  for(int i = 0; i <\
    \ V; i++) {\n    if(mat[i][i] < 0) {\n      puts(\"NEGATIVE CYCLE\");\n      return\
    \ 0;\n    }\n  }\n  for(int i = 0; i < V; i++) {\n    for(int j = 0; j < V; j++)\
    \ {\n      if(j > 0) putchar(' ');\n      if(mat[i][j] == INT_MAX) printf(\"INF\"\
    );\n      else printf(\"%d\", mat[i][j]);\n    }\n    putchar('\\n');\n  }\n}\n"
  dependsOn:
  - template/template.cpp
  - graph/template.cpp
  - graph/shortest-path/warshall-floyd.cpp
  isVerificationFile: true
  path: test/verify/aoj-grl-1-c.test.cpp
  requiredBy: []
  timestamp: '2019-11-30 23:02:43+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-grl-1-c.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-grl-1-c.test.cpp
- /verify/test/verify/aoj-grl-1-c.test.cpp.html
title: test/verify/aoj-grl-1-c.test.cpp
---
