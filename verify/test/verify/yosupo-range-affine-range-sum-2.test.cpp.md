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


# :heavy_check_mark: test/verify/yosupo-range-affine-range-sum-2.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-range-affine-range-sum-2.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-14 23:23:31+09:00


* see: <a href="https://judge.yosupo.jp/problem/range_affine_range_sum">https://judge.yosupo.jp/problem/range_affine_range_sum</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/other/vector-pool.cpp.html">other/vector-pool.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/bbst/lazy-red-black-tree.cpp.html">Lazy-Red-Black-Tree(遅延伝搬赤黒木) <small>(structure/bbst/lazy-red-black-tree.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/range_affine_range_sum"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"

#include "../../other/vector-pool.cpp"

#include "../../structure/bbst/lazy-red-black-tree.cpp"

using mint = ModInt< 998244353 >;

int main() {
  int N, Q;
  cin >> N >> Q;
  using pi = pair< mint, int >;
  using qi = pair< mint, mint >;
  auto f = [](const pi &a, const pi &b) -> pi {
    return {a.first + b.first, a.second + b.second};
  };
  auto g = [](const pi &a, const qi &b) -> pi {
    return {a.first * b.first + mint(a.second) * b.second, a.second};
  };
  auto h = [](const qi &a, const qi &b) -> qi {
    return {a.first * b.first, a.second * b.first + b.second};
  };
  LazyRedBlackTree< pi, qi, decltype(f), decltype(g), decltype(h) > rbt(2 * N, f, g, h, pi(0, 0), pi(1, 0));
  vector< pi > A(N);
  for(int i = 0; i < N; i++) {
    mint a;
    cin >> a;
    A[i] = {a, 1};
  }
  auto root = rbt.build(A);
  for(int i = 0; i < Q; i++) {
    int t;
    cin >> t;
    if(t == 0) {
      int l, r;
      mint b, c;
      cin >> l >> r >> b >> c;
      rbt.set_propagate(root, l, r, qi(b, c));
    } else {
      int l, r;
      cin >> l >> r;
      cout << rbt.query(root, l, r).first << "\n";
    }
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-range-affine-range-sum-2.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/range_affine_range_sum"

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
#line 4 "test/verify/yosupo-range-affine-range-sum-2.test.cpp"

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
#line 6 "test/verify/yosupo-range-affine-range-sum-2.test.cpp"

#line 1 "other/vector-pool.cpp"
template< class T >
struct VectorPool {
  vector< T > pool;
  vector< T * > stock;
  int ptr;

  VectorPool() = default;

  VectorPool(int sz) : pool(sz), stock(sz) {}

  inline T *alloc() { return stock[--ptr]; }

  inline void free(T *t) { stock[ptr++] = t; }

  void clear() {
    ptr = (int) pool.size();
    for(int i = 0; i < pool.size(); i++) stock[i] = &pool[i];
  }
};
#line 8 "test/verify/yosupo-range-affine-range-sum-2.test.cpp"

#line 1 "structure/bbst/lazy-red-black-tree.cpp"
/**
 * @brief Lazy-Red-Black-Tree(遅延伝搬赤黒木)
 * @docs docs/lazy-red-black-tree.md
 */
template< typename Monoid, typename OperatorMonoid, typename F, typename G, typename H >
struct LazyRedBlackTree {
public:
  enum COLOR {
    BLACK, RED
  };

  struct Node {
    Node *l, *r;
    COLOR color;
    int level, cnt;
    Monoid key, sum;
    OperatorMonoid lazy;

    Node() {}

    Node(const Monoid &k, const OperatorMonoid &laz) :
        key(k), sum(k), l(nullptr), r(nullptr), color(BLACK), level(0), cnt(1), lazy(laz) {}

    Node(Node *l, Node *r, const Monoid &k, const OperatorMonoid &laz) :
        key(k), color(RED), l(l), r(r), lazy(laz) {}

    bool is_leaf() const {
      return l == nullptr;
    }
  };

private:
  Node *propagate(Node *t) {
    t = clone(t);
    if(t->lazy != OM0) {
      if(t->is_leaf()) {
        t->key = g(t->key, t->lazy);
      } else {
        if(t->l) {
          t->l = clone(t->l);
          t->l->lazy = h(t->l->lazy, t->lazy);
          t->l->sum = g(t->l->sum, t->lazy);
        }
        if(t->r) {
          t->r = clone(t->r);
          t->r->lazy = h(t->r->lazy, t->lazy);
          t->r->sum = g(t->r->sum, t->lazy);
        }
      }
      t->lazy = OM0;
    }
    return update(t);
  }

  inline Node *alloc(Node *l, Node *r) {
    auto t = &(*pool.alloc() = Node(l, r, M1, OM0));
    return update(t);
  }

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *rotate(Node *t, bool b) {
    t = propagate(t);
    Node *s;
    if(b) {
      s = propagate(t->l);
      t->l = s->r;
      s->r = t;
    } else {
      s = propagate(t->r);
      t->r = s->l;
      s->l = t;
    }
    update(t);
    return update(s);
  }

  Node *submerge(Node *l, Node *r) {
    if(l->level < r->level) {
      r = propagate(r);
      Node *c = (r->l = submerge(l, r->l));
      if(r->color == BLACK && c->color == RED && c->l && c->l->color == RED) {
        r->color = RED;
        c->color = BLACK;
        if(r->r->color == BLACK) return rotate(r, true);
        r->r->color = BLACK;
      }
      return update(r);
    }
    if(l->level > r->level) {
      l = propagate(l);
      Node *c = (l->r = submerge(l->r, r));
      if(l->color == BLACK && c->color == RED && c->r && c->r->color == RED) {
        l->color = RED;
        c->color = BLACK;
        if(l->l->color == BLACK) return rotate(l, false);
        l->l->color = BLACK;
      }
      return update(l);
    }
    return alloc(l, r);
  }

  Node *build(int l, int r, const vector< Monoid > &v) {
    if(l + 1 >= r) return alloc(v[l]);
    return merge(build(l, (l + r) >> 1, v), build((l + r) >> 1, r, v));
  }

  Node *update(Node *t) {
    t->cnt = count(t->l) + count(t->r) + t->is_leaf();
    t->level = t->is_leaf() ? 0 : t->l->level + (t->l->color == BLACK);
    t->sum = f(f(sum(t->l), t->key), sum(t->r));
    return t;
  }

  void dump(Node *r, typename vector< Monoid >::iterator &it, OperatorMonoid lazy) {
    if(r->lazy != OM0) lazy = h(lazy, r->lazy);
    if(r->is_leaf()) {
      *it++ = g(r->key, lazy);
      return;
    }
    dump(r->l, it, lazy);
    dump(r->r, it, lazy);
  }

  Node *merge(Node *l) {
    return l;
  }

public:

  VectorPool< Node > pool;
  const F f;
  const G g;
  const H h;
  const OperatorMonoid OM0;
  const Monoid M1;

  LazyRedBlackTree(int sz, const F &f, const G &g, const H &h, const Monoid &M1, const OperatorMonoid &OM0) :
      pool(sz), M1(M1), OM0(OM0), f(f), g(g), h(h) { pool.clear(); }


  inline Node *alloc(const Monoid &key) {
    return &(*pool.alloc() = Node(key, OM0));
  }

  inline int count(const Node *t) { return t ? t->cnt : 0; }

  inline const Monoid &sum(const Node *t) { return t ? t->sum : M1; }

  pair< Node *, Node * > split(Node *t, int k) {
    if(!t) return {nullptr, nullptr};
    t = propagate(t);
    if(k == 0) return {nullptr, t};
    if(k >= count(t)) return {t, nullptr};
    Node *l = t->l, *r = t->r;
    pool.free(t);
    if(k < count(l)) {
      auto pp = split(l, k);
      return {pp.first, merge(pp.second, r)};
    }
    if(k > count(l)) {
      auto pp = split(r, k - count(l));
      return {merge(l, pp.first), pp.second};
    }
    return {l, r};
  }

  tuple< Node *, Node *, Node * > split3(Node *t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    return make_tuple(x.first, y.first, y.second);
  }

  template< typename ... Args >
  Node *merge(Node *l, Args ...rest) {
    Node *r = merge(rest...);
    if(!l || !r) return l ? l : r;
    Node *c = submerge(l, r);
    c->color = BLACK;
    return c;
  }

  Node *build(const vector< Monoid > &v) {
    return build(0, (int) v.size(), v);
  }

  vector< Monoid > dump(Node *r) {
    vector< Monoid > v((size_t) count(r));
    auto it = begin(v);
    dump(r, it, OM0);
    return v;
  }

  string to_string(Node *r) {
    auto s = dump(r);
    string ret;
    for(int i = 0; i < s.size(); i++) {
      ret += std::to_string(s[i]);
      ret += ", ";
    }
    return ret;
  }

  void insert(Node *&t, int k, const Monoid &v) {
    auto x = split(t, k);
    t = merge(merge(x.first, alloc(v)), x.second);
  }

  Monoid erase(Node *&t, int k) {
    auto x = split(t, k);
    auto y = split(x.second, 1);
    auto v = y.first->key;
    pool.free(y.first);
    t = merge(x.first, y.second);
    return v;
  }

  Monoid query(Node *&t, int a, int b) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    Monoid ret = sum(y.first);
    t = merge(x.first, y.first, y.second);
    return ret;
  }

  void set_propagate(Node *&t, int a, int b, const OperatorMonoid &pp) {
    auto x = split(t, a);
    auto y = split(x.second, b - a);
    y.first->lazy = h(y.first->lazy, pp);
    t = merge(x.first, propagate(y.first), y.second);
  }

  void set_element(Node *&t, int k, const Monoid &x) {
    t = propagate(t);
    if(t->is_leaf()) {
      t->key = t->sum = x;
      return;
    }
    if(k < count(t->l)) set_element(t->l, k, x);
    else set_element(t->r, k - count(t->l), x);
    t = update(t);
  }

  void push_front(Node *&t, const Monoid &v) {
    t = merge(alloc(v), t);
  }

  void push_back(Node *&t, const Monoid &v) {
    t = merge(t, alloc(v));
  }

  Monoid pop_front(Node *&t) {
    auto ret = split(t, 1);
    t = ret.second;
    return ret.first->key;
  }

  Monoid pop_back(Node *&t) {
    auto ret = split(t, count(t) - 1);
    t = ret.first;
    return ret.second->key;
  }
};
#line 10 "test/verify/yosupo-range-affine-range-sum-2.test.cpp"

using mint = ModInt< 998244353 >;

int main() {
  int N, Q;
  cin >> N >> Q;
  using pi = pair< mint, int >;
  using qi = pair< mint, mint >;
  auto f = [](const pi &a, const pi &b) -> pi {
    return {a.first + b.first, a.second + b.second};
  };
  auto g = [](const pi &a, const qi &b) -> pi {
    return {a.first * b.first + mint(a.second) * b.second, a.second};
  };
  auto h = [](const qi &a, const qi &b) -> qi {
    return {a.first * b.first, a.second * b.first + b.second};
  };
  LazyRedBlackTree< pi, qi, decltype(f), decltype(g), decltype(h) > rbt(2 * N, f, g, h, pi(0, 0), pi(1, 0));
  vector< pi > A(N);
  for(int i = 0; i < N; i++) {
    mint a;
    cin >> a;
    A[i] = {a, 1};
  }
  auto root = rbt.build(A);
  for(int i = 0; i < Q; i++) {
    int t;
    cin >> t;
    if(t == 0) {
      int l, r;
      mint b, c;
      cin >> l >> r >> b >> c;
      rbt.set_propagate(root, l, r, qi(b, c));
    } else {
      int l, r;
      cin >> l >> r;
      cout << rbt.query(root, l, r).first << "\n";
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

