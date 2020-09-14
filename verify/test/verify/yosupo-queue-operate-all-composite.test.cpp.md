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


# :heavy_check_mark: test/verify/yosupo-queue-operate-all-composite.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-queue-operate-all-composite.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-05-15 00:40:42+09:00


* see: <a href="https://judge.yosupo.jp/problem/queue_operate_all_composite">https://judge.yosupo.jp/problem/queue_operate_all_composite</a>


## Depends on

* :question: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/structure/others/sliding-window-aggregation.cpp.html">structure/others/sliding-window-aggregation.cpp</a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/queue_operate_all_composite"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"

#include "../../structure/others/sliding-window-aggregation.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int Q;
  cin >> Q;
  using pi = pair< mint, mint >;
  auto f = [](const pi &a, const pi &b) -> pi {
    return {a.first * b.first, a.second * b.first + b.second};
  };
  SlidingWindowAggregation< pi > swa(f);
  while(Q--) {
    int t;
    cin >> t;
    if(t == 0) {
      mint a, b;
      cin >> a >> b;
      swa.push(pi(a, b));
    } else if(t == 1) {
      swa.pop();
    } else {
      mint x;
      cin >> x;
      if(swa.empty()) {
        cout << x << "\n";
      } else {
        auto s = swa.fold_all();
        cout << s.first * x + s.second << "\n";
      }
    }
  }
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-queue-operate-all-composite.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/queue_operate_all_composite"

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
#line 4 "test/verify/yosupo-queue-operate-all-composite.test.cpp"

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
#line 6 "test/verify/yosupo-queue-operate-all-composite.test.cpp"

#line 1 "structure/others/sliding-window-aggregation.cpp"
template< typename SemiGroup >
struct SlidingWindowAggregation {
  using F = function< SemiGroup(SemiGroup, SemiGroup) >;
 
  struct Node {
    SemiGroup val, sum;
 
    Node(const SemiGroup &val, const SemiGroup &sum) : val(val), sum(sum) {}
  };
 
  SlidingWindowAggregation(F f) : f(f) {}
 
 
  const F f;
  stack< Node > front, back;
 
  bool empty() const {
    return front.empty() && back.empty();
  }
 
  size_t size() const {
    return front.size() + back.size();
  }
 
  SemiGroup fold_all() const {
    if(front.empty()) {
      return back.top().sum;
    } else if(back.empty()) {
      return front.top().sum;
    } else {
      return f(front.top().sum, back.top().sum);
    }
  }
 
  void push(const SemiGroup &x) {
    if(back.empty()) {
      back.emplace(x, x);
    } else {
      back.emplace(x, f(back.top().sum, x));
    }
  }
 
  void pop() {
    if(front.empty()) {
      front.emplace(back.top().val, back.top().val);
      back.pop();
      while(!back.empty()) {
        front.emplace(back.top().val, f(back.top().val, front.top().sum));
        back.pop();
      }
    }
    front.pop();
  }
};
#line 8 "test/verify/yosupo-queue-operate-all-composite.test.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int Q;
  cin >> Q;
  using pi = pair< mint, mint >;
  auto f = [](const pi &a, const pi &b) -> pi {
    return {a.first * b.first, a.second * b.first + b.second};
  };
  SlidingWindowAggregation< pi > swa(f);
  while(Q--) {
    int t;
    cin >> t;
    if(t == 0) {
      mint a, b;
      cin >> a >> b;
      swa.push(pi(a, b));
    } else if(t == 1) {
      swa.pop();
    } else {
      mint x;
      cin >> x;
      if(swa.empty()) {
        cout << x << "\n";
      } else {
        auto s = swa.fold_all();
        cout << s.first * x + s.second << "\n";
      }
    }
  }
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

