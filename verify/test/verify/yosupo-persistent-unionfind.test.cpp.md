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


# :heavy_check_mark: test/verify/yosupo-persistent-unionfind.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-persistent-unionfind.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-01 18:25:23+09:00


* see: <a href="https://judge.yosupo.jp/problem/persistent_unionfind">https://judge.yosupo.jp/problem/persistent_unionfind</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/others/persistent-array.cpp.html">structure/others/persistent-array.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/union-find/persistent-union-find.cpp.html">Persistent-Union-Find(永続Union-Find) <small>(structure/union-find/persistent-union-find.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/persistent_unionfind"

#include "../../template/template.cpp"

#include "../../structure/others/persistent-array.cpp"
#include "../../structure/union-find/persistent-union-find.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< PersistentUnionFind > uf(Q + 1);
  uf[0] = PersistentUnionFind(N);
  for(int i = 1; i <= Q; i++) {
    int t, k, u, v;
    cin >> t >> k >> u >> v;
    ++k;
    if(t == 0) {
      uf[i] = uf[k];
      uf[i].unite(u, v);
    } else {
      cout << (uf[k].find(u) == uf[k].find(v)) << "\n";
    }
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-persistent-unionfind.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/persistent_unionfind"

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
#line 4 "test/verify/yosupo-persistent-unionfind.test.cpp"

#line 1 "structure/others/persistent-array.cpp"
template< typename T, int LOG >
struct PersistentArray {
  struct Node {
    T data;
    Node *child[1 << LOG] = {};

    Node() {}

    Node(const T &data) : data(data) {}
  };

  Node *root;

  PersistentArray() : root(nullptr) {}

  T get(Node *t, int k) {
    if(k == 0) return t->data;
    return get(t->child[k & ((1 << LOG) - 1)], k >> LOG);
  }

  T get(const int &k) {
    return get(root, k);
  }

  pair< Node *, T * > mutable_get(Node *t, int k) {
    t = t ? new Node(*t) : new Node();
    if(k == 0) return {t, &t->data};
    auto p = mutable_get(t->child[k & ((1 << LOG) - 1)], k >> LOG);
    t->child[k & ((1 << LOG) - 1)] = p.first;
    return {t, p.second};
  }

  T *mutable_get(const int &k) {
    auto ret = mutable_get(root, k);
    root = ret.first;
    return ret.second;
  }

  Node *build(Node *t, const T &data, int k) {
    if(!t) t = new Node();
    if(k == 0) {
      t->data = data;
      return t;
    }
    auto p = build(t->child[k & ((1 << LOG) - 1)], data, k >> LOG);
    t->child[k & ((1 << LOG) - 1)] = p;
    return t;
  }

  void build(const vector< T > &v) {
    root = nullptr;
    for(int i = 0; i < v.size(); i++) {
      root = build(root, v[i], i);
    }
  }
};

#line 1 "structure/union-find/persistent-union-find.cpp"
/*
 * @brief Persistent-Union-Find(永続Union-Find)
 */
struct PersistentUnionFind {
  PersistentArray< int, 3 > data;

  PersistentUnionFind() {}

  PersistentUnionFind(int sz) {
    data.build(vector< int >(sz, -1));
  }

  int find(int k) {
    int p = data.get(k);
    return p >= 0 ? find(p) : k;
  }

  int size(int k) {
    return (-data.get(find(k)));
  }

  bool unite(int x, int y) {
    x = find(x);
    y = find(y);
    if(x == y) return false;
    auto u = data.get(x);
    auto v = data.get(y);

    if(u < v) {
      auto a = data.mutable_get(x);
      *a += v;
      auto b = data.mutable_get(y);
      *b = x;
    } else {
      auto a = data.mutable_get(y);
      *a += u;
      auto b = data.mutable_get(x);
      *b = y;
    }
    return true;
  }
};
#line 7 "test/verify/yosupo-persistent-unionfind.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< PersistentUnionFind > uf(Q + 1);
  uf[0] = PersistentUnionFind(N);
  for(int i = 1; i <= Q; i++) {
    int t, k, u, v;
    cin >> t >> k >> u >> v;
    ++k;
    if(t == 0) {
      uf[i] = uf[k];
      uf[i].unite(u, v);
    } else {
      cout << (uf[k].find(u) == uf[k].find(v)) << "\n";
    }
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

