---
data:
  _extendedDependsOn:
  - icon: ':x:'
    path: structure/develop/array-pool.cpp
    title: structure/develop/array-pool.cpp
  - icon: ':x:'
    path: structure/develop/diameter.cpp
    title: structure/develop/diameter.cpp
  - icon: ':x:'
    path: structure/develop/link-cut-tree-subtree.cpp
    title: structure/develop/link-cut-tree-subtree.cpp
  - icon: ':x:'
    path: structure/develop/splay-tree.cpp
    title: structure/develop/splay-tree.cpp
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: true
  _pathExtension: cpp
  _verificationStatusIcon: ':x:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A
  bundledCode: "#line 1 \"test/verify/aoj-grl-5-a-2.test.cpp\"\n#define PROBLEM \"\
    http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A\"\n\n#line 1\
    \ \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace std;\n\
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
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/aoj-grl-5-a-2.test.cpp\"\
    \n\n#line 1 \"structure/develop/array-pool.cpp\"\ntemplate< class T, size_t V\
    \ >\nstruct ArrayPool {\n  array< T, V > pool;\n  array< T *, V > stock;\n  int\
    \ ptr;\n\n  ArrayPool() { clear(); }\n\n  inline T *alloc() {\n    return stock[--ptr];\n\
    \  }\n\n  inline void free(T *t) {\n    stock[ptr++] = t;\n  }\n\n  void clear()\
    \ {\n    ptr = (int) pool.size();\n    for(int i = 0; i < pool.size(); i++) stock[i]\
    \ = &pool[i];\n  }\n};\n#line 6 \"test/verify/aoj-grl-5-a-2.test.cpp\"\n\n#line\
    \ 1 \"structure/develop/splay-tree.cpp\"\ntemplate< typename key_t, size_t V >\n\
    struct SplayTree {\n\n  const key_t e;\n\n  SplayTree() : pool(), e(key_t()) {}\n\
    \n  struct Node {\n    Node *l, *r, *p;\n    key_t sum;\n\n    Node() = default;\n\
    \n    explicit Node(const key_t &k) : sum(k), l(nullptr), r(nullptr), p(nullptr)\
    \ {}\n  };\n\n  ArrayPool< Node, V > pool;\n\nprivate:\n  void rotr(Node *t) {\n\
    \    auto *x = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n    t->r\
    \ = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n      if(y->l\
    \ == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n    }\n  }\n\
    \n  void rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r = t->l))\
    \ t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n    if((t->p\
    \ = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n    \
    \  update(y);\n    }\n  }\n\n  void update(Node *t) {\n    t->sum.set_sum();\n\
    \    if(t->l) t->sum.update(t->l->sum);\n    if(t->r) t->sum.update(t->r->sum);\n\
    \  }\n\n  Node *get_right(Node *t) const {\n    while(t->r) t = t->r;\n    return\
    \ t;\n  }\n\n  inline Node *alloc(const key_t &v) {\n    auto p = &(*pool.alloc()\
    \ = Node(v));\n    update(p);\n    return p;\n  }\n\n  void splay(Node *t) {\n\
    \    while(t->p) {\n      auto *q = t->p;\n      if(!q->p) {\n        if(q->l\
    \ == t) rotr(t);\n        else rotl(t);\n      } else {\n        auto *r = q->p;\n\
    \        if(r->l == q) {\n          if(q->l == t) rotr(q), rotr(t);\n        \
    \  else rotl(t), rotr(t);\n        } else {\n          if(q->r == t) rotl(q),\
    \ rotl(t);\n          else rotr(t), rotl(t);\n        }\n      }\n    }\n  }\n\
    \npublic:\n  inline const key_t &sum(Node *t) {\n    return t ? t->sum : e;\n\
    \  }\n\n  Node *push_back(Node *t, const key_t &v) {\n    if(!t) {\n      t =\
    \ alloc(v);\n      return t;\n    } else {\n      Node *cur = get_right(t), *z\
    \ = alloc(v);\n      z->p = cur;\n      cur->r = z;\n      update(cur);\n    \
    \  splay(z);\n      return z;\n    }\n  }\n\n  Node *erase(Node *t) {\n    splay(t);\n\
    \    Node *x = t->l, *y = t->r;\n    pool.free(t);\n    if(!x) {\n      t = y;\n\
    \      if(t) t->p = nullptr;\n    } else if(!y) {\n      t = x;\n      t->p =\
    \ nullptr;\n    } else {\n      x->p = nullptr;\n      t = get_right(x);\n   \
    \   splay(t);\n      t->r = y;\n      y->p = t;\n      update(t);\n    }\n   \
    \ return t;\n  }\n};\n#line 2 \"structure/develop/link-cut-tree-subtree.cpp\"\n\
    \ntemplate< typename T, size_t V >\nstruct LinkCutTreeSubTree {\n  using key_t\
    \ = typename T::key_t;\n  using heavy_t = typename T::heavy_t;\n  using light_t\
    \ = typename T::light_t;\n\n  struct Node {\n    Node *l, *r, *p;\n\n    typename\
    \ SplayTree< light_t, V >::Node *light, *belong;\n    heavy_t sum;\n\n    Node()\
    \ = default;\n\n    bool is_root() const {\n      return !p || (p->l != this &&\
    \ p->r != this);\n    }\n\n    Node(const key_t &key) :\n        belong(nullptr),\
    \ l(nullptr), r(nullptr), p(nullptr), light(nullptr) {\n      sum.set_key(key);\n\
    \    }\n  };\n\n  using ST = SplayTree< light_t, V >;\n\n  ST st;\n  const heavy_t\
    \ ident;\n  ArrayPool< Node, V > pool;\n\n  LinkCutTreeSubTree() : ident(heavy_t()),\
    \ st(), pool() {}\n\n  Node *alloc(const key_t &key) {\n    auto ret = &(*pool.alloc()\
    \ = Node(key));\n    update(ret);\n    return ret;\n  }\n\n  Node *set_key(Node\
    \ *t, const key_t &key) {\n    expose(t);\n    t->sum.set_key(key);\n    update(t);\n\
    \    return t;\n  }\n\n  void update(Node *t) {\n    t->sum.update(t->l ? t->l->sum\
    \ : ident, t->r ? t->r->sum : ident, st.sum(t->light));\n  }\n\n  void rotr(Node\
    \ *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->l = t->r)) t->r->p = x;\n\
    \    t->r = x, x->p = t;\n    update(x), update(t);\n    if((t->p = y)) {\n  \
    \    if(y->l == x) y->l = t;\n      if(y->r == x) y->r = t;\n      update(y);\n\
    \    }\n  }\n\n  void rotl(Node *t) {\n    auto *x = t->p, *y = x->p;\n    if((x->r\
    \ = t->l)) t->l->p = x;\n    t->l = x, x->p = t;\n    update(x), update(t);\n\
    \    if((t->p = y)) {\n      if(y->l == x) y->l = t;\n      if(y->r == x) y->r\
    \ = t;\n      update(y);\n    }\n  }\n\n\n  void splay(Node *t) {\n\n    Node\
    \ *rot = t;\n    while(!rot->is_root()) rot = rot->p;\n    t->belong = rot->belong;\n\
    \    if(t != rot) rot->belong = nullptr;\n\n    while(!t->is_root()) {\n     \
    \ auto *q = t->p;\n      if(q->is_root()) {\n        if(q->l == t) rotr(t);\n\
    \        else rotl(t);\n      } else {\n        auto *r = q->p;\n        if(r->l\
    \ == q) {\n          if(q->l == t) rotr(q), rotr(t);\n          else rotl(t),\
    \ rotr(t);\n        } else {\n          if(q->r == t) rotl(q), rotl(t);\n    \
    \      else rotr(t), rotl(t);\n        }\n      }\n    }\n\n  }\n\n\n  Node *expose(Node\
    \ *t) {\n    Node *rp = nullptr;\n    for(auto *cur = t; cur; cur = cur->p) {\n\
    \      splay(cur);\n      if(cur->r) {\n        cur->light = st.push_back(cur->light,\
    \ cur->r->sum.add());\n        cur->r->belong = cur->light;\n      }\n      cur->r\
    \ = rp;\n      if(cur->r) {\n        cur->light = st.erase(cur->r->belong);\n\
    \      }\n      update(cur);\n      rp = cur;\n    }\n    splay(t);\n    return\
    \ rp;\n  }\n\n  void link(Node *child, Node *parent) {\n    expose(child);\n \
    \   expose(parent);\n    child->p = parent;\n    parent->r = child;\n    update(parent);\n\
    \  }\n\n  void cut(Node *child) {\n    expose(child);\n    auto *parent = child->l;\n\
    \    child->l = nullptr;\n    parent->p = nullptr;\n    update(child);\n  }\n\n\
    \  Node *lca(Node *u, Node *v) {\n    if(get_root(u) != get_root(v)) return nullptr;\n\
    \    expose(u);\n    return expose(v);\n  }\n\n  Node *get_root(Node *x) {\n \
    \   expose(x);\n    while(x->l) {\n      push(x);\n      x = x->l;\n    }\n  \
    \  return x;\n  }\n};\n#line 8 \"test/verify/aoj-grl-5-a-2.test.cpp\"\n\n#line\
    \ 1 \"structure/develop/diameter.cpp\"\ntemplate< typename T >\nstruct Diameter\
    \ {\n\n  using key_t = pair< bool, T >;\n  static const T inf = numeric_limits<\
    \ T >::max() / 3;\n\n  struct light_t {\n    T val, dia;\n\n    T top1, top2;\n\
    \    T diameter;\n\n    light_t() : top1(-inf), top2(-inf), diameter(-inf) {}\n\
    \n    void set_sum() {\n      top1 = val;\n      top2 = -inf;\n      diameter\
    \ = dia;\n    }\n\n    void update(const light_t &p) {\n      if(top1 < p.top1)\
    \ {\n        top2 = top1;\n        top1 = p.top1;\n        if(top2 < p.top2) {\n\
    \          top2 = p.top2;\n        }\n      } else if(top2 < p.top1) {\n     \
    \   top2 = p.top1;\n      }\n      if(diameter < p.diameter) {\n        diameter\
    \ = p.diameter;\n      }\n    }\n  };\n\n  struct heavy_t {\n    bool vertex;\n\
    \    T key;\n\n    T all, p_len, c_len, diameter;\n\n    heavy_t() : all(0), p_len(-inf),\
    \ c_len(-inf), diameter(-inf) {}\n\n    void set_key(const key_t &x) {\n     \
    \ vertex = x.first;\n      key = x.second;\n    }\n\n    void update(const heavy_t\
    \ &p, const heavy_t &c, const light_t &l) {\n      if(vertex) {\n        all =\
    \ p.all + c.all;\n        p_len = max({c.p_len, max(l.top1, p.p_len) + c.all,\
    \ -inf});\n        c_len = max({p.c_len, max(l.top1, c.c_len) + p.all, -inf});\n\
    \        diameter = max({p.diameter, c.diameter, p.p_len + max(l.top1, c.c_len),\
    \ c.c_len + l.top1, l.top1 + l.top2, l.diameter, -inf});\n        if(key) {\n\
    \          p_len = max(p_len, c.all);\n          c_len = max(c_len, p.all);\n\
    \          diameter = max({diameter, p.p_len, c.c_len, l.top1, T(0)});\n     \
    \   }\n      } else {\n        all = p.all + c.all + key;\n        p_len = max({c.p_len,\
    \ max(l.top1, p.p_len) + key + c.all, -inf});\n        c_len = max({p.c_len, max(l.top1,\
    \ c.c_len) + key + p.all, -inf});\n        diameter = max({p.diameter, c.diameter,\
    \ p.p_len + max(l.top1, c.c_len) + key, c.c_len + l.top1 + key, l.top1 + l.top2\
    \ + key, l.diameter, -inf});\n      }\n    }\n\n    light_t add() const {\n  \
    \    light_t x;\n      x.val = c_len;\n      x.dia = diameter;\n      return x;\n\
    \    }\n  };\n};\n#line 10 \"test/verify/aoj-grl-5-a-2.test.cpp\"\n\nint main()\
    \ {\n  int N;\n  cin >> N;\n  using LCT = LinkCutTreeSubTree< Diameter< int >,\
    \ 200000 >;\n  LCT lct;\n  vector< vector< pair< int, int > > > g(N);\n  for(int\
    \ i = 1; i < N; i++) {\n    int x, y, z;\n    cin >> x >> y >> z;\n    g[x].emplace_back(y,\
    \ z);\n    g[y].emplace_back(x, z);\n  }\n  vector< LCT::Node * > vs(N), es(N);\n\
    \  auto rec = MFP([&](auto rec, int idx, int par) -> void {\n    vs[idx] = lct.alloc(make_pair(true,\
    \ 1));\n    for(auto &e : g[idx]) {\n      if(e.first == par) continue;\n    \
    \  rec(e.first, idx);\n      es[e.first] = lct.alloc(make_pair(false, e.second));\n\
    \      lct.link(vs[e.first], es[e.first]);\n      lct.link(es[e.first], vs[idx]);\n\
    \    }\n  });\n  rec(0, -1);\n  lct.expose(vs[0]);\n  cout << vs[0]->sum.diameter\
    \ << \"\\n\";\n}\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_5_A\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../structure/develop/array-pool.cpp\"\
    \n\n#include \"../../structure/develop/link-cut-tree-subtree.cpp\"\n\n#include\
    \ \"../../structure/develop/diameter.cpp\"\n\nint main() {\n  int N;\n  cin >>\
    \ N;\n  using LCT = LinkCutTreeSubTree< Diameter< int >, 200000 >;\n  LCT lct;\n\
    \  vector< vector< pair< int, int > > > g(N);\n  for(int i = 1; i < N; i++) {\n\
    \    int x, y, z;\n    cin >> x >> y >> z;\n    g[x].emplace_back(y, z);\n   \
    \ g[y].emplace_back(x, z);\n  }\n  vector< LCT::Node * > vs(N), es(N);\n  auto\
    \ rec = MFP([&](auto rec, int idx, int par) -> void {\n    vs[idx] = lct.alloc(make_pair(true,\
    \ 1));\n    for(auto &e : g[idx]) {\n      if(e.first == par) continue;\n    \
    \  rec(e.first, idx);\n      es[e.first] = lct.alloc(make_pair(false, e.second));\n\
    \      lct.link(vs[e.first], es[e.first]);\n      lct.link(es[e.first], vs[idx]);\n\
    \    }\n  });\n  rec(0, -1);\n  lct.expose(vs[0]);\n  cout << vs[0]->sum.diameter\
    \ << \"\\n\";\n}\n"
  dependsOn:
  - template/template.cpp
  - structure/develop/array-pool.cpp
  - structure/develop/link-cut-tree-subtree.cpp
  - structure/develop/splay-tree.cpp
  - structure/develop/diameter.cpp
  isVerificationFile: true
  path: test/verify/aoj-grl-5-a-2.test.cpp
  requiredBy: []
  timestamp: '2021-05-01 00:06:55+09:00'
  verificationStatus: TEST_WRONG_ANSWER
  verifiedWith: []
documentation_of: test/verify/aoj-grl-5-a-2.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-grl-5-a-2.test.cpp
- /verify/test/verify/aoj-grl-5-a-2.test.cpp.html
title: test/verify/aoj-grl-5-a-2.test.cpp
---
