---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: math/combinatorics/mod-int.cpp
    title: math/combinatorics/mod-int.cpp
  - icon: ':heavy_check_mark:'
    path: structure/segment-tree/lazy-segment-tree.cpp
    title: "Lazy Segment Tree(\u9045\u5EF6\u4F1D\u642C\u30BB\u30B0\u30E1\u30F3\u30C8\
      \u6728)"
  - icon: ':heavy_check_mark:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: https://judge.yosupo.jp/problem/range_affine_range_sum
    links:
    - https://judge.yosupo.jp/problem/range_affine_range_sum
  bundledCode: "#line 1 \"test/verify/yosupo-range-affine-range-sum.test.cpp\"\n#define\
    \ PROBLEM \"https://judge.yosupo.jp/problem/range_affine_range_sum\"\n\n#line\
    \ 1 \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace std;\n\
    \nusing int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll = (1LL\
    \ << 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup()\
    \ {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed\
    \ << setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
    \ntemplate< typename T1, typename T2 >\nostream &operator<<(ostream &os, const\
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
    \  explicit FixPoint(F &&f) : F(forward< F >(f)) {}\n\n  template< typename...\
    \ Args >\n  decltype(auto) operator()(Args &&... args) const {\n    return F::operator()(*this,\
    \ forward< Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/yosupo-range-affine-range-sum.test.cpp\"\
    \n\n#line 1 \"math/combinatorics/mod-int.cpp\"\ntemplate< int mod >\nstruct ModInt\
    \ {\n  int x;\n\n  ModInt() : x(0) {}\n\n  ModInt(int64_t y) : x(y >= 0 ? y %\
    \ mod : (mod - (-y) % mod) % mod) {}\n\n  ModInt &operator+=(const ModInt &p)\
    \ {\n    if((x += p.x) >= mod) x -= mod;\n    return *this;\n  }\n\n  ModInt &operator-=(const\
    \ ModInt &p) {\n    if((x += mod - p.x) >= mod) x -= mod;\n    return *this;\n\
    \  }\n\n  ModInt &operator*=(const ModInt &p) {\n    x = (int) (1LL * x * p.x\
    \ % mod);\n    return *this;\n  }\n\n  ModInt &operator/=(const ModInt &p) {\n\
    \    *this *= p.inverse();\n    return *this;\n  }\n\n  ModInt operator-() const\
    \ { return ModInt(-x); }\n\n  ModInt operator+(const ModInt &p) const { return\
    \ ModInt(*this) += p; }\n\n  ModInt operator-(const ModInt &p) const { return\
    \ ModInt(*this) -= p; }\n\n  ModInt operator*(const ModInt &p) const { return\
    \ ModInt(*this) *= p; }\n\n  ModInt operator/(const ModInt &p) const { return\
    \ ModInt(*this) /= p; }\n\n  bool operator==(const ModInt &p) const { return x\
    \ == p.x; }\n\n  bool operator!=(const ModInt &p) const { return x != p.x; }\n\
    \n  ModInt inverse() const {\n    int a = x, b = mod, u = 1, v = 0, t;\n    while(b\
    \ > 0) {\n      t = a / b;\n      swap(a -= t * b, b);\n      swap(u -= t * v,\
    \ v);\n    }\n    return ModInt(u);\n  }\n\n  ModInt pow(int64_t n) const {\n\
    \    ModInt ret(1), mul(x);\n    while(n > 0) {\n      if(n & 1) ret *= mul;\n\
    \      mul *= mul;\n      n >>= 1;\n    }\n    return ret;\n  }\n\n  friend ostream\
    \ &operator<<(ostream &os, const ModInt &p) {\n    return os << p.x;\n  }\n\n\
    \  friend istream &operator>>(istream &is, ModInt &a) {\n    int64_t t;\n    is\
    \ >> t;\n    a = ModInt< mod >(t);\n    return (is);\n  }\n\n  static int get_mod()\
    \ { return mod; }\n};\n\nusing modint = ModInt< mod >;\n#line 6 \"test/verify/yosupo-range-affine-range-sum.test.cpp\"\
    \n\n#line 1 \"structure/segment-tree/lazy-segment-tree.cpp\"\n/**\n * @brief Lazy\
    \ Segment Tree(\u9045\u5EF6\u4F1D\u642C\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)\n\
    \ * @docs docs/lazy-segment-tree.md\n */\ntemplate< typename Monoid, typename\
    \ OperatorMonoid, typename F, typename G, typename H >\nstruct LazySegmentTree\
    \ {\n  int n, sz, height;\n  vector< Monoid > data;\n  vector< OperatorMonoid\
    \ > lazy;\n  const F f;\n  const G g;\n  const H h;\n  const Monoid M1;\n  const\
    \ OperatorMonoid OM0;\n\n  LazySegmentTree(int n, const F f, const G g, const\
    \ H h,\n                  const Monoid &M1, const OperatorMonoid OM0)\n      :\
    \ n(n), f(f), g(g), h(h), M1(M1), OM0(OM0) {\n    sz = 1;\n    height = 0;\n \
    \   while(sz < n) sz <<= 1, height++;\n    data.assign(2 * sz, M1);\n    lazy.assign(2\
    \ * sz, OM0);\n  }\n\n  void set(int k, const Monoid &x) {\n    data[k + sz] =\
    \ x;\n  }\n\n  void build() {\n    for(int k = sz - 1; k > 0; k--) {\n      data[k]\
    \ = f(data[2 * k + 0], data[2 * k + 1]);\n    }\n  }\n\n  inline void propagate(int\
    \ k) {\n    if(lazy[k] != OM0) {\n      lazy[2 * k + 0] = h(lazy[2 * k + 0], lazy[k]);\n\
    \      lazy[2 * k + 1] = h(lazy[2 * k + 1], lazy[k]);\n      data[k] = apply(k);\n\
    \      lazy[k] = OM0;\n    }\n  }\n\n  inline Monoid apply(int k) {\n    return\
    \ lazy[k] == OM0 ? data[k] : g(data[k], lazy[k]);\n  }\n\n  inline void recalc(int\
    \ k) {\n    while(k >>= 1) data[k] = f(apply(2 * k + 0), apply(2 * k + 1));\n\
    \  }\n\n  inline void thrust(int k) {\n    for(int i = height; i > 0; i--) propagate(k\
    \ >> i);\n  }\n\n  void update(int a, int b, const OperatorMonoid &x) {\n    if(a\
    \ >= b) return;\n    thrust(a += sz);\n    thrust(b += sz - 1);\n    for(int l\
    \ = a, r = b + 1; l < r; l >>= 1, r >>= 1) {\n      if(l & 1) lazy[l] = h(lazy[l],\
    \ x), ++l;\n      if(r & 1) --r, lazy[r] = h(lazy[r], x);\n    }\n    recalc(a);\n\
    \    recalc(b);\n  }\n\n  Monoid query(int a, int b) {\n    if(a >= b) return\
    \ M1;\n    thrust(a += sz);\n    thrust(b += sz - 1);\n    Monoid L = M1, R =\
    \ M1;\n    for(int l = a, r = b + 1; l < r; l >>= 1, r >>= 1) {\n      if(l &\
    \ 1) L = f(L, apply(l++));\n      if(r & 1) R = f(apply(--r), R);\n    }\n   \
    \ return f(L, R);\n  }\n\n  Monoid operator[](const int &k) {\n    return query(k,\
    \ k + 1);\n  }\n\n  template< typename C >\n  int find_subtree(int a, const C\
    \ &check, Monoid &M, bool type) {\n    while(a < sz) {\n      propagate(a);\n\
    \      Monoid nxt = type ? f(apply(2 * a + type), M) : f(M, apply(2 * a + type));\n\
    \      if(check(nxt)) a = 2 * a + type;\n      else M = nxt, a = 2 * a + 1 - type;\n\
    \    }\n    return a - sz;\n  }\n\n  template< typename C >\n  int find_first(int\
    \ a, const C &check) {\n    Monoid L = M1;\n    if(a <= 0) {\n      if(check(f(L,\
    \ apply(1)))) return find_subtree(1, check, L, false);\n      return n;\n    }\n\
    \    thrust(a + sz);\n    int b = sz;\n    for(a += sz, b += sz; a < b; a >>=\
    \ 1, b >>= 1) {\n      if(a & 1) {\n        Monoid nxt = f(L, apply(a));\n   \
    \     if(check(nxt)) return find_subtree(a, check, L, false);\n        L = nxt;\n\
    \        ++a;\n      }\n    }\n    return n;\n  }\n  \n  template< typename C\
    \ >\n  int find_last(int b, const C &check) {\n    Monoid R = M1;\n    if(b >=\
    \ sz) {\n      if(check(f(apply(1), R))) return find_subtree(1, check, R, true);\n\
    \      return -1;\n    }\n    thrust(b + sz - 1);\n    int a = sz;\n    for(b\
    \ += sz; a < b; a >>= 1, b >>= 1) {\n      if(b & 1) {\n        Monoid nxt = f(apply(--b),\
    \ R);\n        if(check(nxt)) return find_subtree(b, check, R, true);\n      \
    \  R = nxt;\n      }\n    }\n    return -1;\n  }\n};\n\ntemplate< typename Monoid,\
    \ typename OperatorMonoid, typename F, typename G, typename H >\nLazySegmentTree<\
    \ Monoid, OperatorMonoid, F, G, H > get_lazy_segment_tree\n    (int N, const F\
    \ &f, const G &g, const H &h, const Monoid &M1, const OperatorMonoid &OM0) {\n\
    \  return {N, f, g, h, M1, OM0};\n}\n#line 8 \"test/verify/yosupo-range-affine-range-sum.test.cpp\"\
    \n\nusing mint = ModInt< 998244353 >;\n\nint main() {\n  int N, Q;\n  cin >> N\
    \ >> Q;\n  using pi = pair< mint, int >;\n  using qi = pair< mint, mint >;\n \
    \ auto f = [](const pi &a, const pi &b) -> pi {\n    return {a.first + b.first,\
    \ a.second + b.second};\n  };\n  auto g = [](const pi &a, const qi &b) -> pi {\n\
    \    return {a.first * b.first + mint(a.second) * b.second, a.second};\n  };\n\
    \  auto h = [](const qi &a, const qi &b) -> qi {\n    return {a.first * b.first,\
    \ a.second * b.first + b.second};\n  };\n  auto seg = get_lazy_segment_tree(N,\
    \ f, g, h, pi(0, 0), qi(1, 0));\n  for(int i = 0; i < N; i++) {\n    mint a;\n\
    \    cin >> a;\n    seg.set(i, pi(a, 1));\n  }\n  seg.build();\n  for(int i =\
    \ 0; i < Q; i++) {\n    int t;\n    cin >> t;\n    if(t == 0) {\n      int l,\
    \ r;\n      mint b, c;\n      cin >> l >> r >> b >> c;\n      seg.update(l, r,\
    \ qi(b, c));\n    } else {\n      int l, r;\n      cin >> l >> r;\n      cout\
    \ << seg.query(l, r).first << \"\\n\";\n    }\n  }\n}\n"
  code: "#define PROBLEM \"https://judge.yosupo.jp/problem/range_affine_range_sum\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../math/combinatorics/mod-int.cpp\"\
    \n\n#include \"../../structure/segment-tree/lazy-segment-tree.cpp\"\n\nusing mint\
    \ = ModInt< 998244353 >;\n\nint main() {\n  int N, Q;\n  cin >> N >> Q;\n  using\
    \ pi = pair< mint, int >;\n  using qi = pair< mint, mint >;\n  auto f = [](const\
    \ pi &a, const pi &b) -> pi {\n    return {a.first + b.first, a.second + b.second};\n\
    \  };\n  auto g = [](const pi &a, const qi &b) -> pi {\n    return {a.first *\
    \ b.first + mint(a.second) * b.second, a.second};\n  };\n  auto h = [](const qi\
    \ &a, const qi &b) -> qi {\n    return {a.first * b.first, a.second * b.first\
    \ + b.second};\n  };\n  auto seg = get_lazy_segment_tree(N, f, g, h, pi(0, 0),\
    \ qi(1, 0));\n  for(int i = 0; i < N; i++) {\n    mint a;\n    cin >> a;\n   \
    \ seg.set(i, pi(a, 1));\n  }\n  seg.build();\n  for(int i = 0; i < Q; i++) {\n\
    \    int t;\n    cin >> t;\n    if(t == 0) {\n      int l, r;\n      mint b, c;\n\
    \      cin >> l >> r >> b >> c;\n      seg.update(l, r, qi(b, c));\n    } else\
    \ {\n      int l, r;\n      cin >> l >> r;\n      cout << seg.query(l, r).first\
    \ << \"\\n\";\n    }\n  }\n}\n"
  dependsOn:
  - template/template.cpp
  - math/combinatorics/mod-int.cpp
  - structure/segment-tree/lazy-segment-tree.cpp
  isVerificationFile: true
  path: test/verify/yosupo-range-affine-range-sum.test.cpp
  requiredBy: []
  timestamp: '2021-08-28 02:59:12+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/yosupo-range-affine-range-sum.test.cpp
layout: document
redirect_from:
- /verify/test/verify/yosupo-range-affine-range-sum.test.cpp
- /verify/test/verify/yosupo-range-affine-range-sum.test.cpp.html
title: test/verify/yosupo-range-affine-range-sum.test.cpp
---
