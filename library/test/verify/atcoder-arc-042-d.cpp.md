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


# :warning: test/verify/atcoder-arc-042-d.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/atcoder-arc-042-d.cpp">View this file on GitHub</a>
    - Last commit date: 2020-01-07 02:07:19+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define IGNORE

int64_t mod_pow(int64_t x, int64_t n, int64_t mod) {
  int64_t ret = 1;
  while(n > 0) {
    if(n & 1) (ret *= x) %= mod;
    (x *= x) %= mod;
    n >>= 1;
  }
  return ret;
}

int main() {
  int x, p, a, b;
  cin >> x >> p >> a >> b;

  if(p <= a) {
    int k = a / p;
    a -= k * p;
    b -= k * p;
  }

  if((b - a + 1) <= 10000000) {
    int64_t ret = infll;
    auto tmp = mod_pow(x, a, p);
    for(int i = a; i <= b; i++) {
      ret = min(ret, tmp);
      tmp = tmp * x % p;
    }
    cout << ret << endl;
  } else {
    for(int i = 1;; i++) {
      int tmp = mod_log(x, i, p);
      if((a <= tmp && tmp <= b) || (a <= tmp + p && tmp + p <= b)) {
        cout << i << endl;
        break;
      }
    }
  }
}


```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/atcoder-arc-042-d.cpp"
#define IGNORE

int64_t mod_pow(int64_t x, int64_t n, int64_t mod) {
  int64_t ret = 1;
  while(n > 0) {
    if(n & 1) (ret *= x) %= mod;
    (x *= x) %= mod;
    n >>= 1;
  }
  return ret;
}

int main() {
  int x, p, a, b;
  cin >> x >> p >> a >> b;

  if(p <= a) {
    int k = a / p;
    a -= k * p;
    b -= k * p;
  }

  if((b - a + 1) <= 10000000) {
    int64_t ret = infll;
    auto tmp = mod_pow(x, a, p);
    for(int i = a; i <= b; i++) {
      ret = min(ret, tmp);
      tmp = tmp * x % p;
    }
    cout << ret << endl;
  } else {
    for(int i = 1;; i++) {
      int tmp = mod_log(x, i, p);
      if((a <= tmp && tmp <= b) || (a <= tmp + p && tmp + p <= b)) {
        cout << i << endl;
        break;
      }
    }
  }
}


```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

