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


# :heavy_check_mark: test/verify/yukicoder-184.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-184.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-03 21:44:16+09:00


* see: <a href="https://yukicoder.me/problems/no/184">https://yukicoder.me/problems/no/184</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/math/matrix/binary-basis.cpp.html">math/matrix/binary-basis.cpp</a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://yukicoder.me/problems/no/184"

#include "../../template/template.cpp"

#include "../../math/matrix/binary-basis.cpp"

int main() {
  int N;
  cin >> N;
  BinaryBasis< int64 > bb;
  for(int i = 0; i < N; i++) {
    int64 x;
    cin >> x;
    bb.add(x);
  }
  cout << (1LL << bb.size()) << "\n";
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-184.test.cpp"
#define PROBLEM "https://yukicoder.me/problems/no/184"

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
#line 4 "test/verify/yukicoder-184.test.cpp"

#line 1 "math/matrix/binary-basis.cpp"
template< typename T >
struct BinaryBasis {
  vector< T > basis;
  bool update;

  BinaryBasis() : update(false) {}

  bool add(T bit) {
    for(auto &p : basis) {
      bit = min(bit, bit ^ p);
    }
    if(bit) {
      basis.emplace_back(bit);
      return update = true;
    } else {
      return false;
    }
  }

  bool check(T bit) const {
    for(auto &p : basis) {
      bit = min(bit, bit ^ p);
    }
    return bit == 0;
  }

  void normalize() {
    sweep();
    for(int i = (int) basis.size() - 1; i >= 0; i--) {
      for(int j = i - 1; j >= 0; j--) chmin(basis[i], basis[i] ^ basis[j]);
    }
  }

  void sweep() {
    if(exchange(update, false)) {
      sort(begin(basis), end(basis));
    }
  }

  bool operator==(BinaryBasis< T > &a) {
    normalize(), a.normalize();
    return basis == a.basis;
  }

  T get_kth(int64_t k) { /* 0-indexed */
    if((1LL << basis.size()) <= k) {
      return -1;
    }
    T ret = T();
    sweep();
    for(int i = (int) basis.size() - 1; i >= 0; i--) {
      if(k < (1LL << i)) {
        ret = min(ret, ret ^ basis[i]);
      } else {
        k -= 1LL << i;
        ret = max(ret, ret ^ basis[i]);
      }
    }
    return ret;
  }

  size_t size() const {
    return basis.size();
  }
};
#line 6 "test/verify/yukicoder-184.test.cpp"

int main() {
  int N;
  cin >> N;
  BinaryBasis< int64 > bb;
  for(int i = 0; i < N; i++) {
    int64 x;
    cin >> x;
    bb.add(x);
  }
  cout << (1LL << bb.size()) << "\n";
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

