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


# :warning: math/verify/atcoder-arc-042-d.cpp
* category: math/verify


[Back to top page](../../../index.html)



## Code
```cpp
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

[Back to top page](../../../index.html)

