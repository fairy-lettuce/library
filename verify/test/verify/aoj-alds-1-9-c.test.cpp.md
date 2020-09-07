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


# :heavy_check_mark: test/verify/aoj-alds-1-9-c.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/aoj-alds-1-9-c.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-21 01:30:35+09:00


* see: <a href="http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_9_C">http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_9_C</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/heap/leftist-heap.cpp.html">Leftist-Heap <small>(structure/heap/leftist-heap.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_9_C"

#include "../../template/template.cpp"

#include "../../structure/heap/leftist-heap.cpp"

int main() {
  string s;
  LeftistHeap< int, false > que;
  auto root = que.make_root();
  while(cin >> s, s != "end") {
    if(s == "insert") {
      int x;
      cin >> x;
      root = que.push(root, x);
    } else {
      cout << root->key << "\n";
      root = que.pop(root);
    }
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/aoj-alds-1-9-c.test.cpp"
#define PROBLEM "http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_9_C"

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
#line 4 "test/verify/aoj-alds-1-9-c.test.cpp"

#line 1 "structure/heap/leftist-heap.cpp"
/**
 * @brief Leftist-Heap
 */
template< typename T, bool isMin = true >
struct LeftistHeap {
  struct Node {
    Node *l, *r;
    int s;
    T key;
    int idx;

    explicit Node(const T &key, int idx) : key(key), s(1), l(nullptr), r(nullptr), idx(idx) {}
  };

  LeftistHeap() = default;

  virtual Node *clone(Node *t) {
    return t;
  }

  Node *alloc(const T &key, int idx = -1) {
    return new Node(key, idx);
  }

  Node *meld(Node *a, Node *b) {
    if(!a || !b) return a ? a : b;
    if((a->key < b->key) ^ isMin) swap(a, b);
    a = clone(a);
    a->r = meld(a->r, b);
    if(!a->l || a->l->s < a->r->s) swap(a->l, a->r);
    a->s = (a->r ? a->r->s : 0) + 1;
    return a;
  }

  Node *push(Node *t, const T &key, int idx = -1) {
    return meld(t, alloc(key, idx));
  }

  Node *pop(Node *t) {
    assert(t != nullptr);
    return meld(t->l, t->r);
  }

  Node *make_root() {
    return nullptr;
  }
};
#line 6 "test/verify/aoj-alds-1-9-c.test.cpp"

int main() {
  string s;
  LeftistHeap< int, false > que;
  auto root = que.make_root();
  while(cin >> s, s != "end") {
    if(s == "insert") {
      int x;
      cin >> x;
      root = que.push(root, x);
    } else {
      cout << root->key << "\n";
      root = que.pop(root);
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

