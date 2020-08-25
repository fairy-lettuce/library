---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :heavy_check_mark: test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-19 01:56:15+09:00


* see: <a href="https://judge.yosupo.jp/problem/dynamic_tree_vertex_set_path_composite">https://judge.yosupo.jp/problem/dynamic_tree_vertex_set_path_composite</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/bbst/reversible-splay-tree.cpp.html">Reversible-Splay-Tree(反転可能Splay木) <small>(structure/bbst/reversible-splay-tree.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/others/link-cut-tree.cpp.html">Link-Cut-Tree <small>(structure/others/link-cut-tree.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/dynamic_tree_vertex_set_path_composite"

#include "../../template/template.cpp"

#include "../../structure/bbst/reversible-splay-tree.cpp"

#include "../../structure/others/link-cut-tree.cpp"

#include "../../math/combinatorics/mod-int.cpp"

using mint = ModInt< 998244353 >;

int main() {
  int N, Q;
  cin >> N >> Q;

  using pi = pair< mint, mint >;
  using pii = pair< pi, pi >;
  using LCT = LinkCutTree< ReversibleSplayTree, pair< pi, pi > >;
  auto f = [](const pi &x, const pi &y) { return pi(x.first * y.first, x.second * y.first + y.second); };
  auto ff = [&](const pii &a, const pii &b) { return pii(f(a.first, b.first), f(b.second, a.second)); };
  auto flip = [&](const pii &a) { return pii(a.second, a.first); };
  LCT lct(ff, flip, pii());

  vector< LCT::Node * > vs(N);
  for(int i = 0; i < N; i++) {
    mint x, y;
    cin >> x >> y;
    vs[i] = lct.alloc(pii(pi(x, y), pi(x, y)));
  }
  for(int i = 1; i < N; i++) {
    int a, b;
    cin >> a >> b;
    lct.evert(vs[a]);
    lct.link(vs[a], vs[b]);
  }

  while(Q--) {
    int T;
    cin >> T;
    if(T == 0) {
      int U, V, W, X;
      cin >> U >> V >> W >> X;
      lct.evert(vs[U]);
      lct.cut(vs[V]);
      lct.evert(vs[W]);
      lct.link(vs[W], vs[X]);
    } else if(T == 1) {
      int P;
      mint a, b;
      cin >> P >> a >> b;
      lct.expose(vs[P]);
      vs[P]->key = pii(pi(a, b), pi(a, b));
      lct.update(vs[P]);
    } else {
      int U, V;
      mint X;
      cin >> U >> V >> X;
      lct.evert(vs[U]);
      auto ret = lct.query(vs[V]).first;
      cout << ret.first * X + ret.second << "\n";
    }
  }
}



```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/dynamic_tree_vertex_set_path_composite"

#line 1 "template/template.cpp"
#include<bits/stdc++.h>

using namespace std;

using int64 = long long;
const int mod = 1e9 + 7;

const int64 infll = (1LL << 62) - 1;
const int inf = (1 << 30) - 1;

struct IoSetup {
  IoSetup() {
    cin.tie(nullptr);
    ios::sync_with_stdio(false);
    cout << fixed << setprecision(10);
    cerr << fixed << setprecision(10);
  }
} iosetup;


template< typename T1, typename T2 >
ostream &operator<<(ostream &os, const pair< T1, T2 >& p) {
  os << p.first << " " << p.second;
  return os;
}

template< typename T1, typename T2 >
istream &operator>>(istream &is, pair< T1, T2 > &p) {
  is >> p.first >> p.second;
  return is;
}

template< typename T >
ostream &operator<<(ostream &os, const vector< T > &v) {
  for(int i = 0; i < (int) v.size(); i++) {
    os << v[i] << (i + 1 != v.size() ? " " : "");
  }
  return os;
}

template< typename T >
istream &operator>>(istream &is, vector< T > &v) {
  for(T &in : v) is >> in;
  return is;
}

template< typename T1, typename T2 >
inline bool chmax(T1 &a, T2 b) { return a < b && (a = b, true); }

template< typename T1, typename T2 >
inline bool chmin(T1 &a, T2 b) { return a > b && (a = b, true); }

template< typename T = int64 >
vector< T > make_v(size_t a) {
  return vector< T >(a);
}

template< typename T, typename... Ts >
auto make_v(size_t a, Ts... ts) {
  return vector< decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));
}

template< typename T, typename V >
typename enable_if< is_class< T >::value == 0 >::type fill_v(T &t, const V &v) {
  t = v;
}

template< typename T, typename V >
typename enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {
  for(auto &e : t) fill_v(e, v);
}

template< typename F >
struct FixPoint : F {
  FixPoint(F &&f) : F(forward< F >(f)) {}
 
  template< typename... Args >
  decltype(auto) operator()(Args &&... args) const {
    return F::operator()(*this, forward< Args >(args)...);
  }
};
 
template< typename F >
inline decltype(auto) MFP(F &&f) {
  return FixPoint< F >{forward< F >(f)};
}
#line 4 "test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp"

#line 1 "structure/bbst/reversible-splay-tree.cpp"
/**
 * @brief Reversible-Splay-Tree(反転可能Splay木)
 */
template< typename Monoid = int, typename OperatorMonoid = void >
struct ReversibleSplayTree {
public:
  using F = function< Monoid(Monoid, Monoid) >;
  using S = function< Monoid(Monoid) >;

  struct Node {
    Node *l, *r, *p;
    Monoid key, sum;
    bool rev;
    size_t sz;

    bool is_root() const {
      return !p || (p->l != this && p->r != this);
    }

    Node(const Monoid &key) :
        key(key), sum(key), sz(1), rev(false),
        l(nullptr), r(nullptr), p(nullptr) {}
  };

  ReversibleSplayTree(const F &f, const Monoid &M1) :
      ReversibleSplayTree(f, [](const Monoid &a) { return a; }, M1) {}

  ReversibleSplayTree(const F &f, const S &s, const Monoid &M1) :
      f(f), s(s), M1(M1) {}


  inline size_t count(const Node *t) { return t ? t->sz : 0; }

  inline const Monoid &sum(const Node *t) { return t ? t->sum : M1; }

  Node *alloc(const Monoid &v = Monoid()) {
    return new Node(v);
  }

  void splay(Node *t) {
    push(t);
    while(!t->is_root()) {
      auto *q = t->p;
      if(q->is_root()) {
        push(q), push(t);
        if(q->l == t) rotr(t);
        else rotl(t);
      } else {
        auto *r = q->p;
        push(r), push(q), push(t);
        if(r->l == q) {
          if(q->l == t) rotr(q), rotr(t);
          else rotl(t), rotr(t);
        } else {
          if(q->r == t) rotl(q), rotl(t);
          else rotr(t), rotl(t);
        }
      }
    }
  }

  Node *push_front(Node *t, const Monoid &v = Monoid()) {
    if(!t) {
      t = alloc(v);
      return t;
    } else {
      splay(t);
      Node *cur = get_left(t), *z = alloc(v);
      splay(cur);
      z->p = cur;
      cur->l = z;
      splay(z);
      return z;
    }
  }

  Node *push_back(Node *t, const Monoid &v = Monoid()) {
    if(!t) {
      t = alloc(v);
      return t;
    } else {
      splay(t);
      Node *cur = get_right(t), *z = alloc(v);
      splay(cur);
      z->p = cur;
      cur->r = z;
      splay(z);
      return z;
    }
  }

  Node *erase(Node *t) {
    splay(t);
    Node *x = t->l, *y = t->r;
    delete t;
    if(!x) {
      t = y;
      if(t) t->p = nullptr;
    } else if(!y) {
      t = x;
      t->p = nullptr;
    } else {
      x->p = nullptr;
      t = get_right(x);
      splay(t);
      t->r = y;
      y->p = t;
    }
    return t;
  }

  Node *get_left(Node *t) const {
    while(t->l) t = t->l;
    return t;
  }

  Node *get_right(Node *t) const {
    while(t->r) t = t->r;
    return t;
  }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {nullptr, nullptr};
    push(t);
    if(k <= count(t->l)) {
      auto x = split(t->l, k);
      t->l = x.second;
      t->p = nullptr;
      if(x.second) x.second->p = t;
      return {x.first, update(t)};
    } else {
      auto x = split(t->r, k - count(t->l) - 1);
      t->r = x.first;
      t->p = nullptr;
      if(x.first) x.first->p = t;
      return {update(t), x.second};
    }
  }

  template< typename ... Args >
  Node *merge(Node *l, Args ...rest) {
    Node *r = merge(rest...);
    if(!l && !r) return nullptr;
    if(!l) return splay(r), r;
    if(!r) return splay(l), l;
    splay(l), splay(r);
    l = get_right(l);
    splay(l);
    l->r = r;
    r->p = l;
    update(l);
    return l;
  }

  void insert(Node *&t, int k, const Monoid &v) {
    splay(t);
    auto x = split(t, k);
    t = merge(merge(x.first, alloc(v)), x.second);
  }

  Monoid erase(Node *&t, int k) {
    splay(t);
    auto x = split(t, k);
    auto y = split(x.second, 1);
    auto v = y.first->c;
    delete y.first;
    t = merge(x.first, y.second);
    return v;
  }

  Monoid query(Node *&t, int a, int b) {
    splay(t);
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    auto ret = sum(y.first);
    t = merge(x.first, y.first, y.second);
    return ret;
  }

  Node *build(const vector< Monoid > &v) {
    return build(0, (int) v.size(), v);
  }

  void toggle(Node *t) {
    swap(t->l, t->r);
    t->sum = s(t->sum);
    t->rev ^= true;
  }

  Node *update(Node *t) {
    t->sz = 1;
    t->sum = t->key;
    if(t->l) t->sz += t->l->sz, t->sum = f(t->l->sum, t->sum);
    if(t->r) t->sz += t->r->sz, t->sum = f(t->sum, t->r->sum);
    return t;
  }

  tuple< Node *, Node *, Node * > split3(Node *t, int a, int b) {
    splay(t);
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    return make_tuple(x.first, y.first, y.second);
  }

  void push(Node *t) {
    if(t->rev) {
      if(t->l) toggle(t->l);
      if(t->r) toggle(t->r);
      t->rev = false;
    }
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    splay(t);
    sub_set_element(t, k, x);
  }

private:
  const Monoid M1;
  const F f;
  const S s;

  Node *build(int l, int r, const vector< Monoid > &v) {
    if(l + 1 >= r) return alloc(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *sub_set_element(Node *&t, int k, const Monoid &x) {
    push(t);
    if(k < count(t->l)) {
      return sub_set_element(t->l, k, x);
    } else if(k == count(t->l)) {
      t->key = x;
      splay(t);
      return t;
    } else {
      return sub_set_element(t->r, k - count(t->l) - 1, x);
    }
  }


  void rotr(Node *t) {
    auto *x = t->p, *y = x->p;
    if((x->l = t->r)) t->r->p = x;
    t->r = x, x->p = t;
    update(x), update(t);
    if((t->p = y)) {
      if(y->l == x) y->l = t;
      if(y->r == x) y->r = t;
      update(y);
    }
  }

  void rotl(Node *t) {
    auto *x = t->p, *y = x->p;
    if((x->r = t->l)) t->l->p = x;
    t->l = x, x->p = t;
    update(x), update(t);
    if((t->p = y)) {
      if(y->l == x) y->l = t;
      if(y->r == x) y->r = t;
      update(y);
    }
  }

  Node *merge(Node *l) {
    return l;
  }
};
#line 6 "test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp"

#line 1 "structure/others/link-cut-tree.cpp"
/**
 * @brief Link-Cut-Tree
 */
template< template< typename, typename > typename ST, typename Monoid = int, typename OperatorMonoid = Monoid >
struct LinkCutTree : ST< Monoid, OperatorMonoid > {
  using LST = ST< Monoid, OperatorMonoid >;
  using ST< Monoid, OperatorMonoid >::ST;
  using Node = typename LST::Node;

  Node *expose(Node *t) {
    Node *rp = nullptr;
    for(Node *cur = t; cur; cur = cur->p) {
      this->splay(cur);
      cur->r = rp;
      this->update(cur);
      rp = cur;
    }
    this->splay(t);
    return rp;
  }

  void link(Node *child, Node *parent) {
    expose(child);
    expose(parent);
    child->p = parent;
    parent->r = child;
    this->update(parent);
  }

  void cut(Node *child) {
    expose(child);
    auto *parent = child->l;
    child->l = nullptr;
    parent->p = nullptr;
    this->update(child);
  }

  void evert(Node *t) {
    expose(t);
    this->toggle(t);
    this->push(t);
  }

  Node *lca(Node *u, Node *v) {
    if(get_root(u) != get_root(v)) return nullptr;
    expose(u);
    return expose(v);
  }

  void set_propagate(Node *t, const OperatorMonoid &x) {
    expose(t);
    LST::set_propagate(t, x);
  }

  Node *get_kth(Node *x, int k) {
    expose(x);
    while(x) {
      this->push(x);
      if(x->r && x->r->sz > k) {
        x = x->r;
      } else {
        if(x->r) k -= x->r->sz;
        if(k == 0) return x;
        k -= 1;
        x = x->l;
      }
    }
    return nullptr;
  }

  Node *get_root(Node *x) {
    expose(x);
    while(x->l) {
      this->push(x);
      x = x->l;
    }
    return x;
  }

  const Monoid &query(Node *t) {
    expose(t);
    return t->sum;
  }
};
#line 8 "test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp"

#line 1 "math/combinatorics/mod-int.cpp"
template< int mod >
struct ModInt {
  int x;

  ModInt() : x(0) {}

  ModInt(int64_t y) : x(y >= 0 ? y % mod : (mod - (-y) % mod) % mod) {}

  ModInt &operator+=(const ModInt &p) {
    if((x += p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator-=(const ModInt &p) {
    if((x += mod - p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator*=(const ModInt &p) {
    x = (int) (1LL * x * p.x % mod);
    return *this;
  }

  ModInt &operator/=(const ModInt &p) {
    *this *= p.inverse();
    return *this;
  }

  ModInt operator-() const { return ModInt(-x); }

  ModInt operator+(const ModInt &p) const { return ModInt(*this) += p; }

  ModInt operator-(const ModInt &p) const { return ModInt(*this) -= p; }

  ModInt operator*(const ModInt &p) const { return ModInt(*this) *= p; }

  ModInt operator/(const ModInt &p) const { return ModInt(*this) /= p; }

  bool operator==(const ModInt &p) const { return x == p.x; }

  bool operator!=(const ModInt &p) const { return x != p.x; }

  ModInt inverse() const {
    int a = x, b = mod, u = 1, v = 0, t;
    while(b > 0) {
      t = a / b;
      swap(a -= t * b, b);
      swap(u -= t * v, v);
    }
    return ModInt(u);
  }

  ModInt pow(int64_t n) const {
    ModInt ret(1), mul(x);
    while(n > 0) {
      if(n & 1) ret *= mul;
      mul *= mul;
      n >>= 1;
    }
    return ret;
  }

  friend ostream &operator<<(ostream &os, const ModInt &p) {
    return os << p.x;
  }

  friend istream &operator>>(istream &is, ModInt &a) {
    int64_t t;
    is >> t;
    a = ModInt< mod >(t);
    return (is);
  }

  static int get_mod() { return mod; }
};

using modint = ModInt< mod >;
#line 10 "test/verify/yosupo-dynamic-tree-vertex-set-path-composite.test.cpp"

using mint = ModInt< 998244353 >;

int main() {
  int N, Q;
  cin >> N >> Q;

  using pi = pair< mint, mint >;
  using pii = pair< pi, pi >;
  using LCT = LinkCutTree< ReversibleSplayTree, pair< pi, pi > >;
  auto f = [](const pi &x, const pi &y) { return pi(x.first * y.first, x.second * y.first + y.second); };
  auto ff = [&](const pii &a, const pii &b) { return pii(f(a.first, b.first), f(b.second, a.second)); };
  auto flip = [&](const pii &a) { return pii(a.second, a.first); };
  LCT lct(ff, flip, pii());

  vector< LCT::Node * > vs(N);
  for(int i = 0; i < N; i++) {
    mint x, y;
    cin >> x >> y;
    vs[i] = lct.alloc(pii(pi(x, y), pi(x, y)));
  }
  for(int i = 1; i < N; i++) {
    int a, b;
    cin >> a >> b;
    lct.evert(vs[a]);
    lct.link(vs[a], vs[b]);
  }

  while(Q--) {
    int T;
    cin >> T;
    if(T == 0) {
      int U, V, W, X;
      cin >> U >> V >> W >> X;
      lct.evert(vs[U]);
      lct.cut(vs[V]);
      lct.evert(vs[W]);
      lct.link(vs[W], vs[X]);
    } else if(T == 1) {
      int P;
      mint a, b;
      cin >> P >> a >> b;
      lct.expose(vs[P]);
      vs[P]->key = pii(pi(a, b), pi(a, b));
      lct.update(vs[P]);
    } else {
      int U, V;
      mint X;
      cin >> U >> V >> X;
      lct.evert(vs[U]);
      auto ret = lct.query(vs[V]).first;
      cout << ret.first * X + ret.second << "\n";
    }
  }
}



```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

