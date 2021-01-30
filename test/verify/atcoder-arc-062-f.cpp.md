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
  bundledCode: "#line 1 \"test/verify/atcoder-arc-062-f.cpp\"\n#define IGNORE\n\n\
    template< int mod >\nstruct ModInt {\n  int x;\n \n  ModInt() : x(0) {}\n \n \
    \ ModInt(int64_t y) : x(y >= 0 ? y % mod : (mod - (-y) % mod) % mod) {}\n \n \
    \ ModInt &operator+=(const ModInt &p) {\n    if((x += p.x) >= mod) x -= mod;\n\
    \    return *this;\n  }\n \n  ModInt &operator-=(const ModInt &p) {\n    if((x\
    \ += mod - p.x) >= mod) x -= mod;\n    return *this;\n  }\n \n  ModInt &operator*=(const\
    \ ModInt &p) {\n    x = (int) (1LL * x * p.x % mod);\n    return *this;\n  }\n\
    \ \n  ModInt &operator/=(const ModInt &p) {\n    *this *= p.inverse();\n    return\
    \ *this;\n  }\n \n  ModInt operator-() const { return ModInt(-x); }\n \n  ModInt\
    \ operator+(const ModInt &p) const { return ModInt(*this) += p; }\n \n  ModInt\
    \ operator-(const ModInt &p) const { return ModInt(*this) -= p; }\n \n  ModInt\
    \ operator*(const ModInt &p) const { return ModInt(*this) *= p; }\n \n  ModInt\
    \ operator/(const ModInt &p) const { return ModInt(*this) /= p; }\n \n  bool operator==(const\
    \ ModInt &p) const { return x == p.x; }\n \n  bool operator!=(const ModInt &p)\
    \ const { return x != p.x; }\n \n  ModInt inverse() const {\n    int a = x, b\
    \ = mod, u = 1, v = 0, t;\n    while(b > 0) {\n      t = a / b;\n      swap(a\
    \ -= t * b, b);\n      swap(u -= t * v, v);\n    }\n    return ModInt(u);\n  }\n\
    \ \n  ModInt pow(int64_t n) const {\n    ModInt ret(1), mul(x);\n    while(n >\
    \ 0) {\n      if(n & 1) ret *= mul;\n      mul *= mul;\n      n >>= 1;\n    }\n\
    \    return ret;\n  }\n \n  friend ostream &operator<<(ostream &os, const ModInt\
    \ &p) {\n    return os << p.x;\n  }\n \n  friend istream &operator>>(istream &is,\
    \ ModInt &a) {\n    int64_t t;\n    is >> t;\n    a = ModInt< mod >(t);\n    return\
    \ (is);\n  }\n};\n \nusing modint = ModInt< mod >;\n \ntemplate< typename T >\n\
    struct Combination {\n  vector< T > _fact, _rfact;\n \n  Combination(int sz) :\
    \ _fact(sz + 1), _rfact(sz + 1) {\n    _fact[0] = _rfact[sz] = 1;\n    for(int\
    \ i = 1; i <= sz; i++) _fact[i] = _fact[i - 1] * i;\n    _rfact[sz] /= _fact[sz];\n\
    \    for(int i = sz - 1; i >= 0; i--) _rfact[i] = _rfact[i + 1] * (i + 1);\n \
    \ }\n \n  inline T fact(int k) const { return _fact[k]; }\n \n  inline T rfact(int\
    \ k) const { return _rfact[k]; }\n \n  T P(int n, int r) const {\n    if(r < 0\
    \ || n < r) return 0;\n    return fact(n) * rfact(n - r);\n  }\n \n  T C(int p,\
    \ int q) const {\n    if(q < 0 || p < q) return 0;\n    return fact(p) * rfact(q)\
    \ * rfact(p - q);\n  }\n \n  T H(int n, int r) const {\n    if(n < 0 || r < 0)\
    \ return (0);\n    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n \nint64_t euler_phi(int64_t\
    \ n) {\n  int64_t ret = n;\n  for(int64_t i = 2; i * i <= n; i++) {\n    if(n\
    \ % i == 0) {\n      ret -= ret / i;\n      while(n % i == 0) n /= i;\n    }\n\
    \  }\n  if(n > 1) ret -= ret / n;\n  return ret;\n}\n \nint main() {\n  int N,\
    \ M, K;\n  cin >> N >> M >> K;\n  UnWeightedGraph g(N);\n  Combination< modint\
    \ > beet(101010);\n  while(M--) {\n    int x, y;\n    cin >> x >> y;\n    --x,\
    \ --y;\n    g[x].push_back(y);\n    g[y].push_back(x);\n  }\n  BiConnectedComponents<\
    \ UnWeightedGraph > bcc(g);\n  bcc.build();\n  modint ret = 1;\n  for(auto &vs\
    \ : bcc.bc) {\n    set< int > vertex;\n    for(auto &p : vs) vertex.emplace(p.first);\n\
    \    for(auto &p : vs) vertex.emplace(p.second);\n    if(vertex.size() == vs.size()\
    \ + 1) {\n      ret *= K;\n    } else if(vertex.size() == vs.size()) {\n     \
    \ modint add = 0;\n      for(int i = 1; i <= vertex.size(); i++) {\n        if(vertex.size()\
    \ % i == 0) {\n          add += modint(K).pow(vertex.size() / i) * euler_phi(i);\n\
    \        }\n      }\n      add /= vertex.size();\n      ret *= add;\n    } else\
    \ {\n      ret *= beet.H(K, vs.size());\n    }\n  }\n  cout << ret << endl;\n\
    }\n"
  code: "#define IGNORE\n\ntemplate< int mod >\nstruct ModInt {\n  int x;\n \n  ModInt()\
    \ : x(0) {}\n \n  ModInt(int64_t y) : x(y >= 0 ? y % mod : (mod - (-y) % mod)\
    \ % mod) {}\n \n  ModInt &operator+=(const ModInt &p) {\n    if((x += p.x) >=\
    \ mod) x -= mod;\n    return *this;\n  }\n \n  ModInt &operator-=(const ModInt\
    \ &p) {\n    if((x += mod - p.x) >= mod) x -= mod;\n    return *this;\n  }\n \n\
    \  ModInt &operator*=(const ModInt &p) {\n    x = (int) (1LL * x * p.x % mod);\n\
    \    return *this;\n  }\n \n  ModInt &operator/=(const ModInt &p) {\n    *this\
    \ *= p.inverse();\n    return *this;\n  }\n \n  ModInt operator-() const { return\
    \ ModInt(-x); }\n \n  ModInt operator+(const ModInt &p) const { return ModInt(*this)\
    \ += p; }\n \n  ModInt operator-(const ModInt &p) const { return ModInt(*this)\
    \ -= p; }\n \n  ModInt operator*(const ModInt &p) const { return ModInt(*this)\
    \ *= p; }\n \n  ModInt operator/(const ModInt &p) const { return ModInt(*this)\
    \ /= p; }\n \n  bool operator==(const ModInt &p) const { return x == p.x; }\n\
    \ \n  bool operator!=(const ModInt &p) const { return x != p.x; }\n \n  ModInt\
    \ inverse() const {\n    int a = x, b = mod, u = 1, v = 0, t;\n    while(b > 0)\
    \ {\n      t = a / b;\n      swap(a -= t * b, b);\n      swap(u -= t * v, v);\n\
    \    }\n    return ModInt(u);\n  }\n \n  ModInt pow(int64_t n) const {\n    ModInt\
    \ ret(1), mul(x);\n    while(n > 0) {\n      if(n & 1) ret *= mul;\n      mul\
    \ *= mul;\n      n >>= 1;\n    }\n    return ret;\n  }\n \n  friend ostream &operator<<(ostream\
    \ &os, const ModInt &p) {\n    return os << p.x;\n  }\n \n  friend istream &operator>>(istream\
    \ &is, ModInt &a) {\n    int64_t t;\n    is >> t;\n    a = ModInt< mod >(t);\n\
    \    return (is);\n  }\n};\n \nusing modint = ModInt< mod >;\n \ntemplate< typename\
    \ T >\nstruct Combination {\n  vector< T > _fact, _rfact;\n \n  Combination(int\
    \ sz) : _fact(sz + 1), _rfact(sz + 1) {\n    _fact[0] = _rfact[sz] = 1;\n    for(int\
    \ i = 1; i <= sz; i++) _fact[i] = _fact[i - 1] * i;\n    _rfact[sz] /= _fact[sz];\n\
    \    for(int i = sz - 1; i >= 0; i--) _rfact[i] = _rfact[i + 1] * (i + 1);\n \
    \ }\n \n  inline T fact(int k) const { return _fact[k]; }\n \n  inline T rfact(int\
    \ k) const { return _rfact[k]; }\n \n  T P(int n, int r) const {\n    if(r < 0\
    \ || n < r) return 0;\n    return fact(n) * rfact(n - r);\n  }\n \n  T C(int p,\
    \ int q) const {\n    if(q < 0 || p < q) return 0;\n    return fact(p) * rfact(q)\
    \ * rfact(p - q);\n  }\n \n  T H(int n, int r) const {\n    if(n < 0 || r < 0)\
    \ return (0);\n    return r == 0 ? 1 : C(n + r - 1, r);\n  }\n};\n \nint64_t euler_phi(int64_t\
    \ n) {\n  int64_t ret = n;\n  for(int64_t i = 2; i * i <= n; i++) {\n    if(n\
    \ % i == 0) {\n      ret -= ret / i;\n      while(n % i == 0) n /= i;\n    }\n\
    \  }\n  if(n > 1) ret -= ret / n;\n  return ret;\n}\n \nint main() {\n  int N,\
    \ M, K;\n  cin >> N >> M >> K;\n  UnWeightedGraph g(N);\n  Combination< modint\
    \ > beet(101010);\n  while(M--) {\n    int x, y;\n    cin >> x >> y;\n    --x,\
    \ --y;\n    g[x].push_back(y);\n    g[y].push_back(x);\n  }\n  BiConnectedComponents<\
    \ UnWeightedGraph > bcc(g);\n  bcc.build();\n  modint ret = 1;\n  for(auto &vs\
    \ : bcc.bc) {\n    set< int > vertex;\n    for(auto &p : vs) vertex.emplace(p.first);\n\
    \    for(auto &p : vs) vertex.emplace(p.second);\n    if(vertex.size() == vs.size()\
    \ + 1) {\n      ret *= K;\n    } else if(vertex.size() == vs.size()) {\n     \
    \ modint add = 0;\n      for(int i = 1; i <= vertex.size(); i++) {\n        if(vertex.size()\
    \ % i == 0) {\n          add += modint(K).pow(vertex.size() / i) * euler_phi(i);\n\
    \        }\n      }\n      add /= vertex.size();\n      ret *= add;\n    } else\
    \ {\n      ret *= beet.H(K, vs.size());\n    }\n  }\n  cout << ret << endl;\n\
    }\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-arc-062-f.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-arc-062-f.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-arc-062-f.cpp
- /library/test/verify/atcoder-arc-062-f.cpp.html
title: test/verify/atcoder-arc-062-f.cpp
---
