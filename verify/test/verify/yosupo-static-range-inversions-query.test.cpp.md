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


# :heavy_check_mark: test/verify/yosupo-static-range-inversions-query.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-static-range-inversions-query.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-12 02:55:35+09:00


* see: <a href="https://judge.yosupo.jp/problem/static_range_inversions_query">https://judge.yosupo.jp/problem/static_range_inversions_query</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/other/mo.cpp.html">Mo's Algorithm <small>(other/mo.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/structure/others/binary-indexed-tree.cpp.html">Binary-Indexed-Tree(BIT) <small>(structure/others/binary-indexed-tree.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/static_range_inversions_query"

#include "../../template/template.cpp"

#include "../../other/mo.cpp"
#include "../../structure/others/binary-indexed-tree.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > A(N);
  for(auto &a : A) cin >> a;
  Mo mo(N);
  for(int i = 0; i < Q; i++) {
    int l, r;
    cin >> l >> r;
    mo.add(l, r);
  }
  vector< int > xs{A};
  sort(begin(xs), end(xs));
  xs.erase(unique(begin(xs), end(xs)), end(xs));
  for(auto &a : A) a = lower_bound(begin(xs), end(xs), a) - begin(xs);
  BinaryIndexedTree< int > bit(xs.size());
  int64_t inv = 0, all = 0;
  vector< int64_t > ans(Q);
  auto add_left = [&](int idx) {
    inv += bit.query(A[idx] - 1);
    bit.add(A[idx], 1);
    all++;
  };
  auto add_right = [&](int idx) {
    inv += all - bit.query(A[idx]);
    bit.add(A[idx], 1);
    ++all;
  };
  auto erase_left = [&](int idx) {
    inv -= bit.query(A[idx] - 1);
    bit.add(A[idx], -1);
    --all;
  };
  auto erase_right = [&](int idx) {
    inv -= all - bit.query(A[idx]);
    bit.add(A[idx], -1);
    --all;
  };
  auto out = [&](int idx) {
    ans[idx] = inv;
  };
  mo.build(add_left, add_right, erase_left, erase_right, out);
  for(auto &p : ans) cout << p << "\n";
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-static-range-inversions-query.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/static_range_inversions_query"

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
#line 4 "test/verify/yosupo-static-range-inversions-query.test.cpp"

#line 1 "other/mo.cpp"
/**
 * @brief Mo's Algorithm
 */
struct Mo {
  int n;
  vector< pair< int, int > > lr;

  explicit Mo(int n) : n(n) {}

  void add(int l, int r) { /* [l, r) */
    lr.emplace_back(l, r);
  }

  template< typename AL, typename AR, typename EL, typename ER, typename O >
  void build(const AL &add_left, const AR &add_right, const EL &erase_left, const ER &erase_right, const O &out) {
    int q = (int) lr.size();
    int bs = n / min< int >(n, sqrt(q));
    vector< int > ord(q);
    iota(begin(ord), end(ord), 0);
    sort(begin(ord), end(ord), [&](int a, int b) {
      int ablock = lr[a].first / bs, bblock = lr[b].first / bs;
      if(ablock != bblock) return ablock < bblock;
      return (ablock & 1) ? lr[a].second > lr[b].second : lr[a].second < lr[b].second;
    });
    int l = 0, r = 0;
    for(auto idx : ord) {
      while(l > lr[idx].first) add_left(--l);
      while(r < lr[idx].second) add_right(r++);
      while(l < lr[idx].first) erase_left(l++);
      while(r > lr[idx].second) erase_right(--r);
      out(idx);
    }
  }

  template< typename A, typename E, typename O >
  void build(const A &add, const E &erase, const O &out) {
    build(add, add, erase, erase, out);
  }
};
#line 1 "structure/others/binary-indexed-tree.cpp"
/**
 * @brief Binary-Indexed-Tree(BIT)
 * @docs docs/binary-indexed-tree.md
 */
template< typename T >
struct BinaryIndexedTree {
  vector< T > data;

  BinaryIndexedTree() = default;

  explicit BinaryIndexedTree(size_t sz) : data(sz + 1, 0) {}

  explicit BinaryIndexedTree(const vector< T > &vs) : data(vs.size() + 1, 0) {
    for(size_t i = 0; i < vs.size(); i++) data[i + 1] = vs[i];
    for(size_t i = 1; i < data.size(); i++) {
      size_t j = i + (i & -i);
      if(j < data.size()) data[j] += data[i];
    }
  }

  void add(int k, const T &x) {
    for(++k; k < (int) data.size(); k += k & -k) data[k] += x;
  }

  T query(int k) const {
    T ret = T();
    for(++k; k > 0; k -= k & -k) ret += data[k];
    return ret;
  }

  int lower_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] < x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }

  int upper_bound(T x) const {
    int i = 0;
    for(int k = 1 << (__lg(data.size() - 1) + 1); k > 0; k >>= 1) {
      if(i + k < data.size() && data[i + k] <= x) {
        x -= data[i + k];
        i += k;
      }
    }
    return i;
  }
};
#line 7 "test/verify/yosupo-static-range-inversions-query.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > A(N);
  for(auto &a : A) cin >> a;
  Mo mo(N);
  for(int i = 0; i < Q; i++) {
    int l, r;
    cin >> l >> r;
    mo.add(l, r);
  }
  vector< int > xs{A};
  sort(begin(xs), end(xs));
  xs.erase(unique(begin(xs), end(xs)), end(xs));
  for(auto &a : A) a = lower_bound(begin(xs), end(xs), a) - begin(xs);
  BinaryIndexedTree< int > bit(xs.size());
  int64_t inv = 0, all = 0;
  vector< int64_t > ans(Q);
  auto add_left = [&](int idx) {
    inv += bit.query(A[idx] - 1);
    bit.add(A[idx], 1);
    all++;
  };
  auto add_right = [&](int idx) {
    inv += all - bit.query(A[idx]);
    bit.add(A[idx], 1);
    ++all;
  };
  auto erase_left = [&](int idx) {
    inv -= bit.query(A[idx] - 1);
    bit.add(A[idx], -1);
    --all;
  };
  auto erase_right = [&](int idx) {
    inv -= all - bit.query(A[idx]);
    bit.add(A[idx], -1);
    --all;
  };
  auto out = [&](int idx) {
    ans[idx] = inv;
  };
  mo.build(add_left, add_right, erase_left, erase_right, out);
  for(auto &p : ans) cout << p << "\n";
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

