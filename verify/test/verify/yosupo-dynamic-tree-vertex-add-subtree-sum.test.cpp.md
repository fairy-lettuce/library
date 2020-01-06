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


# :heavy_check_mark: test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp

<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-07 02:17:06+09:00


* see: <a href="https://judge.yosupo.jp/problem/dynamic_tree_vertex_add_subtree_sum">https://judge.yosupo.jp/problem/dynamic_tree_vertex_add_subtree_sum</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/others/link-cut-tree-subtree.cpp.html">structure/others/link-cut-tree-subtree.cpp</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/dynamic_tree_vertex_add_subtree_sum"

#include "../../template/template.cpp"

#include "../../structure/others/link-cut-tree-subtree.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;


  struct Node {
    int64 sum, psum, csum, lsum;

    Node() : sum(0), lsum(0), psum(0), csum(0) {}

    void toggle() {
      swap(psum, csum);
    }

    void merge(int64 cost, const Node &parent, const Node &child) {
      sum = cost + parent.sum + child.sum + lsum;
      psum = parent.psum + cost + lsum;
      csum = child.csum + cost + lsum;
    }

    void add(const Node &chsum) {
      lsum += chsum.sum;
    }

    void erase(const Node &chsum) {
      lsum -= chsum.sum;
    }
  } e;

  using LCT = LinkCutTreeSubtree< Node, int64 >;
  LCT lct(e);

  vector< int > A(N);
  cin >> A;

  vector< LCT::Node * > vs(N), es(N);
  for(int i = 0; i < N; i++) {
    vs[i] = lct.make_node(A[i]);
  }
  for(int i = 1; i < N; i++) {
    int a, b;
    cin >> a >> b;
    lct.evert(vs[b]);
    lct.link(vs[b], vs[a]);
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
      int P, X;
      cin >> P >> X;
      lct.set_key(vs[P], vs[P]->key + X);
    } else {
      int V, P;
      cin >> V >> P;
      lct.evert(vs[P]);
      cout << lct.query(vs[V]).csum << "\n";
    }
  }
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/dynamic_tree_vertex_add_subtree_sum"

#line 1 "test/verify/../../template/template.cpp"
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
#line 4 "test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp"

#line 1 "test/verify/../../structure/others/link-cut-tree-subtree.cpp"
template< typename SUM, typename KEY >
struct LinkCutTreeSubtree {
 
  struct Node {
    Node *l, *r, *p;
 
    KEY key;
    SUM sum;
 
    bool rev;
    int sz;
 
    bool is_root() const {
      return !p || (p->l != this && p->r != this);
    }
 
    Node(const KEY &key, const SUM &sum) :
        key(key), sum(sum), rev(false), sz(1),
        l(nullptr), r(nullptr), p(nullptr) {}
  };
 
  const SUM ident;
 
  LinkCutTreeSubtree(const SUM &ident) : ident(ident) {}
 
  Node *make_node(const KEY &key) {
    auto ret = new Node(key, ident);
    update(ret);
    return ret;
  }
 
  Node *set_key(Node *t, const KEY &key) {
    expose(t);
    t->key = key;
    update(t);
    return t;
  }
 
  void toggle(Node *t) {
    swap(t->l, t->r);
    t->sum.toggle();
    t->rev ^= true;
  }
 
  void push(Node *t) {
    if(t->rev) {
      if(t->l) toggle(t->l);
      if(t->r) toggle(t->r);
      t->rev = false;
    }
  }
 
 
  void update(Node *t) {
    t->sz = 1;
    if(t->l) t->sz += t->l->sz;
    if(t->r) t->sz += t->r->sz;
    t->sum.merge(t->key, t->l ? t->l->sum : ident, t->r ? t->r->sum : ident);
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
 
 
  Node *expose(Node *t) {
    Node *rp = nullptr;
    for(auto *cur = t; cur; cur = cur->p) {
      splay(cur);
      if(cur->r) cur->sum.add(cur->r->sum);
      cur->r = rp;
      if(cur->r) cur->sum.erase(cur->r->sum);
      update(cur);
      rp = cur;
    }
    splay(t);
    return rp;
  }
 
  void link(Node *child, Node *parent) {
    expose(child);
    expose(parent);
    child->p = parent;
    parent->r = child;
    update(parent);
  }
 
  void cut(Node *child) {
    expose(child);
    auto *parent = child->l;
    child->l = nullptr;
    parent->p = nullptr;
    update(child);
  }
 
  void evert(Node *t) {
    expose(t);
    toggle(t);
    push(t);
  }
 
  Node *lca(Node *u, Node *v) {
    if(get_root(u) != get_root(v)) return nullptr;
    expose(u);
    return expose(v);
  }
 
 
  Node *get_kth(Node *x, int k) {
    expose(x);
    while(x) {
      push(x);
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
      push(x);
      x = x->l;
    }
    return x;
  }
 
  SUM &query(Node *t) {
    expose(t);
    return t->sum;
  }
};
#line 6 "test/verify/yosupo-dynamic-tree-vertex-add-subtree-sum.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;


  struct Node {
    int64 sum, psum, csum, lsum;

    Node() : sum(0), lsum(0), psum(0), csum(0) {}

    void toggle() {
      swap(psum, csum);
    }

    void merge(int64 cost, const Node &parent, const Node &child) {
      sum = cost + parent.sum + child.sum + lsum;
      psum = parent.psum + cost + lsum;
      csum = child.csum + cost + lsum;
    }

    void add(const Node &chsum) {
      lsum += chsum.sum;
    }

    void erase(const Node &chsum) {
      lsum -= chsum.sum;
    }
  } e;

  using LCT = LinkCutTreeSubtree< Node, int64 >;
  LCT lct(e);

  vector< int > A(N);
  cin >> A;

  vector< LCT::Node * > vs(N), es(N);
  for(int i = 0; i < N; i++) {
    vs[i] = lct.make_node(A[i]);
  }
  for(int i = 1; i < N; i++) {
    int a, b;
    cin >> a >> b;
    lct.evert(vs[b]);
    lct.link(vs[b], vs[a]);
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
      int P, X;
      cin >> P >> X;
      lct.set_key(vs[P], vs[P]->key + X);
    } else {
      int V, P;
      cin >> V >> P;
      lct.evert(vs[P]);
      cout << lct.query(vs[V]).csum << "\n";
    }
  }
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

