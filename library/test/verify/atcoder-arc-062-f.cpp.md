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


# :warning: test/verify/atcoder-arc-062-f.cpp
<a href="../../../index.html">Back to top page</a>

* category: test/verify
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-arc-062-f.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 23:02:43 +0900




## Code
{% raw %}
```cpp
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
};
 
using modint = ModInt< mod >;
 
template< typename T >
struct Combination {
  vector< T > _fact, _rfact;
 
  Combination(int sz) : _fact(sz + 1), _rfact(sz + 1) {
    _fact[0] = _rfact[sz] = 1;
    for(int i = 1; i <= sz; i++) _fact[i] = _fact[i - 1] * i;
    _rfact[sz] /= _fact[sz];
    for(int i = sz - 1; i >= 0; i--) _rfact[i] = _rfact[i + 1] * (i + 1);
  }
 
  inline T fact(int k) const { return _fact[k]; }
 
  inline T rfact(int k) const { return _rfact[k]; }
 
  T P(int n, int r) const {
    if(r < 0 || n < r) return 0;
    return fact(n) * rfact(n - r);
  }
 
  T C(int p, int q) const {
    if(q < 0 || p < q) return 0;
    return fact(p) * rfact(q) * rfact(p - q);
  }
 
  T H(int n, int r) const {
    if(n < 0 || r < 0) return (0);
    return r == 0 ? 1 : C(n + r - 1, r);
  }
};
 
int64_t euler_phi(int64_t n) {
  int64_t ret = n;
  for(int64_t i = 2; i * i <= n; i++) {
    if(n % i == 0) {
      ret -= ret / i;
      while(n % i == 0) n /= i;
    }
  }
  if(n > 1) ret -= ret / n;
  return ret;
}
 
int main() {
  int N, M, K;
  cin >> N >> M >> K;
  UnWeightedGraph g(N);
  Combination< modint > beet(101010);
  while(M--) {
    int x, y;
    cin >> x >> y;
    --x, --y;
    g[x].push_back(y);
    g[y].push_back(x);
  }
  BiConnectedComponents< UnWeightedGraph > bcc(g);
  bcc.build();
  modint ret = 1;
  for(auto &vs : bcc.bc) {
    set< int > vertex;
    for(auto &p : vs) vertex.emplace(p.first);
    for(auto &p : vs) vertex.emplace(p.second);
    if(vertex.size() == vs.size() + 1) {
      ret *= K;
    } else if(vertex.size() == vs.size()) {
      modint add = 0;
      for(int i = 1; i <= vertex.size(); i++) {
        if(vertex.size() % i == 0) {
          add += modint(K).pow(vertex.size() / i) * euler_phi(i);
        }
      }
      add /= vertex.size();
      ret *= add;
    } else {
      ret *= beet.H(K, vs.size());
    }
  }
  cout << ret << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

